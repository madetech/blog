# When to avoid the DRY principle

The Don't Repeat Yourself principle is probably one of the most widely
recognised software design patterns out there. Most beginners in the industry
will have heard of it. More seasoned engineers will have taken it further and
will see it's use in other design patterns such as
[Service-Oriented Architecture][1], [Inversion of Control][2] and
[Composability over inheritance][2].

It's easy to see why DRY is so well known as it's self explanatory, or at least
it is on the surface. To follow, don't repeat yourself. If you see a block of
code that looks similar or the same as a block of code in another file you'll
likely think to yourself, how can I abstract that?

DRY is all about abstraction. Abstraction is the use of interfaces such as
functions and classes to hide away implementation details. It's the method by
which you keep related bits of code together. Instead of writing 5 lines of code
to print a web page when a button is clicked, you may well place those 5 lines
in a function called `printPage()`. Abstraction is related to DRY in that when
you place related pieces of code together, they are easier to reuse and you end
up repeating yourself less. Therefore we can apply abstraction to DRY up our code.

Spotting and abstracting repetition isn't always obvious, it can get a little
nuanced at times. The more experienced engineer may spot less obvious
repetition. They might spot that in an e-commerce application there are multiple
places where products are selected from a collection based on some criteria and
then some action is performed on those products. They might choose to abstract
the filter and map operations on the collection of products into a reusable
class. Someone less experienced might not see this abstraction straight away.

## DRY might not always be the best idea

So we have this principle which is understood right from the start. You move
repetition into methods. It turns out a lot of code is repetitive. In some
languages you might use a for loop in nearly every file, should you abstract a
loop? The answer is: sometimes.

Like all things too much can be a bad thing. Sometimes the principle can be
taken too far, you can get too clever and end up with something that is harder
to understand or work with. I'd like to suggest a few situations where the
principle might not be so useful.

### Unnecessary abstraction

Repetitive code can often be abstracted unnecessarily. Feature testing in RSpec
is a good example of this. A lot of us in the world of rails test features using
capybara a library for interacting with web pages. Often you will visit a page
and then perform an action on the page. Let's look at an example:

``` ruby
feature 'Adding product to cart' do
  scenario 'Adding in stock product' do
    when_a_shopper_adds_an_in_stock_product_to_cart
    then_they_should_see_the_product_in_the_cart
  end

  def when_a_shopper_adds_an_in_stock_product_to_cart
    visit product_path(product)
    click_button 'Add to cart'
  end

  def then_they_should_see_the_product_in_the_cart
    visit cart_path
    expect(page).to have_content(product.name)
  end

  private

  let(:product) { create(:product) }
end
```

This is a feature for adding a product to cart. The when step contains some
capybara functions to add the product. Let's implement adding to cart from
another page. Seeing as it's still about adding to cart there must be something
that will want DRYing up.

``` ruby
feature 'Adding product to cart' do
  scenario 'Adding in stock product' do
    when_a_shopper_adds_an_in_stock_product_to_cart
    then_they_should_see_the_in_stock_product_in_the_cart
  end

  scenario 'Adding product from listing page' do
    when_a_shopper_adds_a_product_to_cart_from_listing_page
    then_they_should_see_the_product_in_the_cart
  end

  def when_a_shopper_adds_an_in_stock_product_to_cart
    add_to_cart_from product_path(product)
  end

  def then_they_should_see_the_in_stock_product_in_the_cart
    assert_product_in_cart
  end

  def when_a_shopper_adds_a_product_to_cart_from_listing_page
    add_to_cart_from products_path(category: product.category)
  end

  def then_they_should_see_the_product_in_the_cart
    assert_product_in_cart
  end

  private

  let(:product) { create(:product) }

  def add_to_cart_from(path)
    visit path
    click_button 'Add to cart'
  end

  def assert_product_in_cart
    visit cart_path
    expect(page).to have_content(product.name)
  end
end
```

Okay so there are two methods that we've abstracted here  `#add_to_cart_from`
and `#assert_product_in_cart`. In this case I would say that `#add_to_cart_from`
is bordering unnecessary since we're just saving one line and the method body
could even be perhaps more descriptive than the method name, that said let's
keep it for now. The `#assert_product_in_cart` is a common pattern in my feature
specs. I like assertions to be clear in their nature so I find abstracting them
even if they aren't used in multiple scenarios useful.

Now let's say we're testing a related feature, recommended products. We want to
test that when we add a product to cart products are recommended on the cart
page.

``` ruby
feature 'Cart product recommendations' do
  scenario 'Recommending products' do
    when_a_shopper_visits_their_cart
    then_they_should_be_recommended_products
  end

  def when_a_shopper_visits_their_cart
    add_to_cart_from product_path(product)
    visit cart_part
  end

  def then_they_should_be_recommended_products
    product.recommendations.each do |recommendation|
      expect(page).to have_content(recommendation.product.name)
    end
  end

  private

  let(:product) { create(:product, :with_recommendations) }

  def add_to_cart_from(path)
    visit path
    click_button 'Add to cart'
  end
end
```

You'll notice `#add_to_cart_from` is duplicated in this feature. We could have
places this method in a module that could be included in both features but why?
What real benefit does this give us? Okay we don't repeat the definition of the
function. The costs? Well you need to look in multiple files instead of one to
understand and work with two features. For me I'd say it isn't worth it.

### Clever abstraction

Now let's say we want to add another scenario to our add to cart feature but
this time for a sized product. Let's be a little clever and be DRY up front.
Both the when and then logic will be similar so lets reused them.

``` ruby
feature 'Adding product to cart' do
  scenario 'Adding in stock product' do
    when_a_shopper_adds_an_in_stock_product_to_cart
    then_they_should_see_the_product_in_the_cart
  end

  scenario 'Adding in stock product with size' do
    when_a_shopper_adds_an_in_stock_product_to_cart(sized: true)
    then_they_should_see_the_product_in_the_cart(sized: true)
  end

  def when_a_shopper_adds_an_in_stock_product_to_cart(options = {})
    if options[:sized]
      visit product_path(sized_product)
      select sized_product.sizes.first, from: :cart_product_size
    else
      visit product_path(product)
    end

    click_button 'Add to cart'
  end

  def then_they_should_see_the_product_in_the_cart(options = {})
    visit cart_path
    expect(page).to have_content(options[:sized] ? sized_product.name : product.name)
  end

  private

  let(:product) { create(:product) }
  let(:sized_product) { create(:product, :with_sizes) }
end
```

We've added an options argument to both methods and added some if logic into
them. With the use of if statements we've handled both scenarios from within
one set of functions. What have we really gained here though? This is basically
being clever for the sake of it.

Instead we could write out more specific when and then methods that are easier
to understand. Instead of providing arguments to the when and then why don't we
create unique methods per scenario.

``` ruby
feature 'Adding product to cart' do
  scenario 'Adding in stock product' do
    when_a_shopper_adds_an_in_stock_product_to_cart
    then_they_should_see_the_product_in_the_cart
  end

  scenario 'Adding in stock product with size' do
    when_a_shopper_adds_an_in_stock_sized_product_to_cart
    then_they_should_see_the_sized_product_in_the_cart
  end

  def when_a_shopper_adds_an_in_stock_product_to_cart
    visit product_path(product)
    click_button 'Add to cart'
  end

  def then_they_should_see_the_product_in_the_cart
    visit cart_path
    expect(page).to have_content(product.name)
  end

  def when_a_shopper_adds_an_in_stock_sized_product_to_cart
    visit product_path(sized_product)
    select sized_product.sizes.first, from: :cart_product_size
    click_button 'Add to cart'
  end

  def then_they_should_see_the_sized_product_in_the_cart
    visit cart_path
    expect(page).to have_content(sized_product.name)
  end

  private

  let(:product) { create(:product) }
  let(:sized_product) { create(:product, :with_sizes) }
end
```

Okay so we've got a few more lines of code and it isn't as *clever*. What do
we gain? We gain easier to read method names, simpler methods that contain
no conditional logic and do what they say on the tin.

Sometimes abstraction can compromise readability so following DRY blindly, or
getting excited by a way of writing less lines of code can often mean your code
is a little harder to read and understand. These examples are simple but I've
seen some pretty bad cucumber steps with nested if statements in the past.
Simple and stupid is good enough for me!

### Wrong abstraction

Okay, time to write a feature for the checkout. We want to run through every
step as a single scenario. The later steps are going to need the previous steps
to have already run, however like good developers we do not share state between
scenarios. Let's be naughty and reuse our steps in subsequent scenarios.

``` ruby
feature 'Checkout' do
  scenario 'Adding address' do
    when_a_shopper_is_ready_to_checkout
    then_they_should_have_to_add_their_address_details
  end

  scenario 'Choosing delivery method' do
    given_a_shopper_has_added_their_address
    when_they_want_a_fast_delivery
    then_they_should_be_able_to_choose_next_day
  end

  scenario 'Paying for order' do
    given_a_shopper_is_ready_to_pay
    when_they_want_to_pay_by_paypal
    then_they_should_be_redirected_to_paypal
  end

  def when_a_shopper_is_ready_to_checkout
    # add product to cart
  end

  def then_they_should_have_to_add_their_address_details
    # fill in address details
  end

  def given_a_shopper_has_added_their_address
    when_a_shopper_is_ready_to_checkout
    then_they_should_have_to_add_their_address_details
  end

  def when_they_want_a_fast_delivery
  end

  def then_they_should_be_able_to_choose_next_day
    # choose next day
  end

  def given_a_shopper_is_ready_to_pay
    when_a_shopper_is_ready_to_checkout
    then_they_should_have_to_add_their_address_details
    when_they_want_a_fast_delivery
    then_they_should_be_able_to_choose_next_day
  end

  def when_they_want_to_pay_by_paypal
    # select paypal
  end

  def then_they_should_be_redirected_to_paypal
    # assert current url is paypal
  end
end
```

I've left out the implementation of the steps but you get the picture. The
given methods of subsequent scenarios reuse previous steps. Now this may be DRY
but we've missed a couple of issues.

Firstly, running capybara steps is much slower than operating directly on a DB.
Instead of running through the browser in given steps, we could use factories
that setup the DB in the right state. This means capybara only tests each step
once. The alternative would be just to have one large scenario which I've seen
done before. I prefer splitting them out so that I can just run the one test
when working on a checkout step.

Second to that we are using given/when/then steps inside of other given steps.
Reading through the code makes sense but it could be a little terser and more
specific to the current test.

With these points in mind we can reimplement the feature:

``` ruby
feature 'Checkout' do
  scenario 'Adding address' do
    when_a_shopper_is_ready_to_checkout
    then_they_should_have_to_add_their_address_details
  end

  scenario 'Choosing delivery method' do
    given_a_shopper_has_added_their_address
    when_they_want_a_fast_delivery
    then_they_should_be_able_to_choose_next_day
  end

  scenario 'Paying for order' do
    given_a_shopper_is_ready_to_pay
    when_they_want_to_pay_by_paypal
    then_they_should_be_redirected_to_paypal
  end

  def when_a_shopper_is_ready_to_checkout
    # add product to cart
  end

  def then_they_should_have_to_add_their_address_details
    # fill in address details
  end

  def given_a_shopper_has_added_their_address
    jump_to_checkout(:delivery_step)
  end

  def when_they_want_a_fast_delivery
  end

  def then_they_should_be_able_to_choose_next_day
    # choose next day
  end

  def given_a_shopper_is_ready_to_pay
    jump_to_checkout(:payment_step)
  end

  def when_they_want_to_pay_by_paypal
    # select paypal
  end

  def then_they_should_be_redirected_to_paypal
    # assert current url is paypal
  end

  private

  def jump_to_checkout(step)
    order = create(:order, :jump_to_step, step: step)
    visit checkout_path(order_token: order.token)
  end
end
```

We have now moved the order creation into a factory. This means we can get more
performant tests. I'd argue that the DRY principle helped us here in seeing that
we were repeating ourselves. The solution was not to reduce the repetition by
reusing steps, that was the wrong abstraction. The right abstraction that gave
us performance benefits was to move into a factory.

Not only was the reuse of capybara steps the wrong abstraction due to
performance, it was also the wrong level of abstraction. I see three levels of
abstraction in a feature spec. The scenario, the steps and then the helpers.
The scenario is isolated inside the do block by RSpec. I separate steps and
helpers with the private keyword. Each level of the abstraction should never
use other methods at the same level of abstraction, they should only call lower
levels of abstraction. The fact we had given steps calling other steps broke
this abstraction layering.

I use abstraction layering as a way of detecting problems in code. I can and
will write a whole article on it eventually. It's a method for structuring your
code so that related methods are found together, and that the various layers
of your application do not cross concerns. Until I write my post, take me at my
word that it's a good idea to use this abstraction layering when thinking about
the DRY principle.

Hopefully I haven't put you off DRY. It's an awesome tool. You just need to be
careful on how you solve it and sometimes it isn't a problem that needs solving.
Let me know what you think on twitter @LukeMorton.

[1]: https://en.wikipedia.org/wiki/Service-oriented_architecture
[2]: https://en.wikipedia.org/wiki/Inversion_of_control
[3]: https://en.wikipedia.org/wiki/Composition_over_inheritance
