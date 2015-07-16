# Working Around IE7 When It Comes To Cross Browser Testing

We're getting ever closer to the point where we can finally stop supporting certain legacy browsers; [IE6 is officially dead](https://www.modern.ie/en-us/ie6countdown), and [the support Microsoft provides for clients running IE7 is extremely limited](https://support.microsoft.com/en-us/gp/microsoft-internet-explorer), but it's still not particularly uncommon to meet a client that requires support for IE7.

You may groan, you may even present a well thought out argument about how the less we support it the more we encourage people to move away from it and towards progress, but unfortunately a lot of corporate clients are locked into particular versions of Windows and, by extension, Internet Explorer. It costs money to upgrade them and, as the saying goes, if it ain't broke, don't do everyone (in our industry) a favour and upgrade it.

With one foot forcibly stuck in the past on such a project, every front end developer knows the mounting sense of dread as you build something that looks beautiful in a modern browser but hasn't yet been cross browser checked, only to find something resembling Frankenstein's monster when you finally do.

As a means to combat said monster, in this post I'll be detailing some of the more useful shims, polyfills, workarounds and ways to debug IE7 I've discovered.

## Setting Up Your Testing Environment

Here at Made, we're all on OSX, so finding a way to test on Windows was a priority. [BrowserStack](https://www.browserstack.com/) offer a nice solution for cross browser testing, but a far more cost effective way to test IE specifically is to take advantage of the virtual machines [modern.ie](http://dev.modern.ie/tools/vms/) provides.

There's no way to rollback to a previous version of IE once you have a later one installed, so if you need to test multiple versions, you'll need to download and install a separate VM for each one. It's unfortunate, as the VMs are huge, and can chew up your hard drive space pretty quickly.

IE7 proper doesn't have any useful developer tools, so it's impossible to debug javascript errors, a lot of which will occur only in IE7 and can have you tearing your hair out. Fortunately, the developer tools that come with more recent versions of IE allow you to simulate older versions, making it much easier to squash those bugs (I've found the IE11 on Windows 8.1 VM to be the most user friendly).

It's important to not lean too heavily on the simulated version of IE7 though, as it isn't a perfect simulation, and there will be small differences only present in true IE7. Do the majority of your cross browser testing/bug fixing in the simulation, and then boot up the IE7 VM to do a final sanity check.

## Setting Up Your Project

First things first; set a strict doctype, like so:

    <!doctype html PUBLIC "-//W3C//DTD HTML 4.0 Strict//EN">

This allows you to use certain CSS properties like `max-width` and `min-height`, and prevents IE7 from defaulting to quirks mode, which is meant to simulate bugs present in even older browsers.

Additionally, there will be a few instances where you need to apply certain styles for IE7 only, so make sure to include some conditional html tags that'll make it easy to target:

    <!--[if IE 7 ]> <html class="ie7"> <![endif]-->
    <!--[if gte IE 8]><!--> <html> <!--<![endif]-->

You can also include multiple conditional tags if you want to specifically target other versions of IE.

We use SCSS on all of our projects, so adding that class allows us to do the following:

    .foo {
      // some styles

      .ie7 & {
        // some IE7 specific styles
      }
    }

(or you could also the much nicer looking [when-inside mixin](https://www.madetech.com/news/brevity-vs-comprehensibility))

Another great tool to include whilst setting your project up is [Modernizr](http://modernizr.com/). Not specific to IE7, Modernizr detects exactly what the current browser is and isn't capable of, and then adds classes to the html tag indicating what it finds. For example, if your browser is a legacy browser that doesn't support media queries, it'll add a `no-mq` class that you can target in much the same way as the `ie7` class in the example above.

## [Polyfills](https://en.wikipedia.org/wiki/Polyfill)

There's an [exhaustive list](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills) of cross browser polyfills, but I'm going to talk about a couple I've gotten the most use out of:


### Box-sizing

The `box-sizing` CSS property wasn't introduced until IE8, and using:

    * { box-sizing: border-box; }

is quite a nice way to avoid having to do lots of mental gymnastics when calculating padding, width and margins. IE7 has no support for this whatsoever, so your layouts will tend to look a bit malformed in it.

The [box-sizing polyfill](https://github.com/Schepp/box-sizing-polyfill) by [Christian Schaefer](https://twitter.com/derSchepp) is a great solution to the problem. Add the htc file to your project, and then update your CSS like so:

    * { box-sizing: border-box; *behavior: url(/polyfills/boxsizing.htc);}

This will immediately fix the majority of layout issues you come across. That said, I have witnessed the polyfill cause strange issues on certain elements, such as ignoring all width styles completely on elements that are dynamically hidden and shown by javascript, and on input fields, which continuously shrink on `focus` and `blur` events, to the point that the text being input can't be read. In these cases, simply removing the behaviour fixes the issue:

    .foo {
      // some styles

      .ie7 & {
        * { box-sizing: border-box; *behavior: none; }
      }
    }

### Console.log

You shouldn't have `console.log` commands lying around in code that's ready to go to production, but in development and staging environments they can be useful for debugging, unless you're in IE7, which doesn't know what to do with `console` and prevents all of your nice js-powered interactions from working.

The fix is to add [this polyfill](https://github.com/paulmillr/console-polyfill) by [Paul Miller](https://twitter.com/paulmillr) to the top of your javascript:

    (function(global) {
      'use strict';
      global.console = global.console || {};
      var con = global.console;
      var prop, method;
      var empty = {};
      var dummy = function() {};
      var properties = 'memory'.split(',');
      var methods = ('assert,clear,count,debug,dir,dirxml,error,exception,group,' +
         'groupCollapsed,groupEnd,info,log,markTimeline,profile,profiles,profileEnd,' +
         'show,table,time,timeEnd,timeline,timelineEnd,timeStamp,trace,warn').split(',');
      while (prop = properties.pop()) if (!con[prop]) con[prop] = empty;
      while (method = methods.pop()) if (!con[method]) con[method] = dummy;
    })(typeof window === 'undefined' ? this : window);

## Workarounds

One of the dirtier workarounds I discovered recently, which I frankly didn't know was even possible, was how to deal with the `:before` and `:after` pseudo elements in IE7.

We use [Icomoon](https://icomoon.io/app/) a lot for our icons; icon fonts are a nice solution for creating icons that look great on any device. In this particular project, we have an icomoon mixin that looks like this:

    @mixin icomoon($icon) {
      font-family: 'icomoon';
      speak: none;
      font-style: normal;
      font-weight: normal;
      font-variant: normal;
      text-transform: none;
      line-height: 1;

      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;

      &:before {
        content: $icon;
      }
    }

However, icon fonts require using psuedo elements, which IE7 simply doesn't see. After some searching, I found the solution to this problem: javascript <em>within</em> css. By adding the following the above mixin:

    *zoom: expression(
      this.runtimeStyle['zoom'] = '1', this.innerHTML = '#{$icon}'
    );

We're able to target IE by using a CSS property only it will see (`*zoom`), and sneak in some javascript so that it will set the icon as the content within the element, bypassing the need for the psuedo element.

This workaround has similarities to a much more innocent workaround, for `display: inline-block`. IE7 doesn't recognise `inline-block` at all, but you can achieve the same effect with the following well-known workaround:

    display: inline-block;
    *display: inline;
    *zoom: 1;

All other browsers ignore CSS properties prefixed with `*`, but IE won't. What `zoom` does is trigger [hasLayout](https://msdn.microsoft.com/en-us/library/bb250481(v=vs.85).aspx) on the element, which gives it `block` properties and, combined with `*display: inline;`, gives us the desired result. Of course, if you're using Compass with your SCSS, that's wrapped up for you in [their mixin](http://compass-style.org/reference/compass/css3/inline_block/).

There are many workarounds for the roadblocks IE7 throws up, and these are just a few that I hope others will find useful, but please, feel free to share any others that have saved you valuable time!
