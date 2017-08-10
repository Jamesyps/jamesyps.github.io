---
layout: post
title: Locking Master Pages in Perch
date: '2017-08-08 20:50:00'
intro: Its built into Runway, but how can you prevent users selecting system master pages in standard Perch?
highlight: emerald

meta:
  description: Its built into Runway, but how can you prevent users selecting system master pages in standard Perch?
---

When building sites using Perch I like to make sure each page is its own master template. This not only makes any future Runway upgrade easier but it feels like a better way of organising pages. Of course if you do not use master templates in this way or have a better solution do let me know!

Typically this involves either moving the system pages (those that are not really reusable, such as a blog archive page) into their own subdirectory and adding a common prefix - usually `core_`. This presents a problem though as clients may select one of these master templates when adding new pages.

A simple solution I have used on a few sites is to add some javascript that prevents regular users from selecting these. Admittedly it is *very* low tech but it has been effective.

First if using Perch 3 you will need to recreate the `addons/plugins/ui` directory. Inside create `_config.inc` file with the following:

```
<?php if (is_object($CurrentUser) && $CurrentUser->logged_in() && !$CurrentUser->roleMasterAdmin()):?>
    <script src="/admin/addons/plugins/ui/hide-core-pages.js"></script>
<?php endif; ?>
```

This injects a Javascript file to all users except the the root user. The content of `hide-core-pages.js` is:

```js
(function($){
    /**
     * String to be hidden
     *
     * @type {string}
     */
    var hidePrefix = 'Core ';

    /**
     * Disables all master page options that have contain the hidePrefix value
     */
    $('#templateID option').filter(function() {
        return $(this).text().indexOf(hidePrefix) > -1;
    }).prop('disabled', true);
})(jQuery);
```

If you use a different prefix (for example `system_`) then you can change the `hidePrefix` variable to the required string.

The end result is that these master templates will be greyed out, helping clients by reducing the risk that they may accidentally create a page not designed for general content.


*This is not really designed for use with Perch Runway as you can natively limit what users can choose to create as a subpage.*