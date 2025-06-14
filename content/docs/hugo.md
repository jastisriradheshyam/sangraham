+++
title = 'Hugo'
date = 2024-12-07T02:39:01+05:30
draft = false
description = 'Information on Hugo'
+++

# Basic Commands

- Simple testing server: `hugo server`
- Create new content: `hugo new content ./content/.../PAGE_NAME.md`

- Highlight code styling: [How to style highlighted code? - support - HUGO](https://discourse.gohugo.io/t/how-to-style-highlighted-code/38487)

# Conditions

## If not equal

```html
{{$linksLen := len .Ancestors.Reverse}}
{{ if not (eq $linksLen 0) }}
...
{{end}}
```