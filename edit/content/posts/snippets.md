---
layout: default
title: "On Sublime Snippets"
permalink: /snippets/
description: easy code automation
category: code
---
Snippets are [Sublime Text](Sublime Text) idea of macros. This article explains how to create and manage your own.

Snippets reside in your computer, so it works offline and are the best way to manage your code collection. Luckily once you learn the basics of it you can take some time to abstract your reusable code and have it at your fingertips, instead of jumping from project to project. It's just, tidy.

As a UI Designer [I use it mostly for SASS and HTML](http://nonlinear.nyc/codecode), but the system is pretty agnostic, so it works fine with any language you throw at it.

## Requirements

In order for it to work, snippets must be:

- one per file
- named with `.sublime-snippet` extension
- inside a `/Packages` folder (per system, below)
- under a certain syntax (also below)

## The Packages Folder

On a Mac, `Packages` folder is under `~/Library/Application\ Support/Sublime\ Text\ 2` (or 3)

On Windows, it's `%APPDATA%/Sublime\ Text\ 2` (or 3) and on Linux, on `~/.config/sublime-text-2` (or 3)

You can add the `.sublime-snippet` file right there, but better to create a folder (call it `snippets` maybe?) and move your creations there. I'll explain why later.

## Syntax

```
<snippet>
  <content>
<![CDATA[
content
]]>
  </content>
  <tabTrigger>trigger</tabTrigger>
  <description>description</description>
</snippet>
```

- `trigger` is what to type to call snippet. It's the only part you should remember, so choose wisely.
- `description` appears when you have more than one snippet using same trigger, to differentiate, so be, well... descriptive.
- `content` is your actual code.

As a convention, I name my files as `trigger-extension`, like `clearfix-SASS.sublime-snippet` or `email-HTML.sublime-snippet` but you can name your `.sublime-snippet` however you want.

## The Content

Anything you paste between `<![CDATA[` and `]]>` becomes the content... Except `$` sign, reserved for variables. So if your language needs it, use `\$` instead.

## Variables

By convention, typing the trigger + tab switches trigger for content, and that's about it.

But you can also assign where cursor lands, too. For that, you just need to add `$` to it.

You can also jump to more than one variable, tab, tab, tab, to customize your code. You need to order it accordingly, with `${1}`, `${2}`, `${3}`...

Lastly, you can also add preset copy to it, with `${1:content}`. I use it for default variables... You can keep it as it is (tab way) or change it (easy since it's preselected.

You can even have more than one variable with same number and Sublime Text will select all at once with its multiple cursor feature.

Sadly it will show content of first variable with same number, disregarding the others.

## Learning

Snippets simplify your coding, but you still need to familiarize yourself with the triggers you have, and where to use it. Take your time to learn it, and document it.

## Organization

So let's assume you were diligent and took the trouble to abstract away all your reusable code under snippets, on a folder of your choice. So what?

Yes, you have it ready on your machine, and you'll grow dependent of it. You should back it up, correct?

If you are versed in git, you can create a respository that points to this folder, so you can clone your snippets into any other machine you land on.

The entire [`lazy-8/exo`](https://github.com/lazy-8/exo) is me and a group of friends eating our dog food, organizing best practices.

Trading snippets with fellow developers (as if building a deck) is also something I'd like to see. I just don't know what to do with dependencies, since some snippets don't work on their own. [I'm open to suggestions](mailto:info@nicholasfrota.com?subject=exo snippet collection).

## Beyond

Snippets only work inside Sublime Text. But what about other text editors? Is there a way to translate it to them?

Forget about text editors: What about a system-wide snippet system... Working on any app? Mac has [Textexpander](https://smilesoftware.com/TextExpander/index.html) and [aText](https://www.trankynam.com/atext/), and iPhones have keyboard shortcuts. But snippets are hard to manage and trade.

## Conclusion

Snippets are an open, scalable, agnostic way to organize your reusable code. [`lazy-8/exo`](https://github.com/lazy-8/exo) made my code so fast (with bootstrap presets, CDN links, SASS mixins), I in fact ditched wireframing and jumped straight in rapid (really rapid) prototyping.

I can't wait to see what other people can do to it... If you create your own snippets or need help, feel free to talk either on [twitter](http://twitter.com/home?status=@nonlinear) or [email](mailto:info@nicholasfrota.com?subject=exo snippet collection).