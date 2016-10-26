# Contributing to docs

## Contents

- [Introduction](#introduction)
- [Submitting a Pull Request](#submitting-a-pull-request)
- [Languages](#languages)
  - [Link Format](#link-format)
  - [Emoji Tagging](#emoji-tagging)
  - [Page Sections](#page-sections)
  - [Page Template](#page-template)
- [Other Types of Content](#other-types-of-content)

## Introduction

Thanks for taking an interest in contributing to *docs*! This page will tell you everything you need
to know about how to contribute your own commits to the project, as well as the format we use to
keep things looking slick. :lipstick:

It's probably a good idea to have a read through all of the sections here before getting started;
if nothing else please make it your mission to read about how we'd like you to go about
[submitting a pull request](#submitting-a-pull-request).

## Submitting a pull request

When writing your own additions, you may fork this repo, or it's okay to create and push a branch
to this repo directly. Stale branches may eventually be pruned, but otherwise you're okay.

Once ready, create a new pull request. At least one [digiteels](https://github.com/digiteels)
administrator must review your PR before it can be merged into `master`. If it's good we'll get it
merged! :shipit:

We squash all pull requests so don't worry too much about your individual commits.

## Languages

The *Languages* section contains Markdown files on individual languages and their frameworks. It's
the bread and butter of *docs* and so, most of this page is dedicated to how we like these pages to
be structured. This format is also applied to other things like [Git](Tools/Git/md).

### Link Format

Sharing is best when we try to give as much credit to the authors and content creators who make this
repo possible. As a result every link you add should be in the following format:

- [JavaScript Promises: There and back again](http://www.html5rocks.com/en/tutorials/es6/promises/) by [Jake Archibald](https://twitter.com/jaffathecake) via [HTML 5 Rocks](http://www.html5rocks.com/)

The following should be true of each link:

- The title links to the article/content.
- The title is taken *without modification* from the page or webpage title.
- Authors are credited using *by*.
  - Real name preferred.
  - Link to whatever seems like the best place to check out the author. This could be their profile
    on the website, their personal website, GitHub account or Twitter.
  - Where no author is listed, use the website or company hosting the content.
- If multiple content creators contribute on this website, also credit the website itself using
  *via*.

Links can always be tidied up later so just try your best not to editorialise, and give credit.
:thumbsup:

### Emoji Tagging

Noticed the [GitHub compatible emojis](http://www.webpagefx.com/tools/emoji-cheat-sheet/) on the end
of the example link above? They convey special meaning! Add as many of the emojis
[listed in the `README`](README.md#emojis) as are applicable, and try and keep them in the order
shown in the table for consistency. :sparkles:

### Page Sections

Each subheading on each page is a broad category of content. Try your best to put your link under
the most appropriate *single* section. Avoid adding your link to multiple Markdown files unless
multiple languages or frameworks are covered equally.

### Page Template

If you're contributing something and need to add an entire new page of links to the *Languages*
section, we've got a template to get you started.

When you apply your template, make sure it goes in the right place!

- New languages:
  - Create a folder under `Languages` for your new language.
  - Your new Markdown file should be called `README.md` and placed in here.
  - Make sure to add a link to it to the top-level `README.md` *Contents* section!
- New frameworks:
  - Your new Markdown file should be named after the framework, e.g. `React.md`.
  - Place it in the folder for the language it belongs to.
  - Make sure to add a link to it to the top-level `README.md` *Contents* section!
  - Make sure to add a link to it in your language's `README.md`!

Now that you've been briefed, you can find the template [here](template.md). :eyes:

## Other Types of Content

Outside of *Languages* are occasional guides that we've written ourselves. If you've got something
you'd like to write about or create a tutorial/guide for, that's great! It's probably best to open
an issue or placeholder pull request before starting to give us a heads up. :smile:
