# TND Notice.

This module helps add a quick notice on a website. Notice information can be configured solely through the site's configuration file or through a page referenced in the site's configuration file.

## Usage

Simply add `{{ partialCached "tnd-notice/print.html" . "tnd-notice/print" }}` in your template file, `baseof.html` or other.

### Customize markup.

  1. Create homonymous partial files in your project at `/layouts/partials/tnd-notice/print.html`
  2. Follow comments from...

## Configure

### API

There are two ways to set the notice, either through the site config or through a page. Either solution uses the same keys under a reserved group key `tnd_notice`

Available keys are:

__title__: The notice title.
__content__: The notice content or body.
__page__: If the notice should link to a page. This needs to be a string formated for Hugo's `GetPage` function. This is only available through the site configuration.
__read_more__: (default: `true`) If disabled, the _Read more_ link will not be printed, even if a `page` is referenced. 
__disable__: (default `false`) If set to true, the notice won't show.

### Through site configuration

```yaml
tnd_notice:
  title: Something came up
  content: "Sed posuere consectetur est [lobortis](https://google.com). Something else."
  page: /notice.md
```

### Through content file referenced in configuration file

For ease of use, if a page is set, user can add the notice title and and notice content on the page Front Matter itself. They will overwride the module configuration on the site level.

This allows users to switch between various notices without having to delete/rewrite settings.

```yaml
---
title: Important Notice
tnd_notice:
  title: Something came up
  content:  - |
    Sed posuere consectetur est at [lobortis](https://google.com).
    Something else.
---
```

## Not publishing the notice page (since Hugo 0.64.0).

If for some reason user wishes to configure the notice through a content file but would rather not have it published, they should use Hugo settings to make sure given page is not surfaced by Hugo.

```yaml
---
title: Important Notice
tnd_notice:
  title: Something came up
_build:
  render: false
  list: false
---
```

Also, user should disable the `read_more` from either the site configuration file or the content file's Front Matter.