---
title: Shortcode, Git, Menu, and Hugo Variables
linktitle: Shortcode, Git, and Hugo Variables
description:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
categories: [variables and params]
tags: [shortcodes,git]
draft: false
weight: 50
aliases: [/extras/gitinfo/,/variables/other/]
toc: true
needsreview: true
---

## Shortcode Variables

[Shortcodes][shortcodes] have access to parameters delimited in the shortcode declaration via [`.Get`][getfunction], page- and site-level variables, and also the following shortcode-specific fields:

`.Parent`
: provides access to the parent shortcode context in nested shortcodes. This can be very useful for inheritance of common shortcode parameters from the root.

`.IsNamedParams`
: boolean that returns `true` when the shortcode in question uses [named rather than positional parameters][shortcodes]

`.Inner`
: represents the content between the opening and closing shortcode tags when a [closing shortcode][markdownshortcode] is used

## Git Variables

Hugo provides a way to integrate Git data into your website.

{{% note "`.GitInfo` Performance Considerations"  %}}
Hugo's Git integrations should be fairly performant but *can* increase your build time. This will depend on the size of your Git history.
{{% /note %}}

### `.GitInfo` Prerequisites

1. The Hugo site must be in a Git-enabled directory.
2. The Git executable must be installed and in your system `PATH`.
3. The `.GitInfo` feature must be enabled in your Hugo project by passing `--enableGitInfo` flag on the command line or by setting `enableGitInfo` to `true` in your [site's configuration file][configuration].

### The `.GitInfo` Object

The `GitInfo` object contains the following fields:

`.AbbreviatedHash`
: the abbreviated commit hash (e.g., `866cbcc`)

`.AuthorName`
: the author's name, respecting `.mailmap`

`.AuthorEmail`
: the author's email address, respecting `.mailmap`

`.AuthorDate`
: the author date

`.Hash`
: the commit hash (e.g., `866cbccdab588b9908887ffd3b4f2667e94090c3`)

`.Subject`
: commit message subject (e.g., `tpl: Add custom index function`)

## Hugo Variables

The `.Hugo` variable provides easy access to Hugo-related data and contains the following fields:

`.Hugo.Generator`
: `<meta>`` tag for the version of Hugo that generated the site. `.Hugo.Generator` outputs a *complete* HTML tag; e.g. `<meta name="generator" content="Hugo 0.18" />`

`.Hugo.Version`
: the current version of the Hugo binary you are using e.g. `0.13-DEV`<br>

`.Hugo.CommitHash`
: the git commit hash of the current Hugo binary e.g. `0e8bed9ccffba0df554728b46c5bbf6d78ae5247`

`.Hugo.BuildDate`
: the compile date of the current Hugo binary formatted with RFC 3339 e.g. `2002-10-02T10:00:00-05:00`<br>

{{% note "Use the Hugo Generator Tag" %}}
We highly recommend using `.Hugo.Generator` in your website's `<head>`. `.Hugo.Generator` is included by default in all themes hosted on [themes.gohugo.io](http://themes.gohugo.io). The generator tag allows the Hugo team to track the usage and popularity of Hugo.
{{% /note %}}

## Menu Variables

A menu entry in a [menu template][] has the following properties:

`.URL`
: string

`.Name`
: string

`.Menu`
: string

`.Identifier`
: string

`.Pre`
: template.HTML

`.Post`
: template.HTML

`.Weight`
: int

`.Parent`
: string

`.Children`
: Menu

## Sitemap Variable

A sitemap is a `Page` and therefore has all the [page variables][pagevars] available to use sitemap templates. They also have the following sitemap-specific variables available to them:

`.Sitemap.ChangeFreq`
: the page change frequency

`.Sitemap.Priority`
: the priority of the page

`.Sitemap.Filename`
: the sitemap filename


[configuration]: /getting-started/configuration/
[getfunction]: /functions/get/
[markdownshortcode]: /content-management/shortcodes/#shortcodes-with-markdown
[menu template]: /templates/menu-templates/
[shortcodes]: /templates/shortcode-templates/