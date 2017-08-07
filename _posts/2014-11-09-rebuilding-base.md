---
layout: post
title: Rebuilding BASE
date: '2014-11-09 12:17:17'
intro: A quick update explaining how we continuously update our SASS workflow in the studio and why OOCSS is truly the way forward for websites in 2014 and beyond.
highlight: emerald
---

BASE is what every new website at the studio where I work is built upon.

It's difficult to define what BASE is. To call it a framework is an overstatement of its purpose while to call it a template is too limiting for what it lets us achieve. It floats somewhere in the middle giving us a great deal of flexibility while ensuring both of us as developers keep to a consistent set of conventions.

The idea being to standardise the code behind the design, not the design itself. While large frameworks such as Bootstrap have proved very popular and customisable, without serious modification their [roots are always apparent](http://notes.gross.is/post/43508972396/please-stop-using-twitter-bootstrap).

### Thinking Small

In its early days it was nothing more than a set of sass mixins, a reset and a directory structure that we could simply copy across, add to CodeKit and begin writing. There was little if any attempt at making the CSS Object Orientated or modular in any form. 

Despite this, it worked fairly well across our projects over the months it was in use. For small to medium sized websites it presented very few obstacles in updating or debugging while giving us considerably more firepower, thanks to SASS, to get the job done.

The larger a project got, however, the sooner the short-comings in a single large SCSS file became apparent. We had only migrated our styling language, but not our build process and as such we still had monster stylesheets that required searching, scrolling and at times flailing about trying to identify which of the hundreds of selectors was causing a particular issue.

Step one was complete, we had a shared foundation. Step two now had address the problems we had now standardised together.

### Happy Medium
The brief for BASE 3 was simple:

> It should be just too large for small websites, while being just too simple for large ones.

The road to Object Orientated was clear in front of us as the only real solution to this conundrum. But which to choose? From the top of my head there is SMACSS, CSS For Grown Ups and many more all promising a different way of making your stylesheets as organised as can be.

We found during testing however that either through our lack of understanding, or time constraints, that these did not suit how we as an organisation worked. For the more illustrative websites they were incredibly constricting, while simpler ones felt crushed by rules and conventions. Instead we took a mixture of all of them and created our own system:

```
├── css
│   └── scss
│       ├── _includes.scss
│       ├── base
│       │   ├── _base.scss
│       │   ├── _mixins.scss
│       │   └── _placeholders.scss
│       ├── components
│       │   ├── _document.scss
│       │   ├── _footer.scss
│       │   ├── _header.scss
│       │   └── document
│       │       ├── _base.scss
│       │       ├── _colourscheme.scss
│       │       ├── _structure.scss
│       │       ├── _typography.scss
│       │       └── _utility.scss
│       ├── main-ie.scss
│       ├── main.scss
│       ├── modules
│       │   ├── _buttons.scss
│       │   ├── _headings.scss
│       │   ├── _images.scss
│       │   └── images
│       │       ├── _base.scss
│       │       ├── _mobile.scss
│       │       ├── _retina.scss
│       │       └── _tablet.scss
│       └── vendor
│           └── _normalize.scss
```
    
Breaking this tree diagram down, the main sections are:

**Base** -
The configuration and main library files. Here a standard set of variables controls the basic blocks of the website design, including colour palettes, widths and the directories for images and fonts.

For the first time we included a library of mixins in one place, taking the leap from a directory structure to a micro-framework. Some from articles online, others written internally to address individual problems as they arose.

**Components** - 
These are the globally available, but not repeatable sections of CSS for a webpage. The document settings including fonts, typography and the grid are defined here alongside other regions such as the site header, navigation and footers.

**Modules** - 
The smallest elements. Buttons, Images and other low-level parts were written in individual files.

**Vendor** -
Third party libraries were placed here, including most often Gridset.

As well as just SCSS, BASE 3 included the latest social media meta-data for Open Graph, Twitter, Windows 8 and iOS / Android devices as well as some extra libraries via Composer for generating sitemaps.

BASE 3 has been the most widely used, with the majority of the new 2014 websites built upon it. During this time it has had very minor evolutions, including breaking out the `_document.scss` into sub-components and organising the images directory.

Throughout this period it proved flexible and reliable, however recently we have won increasingly larger jobs stretching that initial brief of "just too small" further and further beyond what it was meant to be.

### Go Big or Go Home
BASE 4 follows a very different set of rules to BASE 3. While not an extensive re-write, the core structure of 3 being perfectly fine with some exceptions. In BASE 4 *everything* is a module.

There are two reasons for that. The first being that there are increasing number of articles about how to structure modular HTML and CSS. The idea being that they no longer sit in their page context, but become their own context.

One example given is a news listing page. Designs often implement a second 'read these articles' listing at the bottom of a post. The argument being that the listing section is designed for this purpose, why can we not simply drop it in?

As sites get larger this way of thinking becomes a necessity. Hundreds of pages, some with minor variations cannot be considered individual entities sharing only fonts, colours, headers and footers but each element must be able to sit in as many places as possible. Fortunately, a library recently surfaced that provided that in a structured way: [http://www.csstyle.io](http://www.csstyle.io).

CSSTYLE in many ways forces you to consider each element individually. It becomes *more* difficult to attempt to interlink them than to not and while there is a slight cost to this in repeated code, the benefit is in isolated and easily recognisable code both front-end and in the stylesheets. So long as you are comfortable reading pure SCSS rather than traditional CSS.

The second being the increasing use of living styleguides to showcase these elements. [Github's](https://github.com/styleguide) is one of the better known ones giving a great deal of insight into each module on its own.

Initially this idea seemed only useful for one of our collaborative jobs with an outside developer, but once I had began testing it on a smaller project combined with CSSTYLE it became a self-documenting dream. Not only was the starting goal of BASE realised, but we could now write consistent documentation using a [specification](https://github.com/kneath/kss/blob/master/SPEC.md).

As such it was rolled into BASE 4, with all the mixins, placeholders and other starting elements fully documented using the KSS specification - the result for any new project is an instant overview of what is possible:

### Closing Thoughts
Building BASE has been a version-controlled example of the learning process that started when I was first hired. In the Web Development industry you have to at many points in your career it seems drop what you know and move forward in a very short amount of time.

OOCSS is very much the way any website should be built today. In 2015 if you are not employing some sort of build process, be it a full Grunt stack or a simple app such as CodeKit or Hammer then you are at risk of being left behind. Even now these ways of organising code have been around for years.

But one closing word of advice - find the one that works for you. Do not blindly follow the most popular or most talked about. Some fit better than others, just like all tools and no one framework is ever the complete solution. The most important step is identifying where your problems are and which can address those best, and knowing when these solutions are at their limit.