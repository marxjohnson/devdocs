---
title: Moodle 5.0 developer update
tags:
- Core development
- Moodle 5.0
---

<!-- markdownlint-disable no-inline-html -->

This page highlights the important changes that are coming in Moodle 5.0 for developers.

## Subplugins

<Since version="5.0" issueNumber="MDL-83705" />

The `subplugins.json` file now requires a new `subplugintypes` object to define the subplugins available within a plugin.

The format of this is identical to the existing `plugintypes` object, but the value should be a path which is relative to the plugin's root directory.

:::tip Example of the new `subplugintypes` values

The Quiz Activity located in `mod/quiz` defines the `quizaccess` subplugin type.

The legacy `plugintype` entry for this is as follows:

```json title="mod/quiz/db/subplugins.json demonstrating the legacy plugintypes object"
{
    "plugintypes": {
        "quizaccess": "mod/quiz/accessrule"
    }
}
```

The new `subplugintypes` value is relative to the plugin root as follows:

```json title="mod/quiz/db/subplugins.json demonstrating the new subplugintypes object"
{
    "subplugintypes": {
        "quizaccess": "accessrule"
    }
}
```

Both of these values may be combined for plugins supporting both Moodle 4.5 and earlier, and Moodle 5.0 onwards.

```json title="mod/quiz/db/subplugins.json demonstrating both the legacy plugintypes and the new subplugintypes values"
{
    "plugintypes": {
        "quizaccess": "mod/quiz/accessrule"
    },
    "subplugintypes": {
        "quizaccess": "accessrule"
    }
}
```

:::

## Themes

<Since version="5.0" issueNumber="MDL-83725" />

Themes can now customize activity icon colors using simple CSS variables. The new variables introduced are:

- `$activity-icon-administration-bg`
- `$activity-icon-assessment-bg`
- `$activity-icon-collaboration-bg`
- `$activity-icon-communication-bg`
- `$activity-icon-content-bg`
- `$activity-icon-interactivecontent-bg`

All previous `$activity-icon-*-filter` elements can be removed, as they are no longer in use.

:::tip Example of customizing activity icon colors

Themes can customize the activity icon colors by overriding the following variables before loading the Boost scss:

```scss
$activity-icon-administration-bg: #5915b1;
$activity-icon-assessment-bg: #17857f;
$activity-icon-collaboration-bg: #cf7a34;
$activity-icon-communication-bg: #c70827;
$activity-icon-content-bg: #5915b1;
$activity-icon-interactivecontent-bg: #c70827;
```

:::
