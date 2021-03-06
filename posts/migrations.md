# Migrations, seeds and pipelines

Most applications you write rely on certain data stored in a database that is essential for it to work. That data defines your business logic as much as the code. That data should be represented _in_ code. In this post I'll discuss how we handle migrations and seed data through our Continuous Delivery pipeline at Made.

If you're currently practising this correctly, you'd be able to delete your database and migration files, and be in a production-like state in less than a minute with a couple of commands. You don't want to have to manually setup—or try and remember—what data you need so that you're in a position to code if you're starting afresh.

You should only need to run `rake db:setup` or `rake db:reset` if you've already got a database created. These commands will handle the setting up of the structure (or schema) of your database, and the data that it contains.

## Schema

As you're building your app, you write migrations incrementally as you go along. You run `rake db:migrate` so that your database structure is altered and for the changes to be reflected in your `db/schema.rb` file. This is the single source of truth for the current structure of your database.

When you or another developer wants to work on the project, you should be able to just run `rake db:setup` in order for the database to be created, and for the current version of your schema to be setup. There's no need to run the migrations for a fresh project clone. Why run through each migration sequentially when `db/schema.rb` has the end result?

As you continue to develop the project in a team, add more migrations, you'll want to run `rake db:migrate` to get the latest changes that differ from what you already have.

## Data

Migrations are a means to alter your database schema, but also can potentially be used to alter the data contained within it. You might have used a migration to populate your app data, or have done it manually via an admin interface or the Rails console. But the thing to bear in mind is that your `db/schema.rb` file only contains your database structure. The data you add to the database isn't persisted anywhere in code. So if you have to reset your database, or someone new works on the project, if they run a `rake db:setup` they'll get a database with the correct structure and zero data.

_An example Rails migration:_

```
class AddPreferencesToSpreeOrders < ActiveRecord::Migration
  def change
    add_column :spree_orders, :preferences, :text
  end
end
```

_The changes in this file will be reflected in the `db/schema.rb` file._

This is where `db/seeds.rb` comes in handy. This file is to data what `db/schema.rb` is for the structure. The difference though is that you have to manage this file yourself. When you create a migration that alters the data somehow, Rails won't be updating the `db/seeds.rb` file for you.

_An example Rails seed file:_

```
Spree::ReturnAuthorizationReason.create!(name: 'Not satisfied with the item')
Spree::ReturnAuthorizationReason.create!(name: 'Colour appearance')
Spree::ReturnAuthorizationReason.create!(name: 'Wrong size')
```

_And corresponding migration file to include it:_

```
class SeedDefaultReturnAuthorizationReasons < ActiveRecord::Migration
  def change
    Spree::ReturnAuthorizationReason.delete_all
    require_relative('../seeds/return_authorization_reasons')
  end
end
```

_Anything altered in the database as a result of this migration will not be reflected in the `db/schema.rb` file._

When you run `rake db:setup` or `rake db:reset` Rails will create/empty your database, load your current schema, and then run the `db/seeds.rb` file to populate  the database. By mirroring the data your app requires in code in the `db/seeds.rb` file, you can get yourself or others up to speed much quicker. That may be a set of categories, tags or users, for example.

Breaking down your seed data into multiple files helps you organise it into logical pieces. `require_relative` is your friend to load in additional files. Setting up a bunch of users? Throw that all in a `db/seeds/users.rb` file. Then `require_relative('seeds/users.rb')` in your `db/seeds.rb` file.

## Up the pipeline

This isn't to say that you should stop writing migrations and use seeds solely as a means to get your data into your database. It's not practical to reset your database everytime, nor can you expect other developers on your team to do this. You'll want to get the data into your local environment via a migration as you want to be sure it works fine for others. 

Also, because you probably have a Continuous Delivery pipeline (right?) where you need to get seed data up to your production environment, it's completely unrealistic to reset the production database. Migrations are the only solution. This is why it's important that the data in your migrations and seed data mirror one another so that if someone were to do a `db:reset` they'd have that same data as if it were added via a migration.

## Graveyarding

Once your migrations have been pushed through your pipeline, and your `db/seeds.rb` file is current, it's safe to delete your old migrations. Though I'd recommend keeping the last 5 just in case you're developing, trying something out, and may need to revert back.

## Summary

Discipline is essential. And the best way to make sure you're disciplined is to not be afraid to run a `rake db:reset` every so often. If there's something you find yourself manually adding to the data, it probably belongs in a seed. If you're ever tempted to add something to the db that is essential and should be in code, then:

 1. Write a migration with the change
 2. Ensure that the data the migration is changing is reflected in `db/seeds.rb` so that if you `rake db:reset` you'd have the same state of data
 3. Push the migration through your pipeline
 4. Remove all but the last 5 migrations in your project to keep things clean

