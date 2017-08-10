---
layout: post
title: Adding Predefined Links to Perch Redactor
date: '2017-08-10 19:00:00'
intro: Here's a quick guide to adding the Predefined Links plugin into the Perch Redactor editor and populating it with the current page tree.
highlight: emerald

meta:
  description: Here's a quick guide to adding the Predefined Links plugin into the Perch Redactor editor and populating it with the current page tree.
---

On a project recently I found there were a numerous links to internal pages that had to added to through the rich-text Redactor editor. Normally if there are internal page links I would choose the [Pagelist](https://addons.perchcms.com/addons/pagelist) field type but obviously in this case that's not going to cut it.

The solution is to make use of an existing [Redactor plugin](https://imperavi.com/redactor/plugins/definedlinks/) and the custom editor configuration introduced in [Perch 3.0.5](https://grabaperch.com/update/v3-0-5). In this post I'll run through the code you need to get started.

![Redactor links panel](/assets/resources/blog/redactor-links.png)

Firstly the Redactor plugin *Predefined Links*. This lets you pass through JSON data to give users a new dropdown menu when adding or editing links to select predefined values. You should take the `predefinedlinks.js` file and place it in `perch/addons/plugins/editors/redactor-plugins/`.

Once this is in place you should create (unless it is already in place) the `perch/addons/plugins/editors/config.js` and add the following code:

```js
Perch.UserConfig.redactor = function () {

    var get = function (profile, config, field) {
        if (config.plugins.indexOf('definedlinks') === -1) {
            config.plugins.push('definedlinks');
            config.definedLinks = Perch.path + '/addons/plugins/editors/redactor-plugins/page-list.php';
        }

        return config;
    };

    var load = function (cb) {
        if (typeof jQuery.Redactor.prototype.definedlinks == 'undefined') {
            jQuery.getScript(Perch.path + '/addons/plugins/editors/redactor-plugins/definedlinks.js', cb);
        } else {
            cb();
        }
    };

    return {
        'get': get,
        'load': load
    }

}();
```

This code hooks into the Perch core javascript and injects the correct plugins and any supporting files. You can find more information about this here in [the documentation](https://docs.grabaperch.com/api/editors/).

The keen-eyed will have spotted a new file referenced: `/addons/plugins/editors/redactor-plugins/page-list.php`. This file takes the current page tree and exports it into a JSON format. This is very similar to the Pagelist fieldtype only it does not output as a `<select>` menu.

Add the following code to this file:

```php
<?php require __DIR__ . '/../../../../core/inc/api.php';

if (!class_exists('PerchContent_Pages')) {
    include_once(PERCH_CORE . '/apps/content/PerchContent_Pages.class.php');
    include_once(PERCH_CORE . '/apps/content/PerchContent_Page.class.php');
}

$Pages = new PerchContent_Pages();
$pages = $Pages->get_page_tree();

$opts = [];

if (PerchUtil::count($pages)) {
    foreach ($pages as $Item) {
        $depth = $Item->pageDepth() - 1;

        if ($depth < 0) {
            $depth = 0;
        }

        $opts[] = ['name' => str_repeat('-', $depth) . ' ' . $Item->pageNavText(), 'url' => $Item->pagePath()];
    }
}

header('Content-Type: application/json');
echo json_encode($opts);
```

Finally you should make sure that your config allows custom editor configs. If this isn't set then you simply add the following to your Perch config file.

```php
define('PERCH_CUSTOM_EDITOR_CONFIGS', true);
```

If you've found this to be useful or have any suggestions for improvements feel free to get in touch.