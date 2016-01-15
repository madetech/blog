#Design perfect Web Typography

Longstanding is the battle between Designer and Front end engineer with regard to getting font rendering design perfect consistently between different browsers, and operating systems. In the dark days designers were lucky to get a custom font face.

However since vendors started implementing the working draft of CSS Level 3 (CSS3) there has is a new hope for pixel perfect web typography.

Some of the new properties and attributes unlock font features, whilst others provide better control over how the browser renders your web font.

###Font weight synthesis
Ever noticed how in some browser - like Chrome - if you don't have a bold font specified it will bolden your regular type face, to a varying degree of success? Well this is the browser synthesizing the missing typeface.

Whilst you _might_ want this ugly attempt at font weight or style you can keep it. However if you long for the control (I mean who doesn't!?) then specify `font-synthesis` at a global level.

```css
font-synthesis: none;
```

###Tracking

```sass
@mixin tracking($space) {
  letter-spacing: ($space / 1000) * 1em;
}
```

###Leading
Leading, or as its better known in CSS line-height

##Font Features
One of the biggest typography features to drop in CSS3 is the ability to enable OpenType font (OTF) features, and with that you gain a lot flexibility providing your font face supports a given feature. There are too many to list individually, and there are plenty of (articles)[http://help.typekit.com/customer/portal/articles/1789736] that list all the possible features.

###Kerning

`font-kerning`

##Browsers

##IE
https://technet.microsoft.com/en-us/library/dn640697.aspx

```html
<meta http-equiv="X-UA-TextLayoutMetrics" content="gdi" />
```

##The Future - CSS Level 4



###External Links
[OpenType Font Features in CSS](http://help.typekit.com/customer/portal/articles/1789736)
[State of Web Type](http://www.stateofwebtype.com/)
[CSS Fonts 3](https://drafts.csswg.org/css-fonts-3)
[CSS Fonts 4](https://drafts.csswg.org/css-fonts-4)


Image, a CSS version of http://www.better2web.com/djfiles/typography-b2w.jpg