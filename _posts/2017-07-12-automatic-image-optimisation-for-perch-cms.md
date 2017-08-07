---
layout: post
title: Automatic Image Optimisation for Perch CMS
date: '2017-06-05 12:15:00'
intro: Once a site is launched how do you keep it rankly highly for speed? It's not always easy once you're no longer in control of the content.
highlight: amber
---

Once the keys have been handed over to a client it can difficult to ensure that uploaded content is as optimised as possible. As a developer there are a myriad of tools at your disposal to compress images, stylesheets and other static assets but these aren't easy to integrate into a client's workflow.

My own personal opinion is that clients should not be burdened with any additional work on top of managing their content - afterall the job of the developer is to solve problems not add them.

To tackle this problem I created the [Image Optimiser](https://github.com/RedFinch/Perch-Image-Optim) application for Perch. This hooks into the native events API and uses standard open source tools to compress and optimise images at a server level.

This is not too different to an [existing Perch app](https://addons.perchcms.com/addons/kraken) which uses the [Kraken service](https://kraken.io), however the aim of my own app was to keep everything local. The optimisation tools are installed to the server and are executed by PHP using a [brilliant wrapper package](https://github.com/spatie/image-optimizer) by [Spatie](https://spatie.be/en), a software development company based in Belgium.

Just like the Kraken integration, the app requires no changes to end user behaviour. They continue to use the CMS as normal - uploading images and managing their content. Anything they do upload is queued in the background and processed later on a scheduled task.

![Scheduled tasks](/assets/resources/blog/image-optimiser-scheduler.png)

To help with any potential problems, the scheduled task will note any images that did not successfully execute. There is a full output log that can be viewed within Perch to route out any problems that may prevent the image being optimised. The image below shows a warning, noting that 35 GIFs could not be optimised. The cause for this was quickly found and rectified.

The application also makes use of the Permissions API - allowing developers to grant access to running tasks in-browser or accessing a detailed settings panel. Editors may find that they wish to preserve some greater detail in their photos even if this reduces the compression level. The application is entirely flexible to the needs of both developers and content producers.

![Scheduled tasks](/assets/resources/blog/image-optimiser-settings.png)

It is already in place on couple of websites, with an average compression ratio of 50% for JPEG images. The site's content is under heavy development and the optimiser has happily crunched down over 160 images over the last week.

![Scheduled tasks](/assets/resources/blog/image-optimiser-tasks.png)

To find out how to install the application you can view [the documentation and download](http://redfinch.org/releases/image-optimiser) it from the RedFinch profile page.

