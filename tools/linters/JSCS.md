# JSCS - JavaScript Code Style

> JSCS — JavaScript Code Style is a code style linter which checks your code against your chosen preset coding standard. See [mdevils/node-jscs](https://github.com/mdevils/node-jscs) for more informations about JSCS.

We recommend that you use this with Atom however it is available on a range of other tools.


The following installation and setup is for Atom and the Airbnb ES5 coding standards.

## Installation

* `$ apm install linter-jscs`

## Setup
* In Atom open up the Settings/Preferences and find the linter-Jscs package
* In the linter-Jscs package settings ensure the 'preset' is set to airbnb

At this point your linter will be setup however it will be using the Airbnb ES6 coding standards, therefore we need to tweak the setup a little bit.

* In your Atom Settings/Preferences there will be a 'Open Config Folder'
* Go to Atom > Packages > linter-jscs > .jscsrc
* Remove requireTrailingComma and replace with disallowTrailingComma as shown below.

```json
{
    "preset": "airbnb",
    "esnext": true,

    "disallowTrailingComma": true
}
```

Ensure you save this file.

* In the Config folder go to Atom > Packages > linter-jscs > node_modules > jscs > presets > airbnb.json

* Find and replace
```json
"requireTrailingComma": { "ignoreSingleLine": true },
```
with
```json
"disallowTrailingComma": true,
```

Ensure you save this file, exit Atom and re-open and your linter should be working.


See https://github.com/AtomLinter/linter-jscs for more details
