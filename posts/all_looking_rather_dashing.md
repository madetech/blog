# All looking rather dashing

At Made we collect a lot of metrics. From projects, to servers, to support, to admin. All of these are stored in various services and it's not that easy to get quick and simple visibility of these.

Metrics such as error rates and response times are critical. If there is a sudden spike with one, then visitors' experiences to our clients websites can be serverely affected, which could result in loss of sales.

We have automated alerts when metrics hit particular thresholds so that someone is always able to respond. However, it's not just about putting out fires, but seeing things that could be better and optimised.

Besides wanting a dashboard with lots of squares, numbers and pretty colours,  we wanted to make these metrics visble to the entire team in the office wih just a quick glance. This sparks communication between the different teams and promotes knowledge share.

## Metrics, metrics, metrics

With a couple of hours dedicated to the dashboard project, and hundreds of metrics to pick from, we prioritised and picked four to focus on so that at the end of the day we'd have something usable. We selected:

 * Error rates
 * Deploy deltas
 * Apdex scores
 * Support hours

Being able to integrate with various services where this information was stored was essential so that we could pull this data out.

We compared a number of different hosted services based on how easily they integrated with these services, along with pricing and the look-and-feel of the dashboard itself (we wanted it to look nice afterall!) While the leaders in the market were impressive in the number of integrations they offered and the ease at which to set them up, when it came to demo'ing our initial setup to the rest of the team, it was clear that metrics that deserved some attention weren't getting noticed as they didn't stand out amongst the others.

## Visibility

This meant changing tact, and switching to [Dashing](http://dashing.io/), an open-source solution that gives us a lot more control. It's written in Ruby and CoffeeScript so we were able to jump in and customise right away.

The widgets that come with Dashing out of the box don't support changing the background colours of the tiles based on a conditional. For example, if an Apdex score went below `0.9` then we wanted the tile to turn yellow, and below `0.8` to turn red. 

However, there are some '[hidden](https://github.com/Shopify/dashing/blob/ca2dad41cdbfb766028de64b83a1623f2f9e372e/templates/project/assets/stylesheets/application.scss#L19)' styles under the hood that do exactly what we wanted; being able to switch to a red or yellow background when needed.

We created some new widgets based on the simple Text widget, and by hooking into the `onData` method we were able to alter the styling as needed:

```
onData: (data) ->
  score = support_hours / @daysInMonthRemaining()

  if score > 4
    $(@node).addClass('status-warning')
  else if score > 2
    $(@node).addClass('status-danger')
  else 
    $(@node).removeClass('status-warning status-danger')
```

As we have multiple projects, we decided on using a dashboard per metric, with a tile per project displayed. We then used [Sinatra Cyclist](https://github.com/vrish88/sinatra_cyclist) (Dashing is built with [Sinatra](http://www.sinatrarb.com/)) to cycle through the different dashboards every 25 seconds.

***

There's certainly a lot more we can do with our status dashboard. However, Thursday allowed us to build a good solid foundation. I'm sure we'll now add more to it. We'll need to try and get a good balance between helpful and important metrics while not trying to overcrowd it by providing too much data.
