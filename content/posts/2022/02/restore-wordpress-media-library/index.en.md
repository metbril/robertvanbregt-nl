---
title: "Restore WordPress media library"
slug: "restore-wordpress-media-library"
date: 2022-02-16T21:00:00+01:00
author: Robert van Bregt
tags: [meta, plugin, wordpress]
categories:
  - Technologie
draft: true
---
After importing all posts back to an empty WordPress install, I used the [Media Sync plugin](https://wordpress.org/plugins/media-sync/) to easily restore the media library from the files in my uploads folder. I also needed [my SQL script to restore the paths]({{< ref "sql-update-query-wordpress-voor-uploads" >}}), since I decided to install WordPress in a subfolder of the root. So glad I saved that more than 10 years ago.
