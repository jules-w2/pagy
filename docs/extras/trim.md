---
title: Trim
categories:
- Feature
- Extra
---

# Trim Extra

Remove the `page=1` param from the link of the first page.

!!!warning
This extra is needed only for very specific scenarios, for example if you need to avoid frontend cache duplicates of the first
page.
!!!

## Synopsis

```ruby pagy.rb (initializer)
require 'pagy/extras/trim' # it will trim without any further configuration,
```

```ruby Controller (and initializer)
# you can disable it explicitly for specific requests
@pagy, @records = pagy(collection, trim_extra: false)

# or...

# disable it by default (opt-in) in pagy.rb initializer:
Pagy::DEFAULT[:trim_extra] = false   # default true
# in this case you have to enable it explicitly when you want the trimming
@pagy, @records = pagy(collection, trim_extra: true)
```

## Variables

| Variable      | Description                   | Default |
|:--------------|:------------------------------|:--------|
| `:trim_extra` | enable or disable the feature | `true`  |

You can use the `:trim_extra` variable to opt-out of trimming even when the extra is required (trimming by default).

You can set the `Pagy::DEFAULT[:trim_extra]` default to `false` if you want to explicitly pass the `trim_extra: true` variable in
order to trim the page param.

## Methods

The `trim` extra overrides the `pagy_anchor` method in the `Pagy::Frontend` module.

==- `pagy_anchor(pagy)`

This method overrides the `pagy_anchor` using the `pagy_trim` to process the link to the first page.

==- `pagy_trim(pagy, a)`

Sub-method called only by the `pagy_anchor` method, it removes the the `:page_param` param from the first page link (
usually `page=1`).

Override this method if you are [customizing the urls](/docs/how-to.md#customize-the-url).

If you use a `pagy_*nav_js` helper you should customize also the `Pagy.trim` javascript function.

===
