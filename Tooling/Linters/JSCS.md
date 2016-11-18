# JSCS: JavaScript Code Style

*Note - this guide is written for [Atom Text editor]((https://atom.io/))*

- Website: http://jscs.info/
- GitHub repo: https://github.com/jscs-dev/node-jscs
- Atom package: https://atom.io/packages/linter-jscs

## Contents

- [Introduction](#introduction)
- [Atom Installation](#atom-installation)
  - [ES5 Specific](#es5-specific)

## Introduction

JSCS is a code style linter that checks your code against your chosen preset coding standard. The following installation and setup is for Atom and the Airbnb ES5 coding standards.

## Installation

`apm install linter-jscs`

## Atom Setup

- Open/restart Atom.
- Open the *Settings/Preferences* tab (OS X shortcut: `Cmd` + `,`).
- Navigate to *Packages* and find the `linter-jscs` package.
- In the `linter-jscs` package settings ensure the *Preset* dropdown is set to `airbnb`.

### ES5 Specific

At this point your linter will be setup to use the
[Airbnb ES6 coding standards](https://github.com/airbnb/javascript). If you are working with the
[ES5 standards](https://github.com/airbnb/javascript/tree/es5-deprecated/es5) the setup needs tweaking a
little bit:

- Click the *Open Config Folder* button in Atom *Settings/Preferences*.
- Using the *Tree View* (OSX shortcut: `Cmd` + `\`) browse to `packages/linter-jscs/.jscsrc`.
- Remove the `requireTrailingComma` JSON key if present and add `disallowTrailingComma` as shown
below:

```json
{
    "preset": "airbnb",
    "esnext": true,
    "disallowTrailingComma": true
}
```

- Ensure you save this file.
- Browse to `packages/linter-jscs/node_modules/jscs/presets/airbnb.json`.
- Remove the `requireTrailingComma` JSON key and add `disallowTrailingComma` as shown below:

```json
"disallowTrailingComma": true,
```

- Ensure you save this file.
- Exit Atom and re-open and your linter should be working.
