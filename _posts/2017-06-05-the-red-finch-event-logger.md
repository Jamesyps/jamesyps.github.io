---
layout: post
title: The Red Finch Event Logger
date: '2017-06-05 12:15:00'
intro: It's a nice experience to evolve your own software. Lets explore the design decisions behind the rebuild of the Perch Event Log application.
highlight: candy
---

With the recent release of Perch 3 I wanted to take some time to update one of my more popular open source packages to take advantage of the new APIs and UI. 

It also felt a good opportunity to push breaking changes and address some of the architectural shortcomings of [version 1](https://github.com/Jamesyps/Perch-Activity-Log), namely the lack of flexibility in adding new event listeners. The application was originally created in 2015 and was long overdue an update.

Version 1's event listeners were defined in a [single file](https://github.com/Jamesyps/Perch-Activity-Log/blob/master/addons/apps/jw_activity_log/listeners.php) and manually transformed the event data passed through to match the database fields for logging, the result was a series of callback functions that looked like so:

```php
<?php 
$API->on('region.add_item', function (PerchSystemEvent $Event) use ($Actions) {
    $data = array();
    $user = $Event->user->to_array();
    $subject = $Event->subject->to_array();
    $data['actionKey'] = $Event->event;
    $data['userAccountID'] = $user['userID'];
    $data['userAccountData'] = $user;
    $data['resourceType'] = LOG_REGION_TYPE;
    $data['resourceID'] = $subject['regionID'];
    $data['resourceTitle'] = $subject['regionKey'];
    $data['resourceModification'] = $subject['regionHTML'];
    // Save
    $Actions->create($data);
    // Debug
    PerchUtil::debug('Inserting new action log data:');
    PerchUtil::debug($data);
});
```
While simple, any database schema changes would be difficult to accomplish without significant rewrites to these methods. The same was true for any potential breaking changes to the Perch APIs.

There were other issues too. The history view was [hard coded](https://github.com/Jamesyps/Perch-Activity-Log/blob/master/addons/apps/jw_activity_log/modes/view.post.php#L76) using a conditional:

```php
if ((PerchUtil::count($historical_logs) > 1) && ($Action->resourceType() === LOG_REGION_TYPE)) {
```

Not exactly sustainable as the featureset of Perch grew, including the release of [Perch Runway](https://perchrunway.com) which added collections. The history view was also limited to showing paragraph level changes - with large quantities of content and frequent updates the usefuless of this capability would be diminished.

## Event Transformers

[Version 2](https://github.com/RedFinch/Perch-Event-Log) was built to tackle these problems from the start, with a completely clean slate.

The first stage was to build an abstraction layer on top of the core Events system. This would take the raw PHP objects returned by Perch into a standard format that would be saved by the application - these [classes](https://github.com/RedFinch/Perch-Event-Log/tree/master/perch/addons/apps/redfinch_logger/lib/types) were called 'types'.

The `TypeBase` class includes a series of methods that are used to extract information from a `PerchSystemEvent` instance. As Perch is a content management system and its regions are defined by developers it was important to make sure that the type classes did not limit what could be logged - optional methods such as `media()` allow for files to be included (such as those uploaded into the assets system).

The result is a common set of properties that are shared by all types:

```php
[
    'id'      => 0,
    'title'   => null,
    'content' => null,
    'media'   => false
]
```

An abstract method `map()` must be defined by all [child classes](https://github.com/RedFinch/Perch-Event-Log/blob/master/perch/addons/apps/redfinch_logger/lib/types/RedFinchLogger_TypeRegion.php#L17) to extract data into this format.

Types are passed through to the `Dispatcher` class which takes this data and combines with additional system properties to form a [full event log record](https://github.com/RedFinch/Perch-Event-Log/blob/master/perch/addons/apps/redfinch_logger/lib/RedFinchLogger_Dispatcher.php#L88). These include the date and time, the user commiting the change and the event keys.

Event listeners could now be simplified, rather than a long list they were broken up into namespaced files (assets, categories, regions etc).

```php
<?php
foreach(['category.create', 'category.update'] as $eventKey) {
    $API->on($eventKey, function(PerchSystemEvent $Event){
        $Dispatcher = new RedFinchLogger_Dispatcher(
            $Event->event,
            new RedFinchLogger_TypeCategory($Event->subject),
            $Event->user
        );
        $Dispatcher->save();
    });
}
```

This is far more maintainable - new properties can be added without rewrites being needed for all types. Provide a common data structure also allowed for a universal history view rather than the manual assembly in version 1. By breaking the history view down into a method it became possible to paginate the results improving performance and no longer overwhelming content auditors.

## Other Changes

Perch 3 launched with [new APIs](https://docs.grabaperch.com/api/reference/adminlisting/) for creating a consistent and native looking UI within the CMS. Version 2 took advantage of these to produce a clean and simple interface while still providing an insight into the way content is managed by editors.

A simple yet attractive change was to make use of a new property of the `PerchAdminListing` API, which allows for Gravatars to be displayed next user information providing some visual flair to break up the list of events.

![Event logger view](/assets/resources/blog/redfinch-event-log.png)

Moving forward it would be great to add export functionality and notifications for key events or changes. Luckily the codebase is ready to support such extensions and I'm looking forward to continuing to work on the application.

For more information, download links and links to the GitHub repository you can view the [application profile here at the RedFinch homepage](http://redfinch.org/releases/event-logger).
