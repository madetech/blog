#Practical Checkout Enhancements

At Made we pride ourselves on crafting websites that deliver a great aesthetic, and a rich user experience.

Over the last few years I have spent the majority of my time building eCommerce sites, were some good UX can make or break conversion rate, and profitability. 

In this post I am going to share a few ways to enhance your checkout flow, that will hopefully have positive effect.

##The Address Step

Nothing daunts a user more than a page full of form inputs, and within your checkout flow the biggest form - I hope - is customer address entry.

The first, and most obvious way to instantly halve the size of this form, is to allow the customer to use the same address for both their shipping, and billing address. From personal and professional experience this is best achieved using a simple check box. That in most cases can be preselected.

The second, is to remove the address fields all together and provide auto-complete suggestions based on postcode. There are a few services that can provide this for you. One that we've implemented a few times at Made, is Postcode Anywhere.

##The Payment Step

The taking of payment is arguably the most important part of your checkout process. And making it as quick, and simple as possible for a potential customer, will have positive effects on both conversion and customer satisfaction.

The obvious way to speed a registered customer through the payment step is offering to save their card details, and using those details for all future orders. But for those shopper who aren't returning account holders we can improve the way we collect that data.

Stripe have a great open source [jQuery plugin](https://github.com/stripe/jquery.payment) allows you to validate a customers card type and number. Its up to you how you display this back to a customer, but this early visual indicator will enable them to correct any mistakes in card details before they even submit their payment.

Another way we can improve the customer experience of the payment step, only really relates to mobile users, and the input types we use in the form itself.


##But... Why reinvent the wheel?
Its quite likely that your customers will already have an account with Amazon or PayPal - I mean who doesn't these days.

With some integration work, you can implement the checkout with PayPal (or Amazon) functionality. Yes it completely bypasses your own checkout flow, but is that a bad thing? By leveraging the addresses, and card details already stored on the customers preferred payment system, they can get from cart to confirmation in a few clicks.


##Conclusion
Whilst I know these suggestions aren't ground breaking, and don't reinvent the wheel you'd be surprised how often
