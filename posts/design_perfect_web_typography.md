#Design perfect Web Typography

Longstanding was the battle between designer and front end engineer in regards to having fonts render perfectly as per the design, and consistently between different browsers and operating systems. In even darker days, designers were lucky to get a custom font face.

Thankfully those days are behind us. This is largely because browser vendors (Google, Mozilla, Microsoft, and Opera) have started implementing the working draft of CSS Level 3 (CSS3). This, in turn, has lead to the release of a number of great JavaScript plugins that can enable us to create the right typographic layouts; there is a new hope for pixel perfect web typography.

So what exactly are the these new features? Chances are you've already been using them, albeit unknowingly, but in this article I'll cover some of these new features, how to implement them, what impact they can have, and I'll maybe even share a rendering fix for Internet Explorer (because, Spoiler Alert, there is one).

In addition to the new CSS3 features we'll also look at some existing CSS2 attributes which, when used in the correct manner, can also be just what you need.

##The CSS

###Font weight synthesis AKA "Mystery Emboldening"
The font face rule is now quite commonplace, but have you ever noticed that in some browsers - such as Chrome - if you don't have a matching font-weight (e.g. bold) for your webfont, the browser will help you out by artificially emboldening your regular type face (usually with varying degrees of success)? Well, this is the browser synthesizing the missing typeface. You'll see the difference below in these examples.

Fig. 1 - Missing typeface:
http://codepen.io/SebAshton/pen/VeVJLq

Fig. 2 - Typeface present:
http://codepen.io/SebAshton/pen/xZQoGj

Some _might_ see this as desirable behaviour, as it's better to have a bold weight than none at all. However, I am of the opinion that this font rendering isn't correct, and we as developers should stop this from happening. The addition of the `font-synthesis` attribute at a global level will suffice in solving this rendering quirk. Which means you'll notice when you've not selected the right weight.

```css
* { font-synthesis: none; }
```

Fig. 3 - Font synthesis off (Firefox only)
http://codepen.io/SebAshton/pen/BjGgoy

###Tracking
Often we are handed a design where the designer has tweaked the tracking - or letter spacing as its referred to in CSS - of the font, in order to "tighten up" the design. As long as this change is across the whole body of text, it is quite straight forward to match the letter-spacing.

In the past I've used this mixin to convert the PSD tracking value to ems. It's always best to specify letter spacing in ems - especially for responsive layouts - as it means you can redefine the font size and the letter-spacing will scale.

```sass
@mixin tracking($spacing) {
  letter-spacing: ($spacing / 1000) * 1em;
}
```

Fig. 4 - Differently tracked text.
http://codepen.io/SebAshton/pen/obQrYJ

However if the design does require more in-depth and accurate kerning, as opposed to tracking (the difference between the two is explained [here](https://creativemarket.com/blog/2014/09/18/whats-the-difference-between-leading-kerning-and-tracking)) then you'll need to employ some JavaScript, but I'll cover more on that later.

###Leading and line height
Leading isn't the same as line-height in CSS. Leading is in fact the half difference between the font-size and line-height.

Line-height isn't something new, but worth briefly mentioning for an accessibility reason. For big blocks of text (e.g. an article or a blog post) line-height should be at least 1.5 times the font size according to (WCAG rule 1.4.8.4)[https://www.w3.org/TR/WCAG20/#visual-audio-contrast-visual-presentation] which is easily achieved using ems.

Fig. 5 - Em based line heights
http://codepen.io/SebAshton/pen/YwdXxa

###Font features
One of the biggest typography features to arrive with CSS3 is the ability to enable OpenType font (OTF) features, of which there are a lot. [Typekit](http://help.typekit.com/customer/portal/articles/1789736) have an awesome article explaining them all in great detail, which I'll refrain from repeating here.

I will, however, demonstrate how to use a common font feature: enabling ligatures.

Fig. 6 - Ligatures in Lato.
http://codepen.io/SebAshton/pen/MKZYaB

Typically OTF WebFonts with font features are a bigger download for a user, so this might put you off using them. However, using them generally makes your long form copy look a lot nicer, and will deliver a better aesthetic.

It's worth noting that specifying `text-rendering: optimizeLegibility` will also add ligatures to your text. As a side note, this is one reason why you should only add this property in areas where you definitely want ligatures.

###Kerning
Kerning is defined as "the process of adjusting the spacing between characters in a proportional font, usually to achieve a visually pleasing result" by (Wikipedia)[https://en.wikipedia.org/wiki/Kerning], which is pretty accurate.

In CSS there are a couple of ways to enable kerning, the first being `text-rendering` which can have mixed results, and the second being `font-kerning`. Due to browser support it's probably worth specifying both, and (as noted above) you'll get the added bonus of enabling ligatures too!

Fig 7. - Un-kerned and kerned text.
https://codepen.io/SebAshton/pen/XXoJpQ

And also like ligatures, text kerning can be enabled using font-features.

###Font smoothing
There are a lot of [articles](https://davidwalsh.name/font-smoothing) in support of using font-smoothing in your CSS and quite a few [against](http://usabilitypost.com/2012/11/05/stop-fixing-font-smoothing/) it, with the arguments centering, respectively, around making the text more attractive, and usability.

Personally, I always specify it in my CSS, as it does make the fonts look a lot crisper, especially at low font weights.

Fig 8. - Font smoothing at low font weight
http://codepen.io/SebAshton/pen/KVbwrb

However, this is a Mac only feature. To get your fonts rendering nicely on Windows you'll need to employ [ClearType](https://blogs.msdn.microsoft.com/ie/2010/11/03/sub-pixel-fonts-in-ie9/). ClearType is enabled using a meta tag in the `head` of your html.

`<meta http-equiv="cleartype" content="on" />`

Also, while we're on on the subject of font rendering and Internet Explorer, there is another meta tag that could make your life easier if you are having issues with the appearance of your font on older versions of the browser we love to hate.

`<meta http-equiv="X-UA-TextLayoutMetrics" content="gdi" />`

This meta tag will turn off the inter-pixel spacing in IE9+ and uses [GDI metrics](https://msdn.microsoft.com/en-us/library/ff986079(v=vs.85).aspx) instead.

##JavaScript Solutions
We can't talk about web typography and not mention a few of the JavaScript solutions available on the Internet.

Two such solutions are [letteringjs](http://letteringjs.com) and [kerningjs](http://kerningjs.com/), and both achieve their tweaks in a similar way, with the former being a touch more manual than the latter.

The method they both use to achieve this is to wrap each character of the string in a `<span>`. This will make your generated markup look ugly, but it allows you to fine tune the kerning and vertical positioning.

It's worth noting that if accessibility is a priority for your site, screen readers will pause on each span, which isn't ideal. This can be overcome by adding aria-* attributes on the spans, which is something [letteringjs](https://github.com/davatron5000/Lettering.js/blob/master/jquery.lettering.js#L20) does do.


###External Links
[OpenType Font Features in CSS](http://help.typekit.com/customer/portal/articles/1789736)
[State of Web Type](http://www.stateofwebtype.com/)
[CSS Fonts 3](https://drafts.csswg.org/css-fonts-3)
[CSS Fonts 4](https://drafts.csswg.org/css-fonts-4)


Image, a CSS version of http://www.better2web.com/djfiles/typography-b2w.jpg
