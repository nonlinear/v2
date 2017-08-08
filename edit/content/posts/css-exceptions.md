---
title:       CSS Browser Debugging
description: best JS libraries for proper browser debugging
slug:        css-browser-debugging
template:    post.hbs
date:        2015-01-23
author:      nicholas
---
Sometimes you need CSS rules only for a certain browser or operating system to save the day. In this article, I explain a foolproof way to add exception rules precisely, without affecting _other_ browsers or systems.

## Step 1: Modernizr

[Modernizr](http://modernizr.com) scans browser capabilities and reports its findings as classes on `html` tag.

For instance, a page using modernizr on a touchscreen browser (cellphone, tablet) reveals `touch` class on `html`. The same page, on desktops and notebooks reveals `no-touch` class instead.

You can install it with CDN, with `<script src="https://cdnjs.cloudflare.com/ajax/libs/modernizr/2.8.3/modernizr.js"></script>` or [download and install](http://modernizr.com) a local version.

## Step 2: Detectizr

[Detectizr](https://github.com/barisaydinoglu/Detectizr) expands modernizr detection, by revealing browser operating system (`mac`, `android`, `ios`, `windows`, `linux`, etc) browser type (`safari`, `chrome`, `firefox`, `ie`, etc) and even specific versions.

Install it with CDN with `<script src="https://raw.githubusercontent.com/barisaydinoglu/Detectizr/master/dist/detectizr.js"></script>` or [download and install](https://github.com/barisaydinoglu/Detectizr) local version.

since detectizr depends on modernizr, it should go _after_ modernizr script.

## Step 3: Write your CSS exceptions

Your page is now using javascript for what it does best:

- detection
- right on top of your DOM
- affecting _anything_ below it

You know where we're heading, correct? You can now style CSS exceptions freely. For instance,

```
.foo {
  background-color: red;
}
html.safari .foo {
  background-color: blue;
}
```

renders any object with `foo` class as red except if browser is safari, rendering blue instead.

You can use any of the classes above to differentiate.

## Automation: _Only_ and _Unless_ Mixins

We can make the code better, correct? If you use SASS 3.1+, use these mixins

```
@mixin only($only) {
  html.#{$only} & {
    @content;
  }
}
@mixin unless($unless) {
  html:not(.#{$unless}) & {
    @content;
  }
}
```

so you can write exceptions inside the objects, way easier to read:

```
.foo {
  background-color: red;
  @include only(safari) {
    background-color: blue;
  }
}
```

You can do the inverse by writing rules for all browsers _except_ the one listed with `unless`. For instance,

```
.foo {
  @include unless(safari) {
    display: none;
  }
}
```

hides objects with class `foo`, _unless_ browser is safari.

## Bonus Phase: Visibility

Why stop there? We can add visibility rules and show or hide objects at will.

```
html:not(.mac) .visible-mac,
html.mac .hidden-mac,
html:not(.windows) .visible-windows,
html.windows .hidden-windows,
html:not(.linux) .visible-linux,
html.linux .hidden-linux,
html:not(.ios) .visible-ios,
html.ios .hidden-ios,
html:not(.android) .visible-android,
html.android .hidden-android,
html:not(.firefox) .visible-firefox,
html.firefox .hidden-firefox,
html:not(.chrome) .visible-chrome,
html.chrome .hidden-chrome,
html:not(.ie) .visible-ie,
html.ie .hidden-ie,
html:not(.safari) .visible-safari,
html.safari .hidden-safari,
html:not(.touch) .visible-touch,
html.touch .hidden-touch {
  display: none !important;
}
```

Now you can use class `visible-` or `hidden-` for any system or browser above.

* * *

## Conclusion and More

There you have it, powerful and readable exception rules for your CSS. It saved my skin more than once at work.

This and other CSS lifesavers are in [codecode](http://nonlinear.nyc/codecode), a collection of macros to simplify coding.

If you use Sublime Text [make sure to install it](http://nonlinear.nyc/codecode), so you have it always at your fingertips.