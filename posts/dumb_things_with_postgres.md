# Doing dumb things with Postgres

A couple of months ago I gave a talk about PostgreSQL, and specifically using the Array datatype at [London Ruby User Group](https://skillsmatter.com/skillscasts/9865-london-ruby-lightning-talks) and I wanted to take some time to dive into this in more detail.

I've been fascinated with the Array datatype from Postgres and using it in Rails since it became usable in 2014, at the time I worked for a company that used Postgres for all of the new projects and several came up where it fitted in nicely with the work we were doing. Based on this I decided to give it a go and see what benefits we could gain and also try to work out any major pitfalls.

The array datatype works exactly as expected, instead of storing an string or integer it instead allows you to save arrays of these types. We used these for all sorts of things; from storing article tags and CSS classes to storing multiple associations without the use of a joining table. The latter usage is the area I became most involved an interested in. Given the product we worked on would be mainly used in a read heavy manner the additional overhead of joining tables could occassionally cause bottlenecks, especially on more complicated projects, by leveraging arrays, Rails caching and some code that I've come to regret we were able to mitigate these.

Example:

You have a series of news articles that can have associated tags that we use to find other articles, normally you would do this by implementing this;

Articles Table -> Taggings joining table -> Tags Table

# PUT DIAGRAM/screenshot ABOVE

Using the array datatype you could instead have;

Articles Table -> Tags Table

# PUT DIAGRAM/screenshot ABOVE

Doing this provides us a couple of advantages, with caching this can be noticeably faster than joining the 3 seperate tables and provides us a clean datastructure that we don't have to manipulate or `pluck` from to get the thing we care about, in this case the tag IDs. It also allows us to easily execute some very basic SQL to find articles that have the same tags as the current one being shown to the site user.

```ruby
class Article < ActiveRecord::Base
  # all the other logic

  def associated_articles
    Article.where.not(id: self.id).where("tags = ANY(#{self.tags})")
  end
end
```

If you've been using Rails/Postgres over the past couple of years this might be very run of the mill so lets dive into some of the madness you can cause.

Example:

A customer already has a series of one to one relations like Products to Product Categories but they now want this to be a many to many relation. They've already input lots of data and if possible they want to keep this. The obvious solution would be to create a joining table, iterate over the existing products and create entries for each of the associations and then drop the columns, I instead decided to do something a bit more out there, what if we could convert this integer column over to an array column while keeping all the existing data and not have to iterate over everything that's already there. To do this you'll need a really weird migration like this;

```ruby
class ChangeXIdColumn < ActiveRecord::Migration
  def up
    remove_index :products, :product_category_id
    change_column :products, :product_category_id, 'integer[] USING ARRAY[product_category_id]::INTEGER[]', array: true, null: false, default: []
    rename_column :products, :product_category_id, :product_category_ids
    add_index :products, :product_category_ids, using: 'gin'
  end

  def down
    raise ActiveRecord::IrreversibleMigration
  end
end
```

There's a lot going on in this migration so I'll break it down a bit.
```ruby
  change_column :products, :product_category_id, 'integer[] USING ARRAY[product_category_id]::INTEGER[]', array: true, null: false, default: []
```
This line takes our existing foreign key column and converts it to and array type, the SQL being executed recasts the existing data in the correct format so `4` would become `{4}`. The curly braces are how Postgres denotes an array, when returned by ActiveRecord the data would be represented as a standard array.

```ruby
  add_index :products, :product_category_ids, using: 'gin'
```
This is clearly an index, the important part however is that it's using "GIN" as it's index type. GIN is lossless versus GiST, the other index type available, which is lossy introducting the chance for incorrect results slightly. In practice it probably won't make a huge amount of difference to you which one you use but if you want to read more on these types I'd recommend the [Postgres documentation](https://www.postgresql.org/docs/current/static/textsearch-indexes.html). One thing to watch out for is that GIN indexes can have long build times but there are ways to mitigate that.

It's interesting to note that by choosing not to sort this array and restore it would allow the potential of using `SELECT unnest(arr[1:array_length(arr, 1)][1]) as id from data` or similar to get the first item to create a reversible migration. This is only advisable as a thought exercise and I'd recommend you _never_ do that.

The first snag we'll hit here is that we no longer have support for any of the Rails nicities around associations like `has_many` you can solve this by using code similar to the example above;

```ruby
  def product_categories
    ProductCategories.where(id: self.product_category_ids)
  end
```

This will return all the Product Categories that have been saved in the Products `product_category_ids` column in the same way as `has_many` would. One of the biggest issues I have with using arrays like this is the amount of boiler plate code you end up writing due to losing the ActiveRecord association behaviours but like I said sometimes the speed benefits on a read heavy site outweigh this.

There's also the concern that when this is shown to the end user it can introduce a lot of delay to loading if there are lots of associations, the main way I've found around this was to update a cache in Redis or similar every time a Product is updated. You can also make this even less blocking if you pass it off to a queuing system rather than blocking the update/create actions.

I'd also like to throw out an honourable mention to the [PostgresExt gem](https://github.com/DockYard/postgres_ext) for providing native support for [querying the array datatype (and others)](https://github.com/DockYard/postgres_ext/blob/master/docs/querying.md#arrays) natively via Arel.

Overall I think there are some amazing things you can do with PostgreSQL's array datatype in association with Rails but it's a very sharp and dangerous knife at times and truly requires you to be aware of what you're trying to do at all times.
