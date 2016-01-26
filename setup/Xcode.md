# Xcode

This guide will show you how to setup Xcode which will allow you to build iOS applications. As of Xcode 7 you can now build directly to iOS devices without having the expensive developer certificates.

## Install the SDK

In order to install Xcode you should sign up for an Apple Developer Account. You can do this [here](https://developer.apple.com/)

There are two ways to download Xcode

* The Mac App store, search for "Xcode" and click install - this may ask for your apple id and password (use your developer account)
* Apple Developer Downloads - requires an apple developer account

## Install Deploy Tools

The following deployment tools will allow you to utilise Xcode's deployment and simulation features from the command line

Run the following commands in your command line terminal

```bash
$ npm install -g ios-sim
$ npm install -g ios-deploy
```
