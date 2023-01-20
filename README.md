<p align="center">
  <img src="/assets/images/xcmonkey.png"/>
</p>

<p align="center">
  <a href="https://github.com/alteral/xcmonkey/actions"><img src="https://github.com/alteral/xcmonkey/actions/workflows/test.yml/badge.svg" /></a>
  <a href="https://sonarcloud.io/summary/new_code?id=alteral_xcmonkey"><img src="https://sonarcloud.io/api/project_badges/measure?project=alteral_xcmonkey&metric=coverage" /></a>
  <a href="https://rubygems.org/gems/xcmonkey"><img src="https://img.shields.io/gem/v/xcmonkey.svg?style=flat" /></a>
  <a href="/LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg?style=flat" /></a>
</p>

## Description

*xcmonkey* is a tool for doing stress testing of iOS apps. It's inspired by and has similar goals to [*monkey*](https://developer.android.com/studio/test/monkey) on Android.

Under the hood, *xcmonkey* uses [iOS Development Bridge](https://fbidb.io/) as a driver, that's why it's pretty smart and can do a lot of things, such as taps, swipes and presses. All that comes «pseudo-random» because it has access to the screen hierarchy, and so can either do actions blindly (like tapping on random points) or precisely (like tapping on the existing elements).

## Prerequisites

```bash
brew install facebook/fb/idb-companion
pip3.6 install fb-idb
```

## Installation

```bash
gem install xcmonkey
```

If you prefer to use [*bundler*](https://bundler.io/), add the following line to your `Gemfile`:

```ruby
gem 'xcmonkey'
```

## Usage

### To run a stress test

```bash
xcmonkey test --udid "413EA256-CFFB-4312-94A6-12592BEE4CBA" --bundle-id "com.apple.Maps" --duration 100

12:44:19.343: Device info: {
  "name": "iPhone 14 Pro",
  "udid": "413EA256-CFFB-4312-94A6-12592BEE4CBA",
  "state": "Booted",
  "type": "simulator",
  "os_version": "iOS 16.2",
  "architecture": "x86_64",
  "path": "/tmp/idb/413EA256-CFFB-4312-94A6-12592BEE4CBA_companion.sock",
  "is_local": true,
  "companion": "/tmp/idb/413EA256-CFFB-4312-94A6-12592BEE4CBA_companion.sock"
}

12:44:22.550: App info: {
  "bundle_id": "com.apple.Maps",
  "name": "Maps",
  "install_type": "system",
  "architectures": [
    "x86_64",
    "arm64"
  ],
  "process_state": "Running",
  "debuggable": false,
  "pid": "49186"
}

12:44:23.203: Tap: {
  "x": 53,
  "y": 749
}

12:44:23.511: Swipe (0.5s): {
  "x": 196,
  "y": 426
} => {
  "x": 143,
  "y": 447
}

12:44:24.355: Press (1.2s): {
  "x": 143,
  "y": 323
}
```

### To repeat the stress test from generated session

```bash
xcmonkey repeat --session-path "./xcmonkey-session.json"
```

### To describe the required point

```bash
xcmonkey describe -x 20 -y 625 --udid "413EA256-CFFB-4312-94A6-12592BEE4CBA"
```

## [fastlane](https://github.com/fastlane/fastlane) integration

To run *xcmonkey* from *fastlane*, add the following code to your `Fastfile`:

```ruby
require 'xcmonkey'

lane :test do
  Xcmonkey.new(
    udid: '413EA256-CFFB-4312-94A6-12592BEE4CBA',
    bundle_id: 'com.apple.Maps',
    duration: 100
  ).run
end
```

## Code of Conduct

Help us keep *xcmonkey* open and inclusive. Please read and follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## License

This project is licensed under the terms of the MIT license. See the [LICENSE](LICENSE) file.
