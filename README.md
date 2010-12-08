# SimpleGeo.framework

This is an Objective-C client library for the SimpleGeo API, suitable for use
in both Mac OS X and iOS applications.

`SimpleGeo.framework` embeds
[ASIHTTPRequest](http://allseeing-i.com/ASIHTTPRequest/), so that will become
available when you introduce this as a dependency.

## Getting Started

In order to run the framework tests, you'll need to install `GHUnit.framework`
into `/Library/Frameworks` (or somewhere similar). Look for the most recent
version of `GHUnit-*.zip` on the [gh-unit](https://github.com/gabriel/gh-unit)
[Downloads page](https://github.com/gabriel/gh-unit/downloads).

You'll also need to install `YAJL.framework`. Same deal, but this time, grab
the latest `YAJL-*.zip` from the
[yajl-objc](https://github.com/gabriel/yajl-objc) [Downloads
page](https://github.com/gabriel/yajl-objc/downloads).

For network tests to succeed, you'll want to clone and start the mock SimpleGeo
server:

    $ git submodule update --init
    $ ruby -rubygems server/server.rb

If it worked, it should say something like:

    == Sinatra/1.1.0 has taken the stage on 4567 for development with backup from Mongrel

If it failed, install the dependencies and try again:

    $ sudo gem install oauth json sinatra

To actually run the tests, choose "Tests" as the *Active Target* (via the
*Project* menu) and click "Build and Run".

## Building

To generate a usable `SimpleGeo.framework` from the command-line:

    $ make

The resulting Framework will be in `build/Release`.

## Docs

To generate docs, make sure you've got `doxygen` installed (`brew install
doxygen`, for example), then:

    $ make docs

If you'd like a handy-dandy Xcode docset:

    $ cd docs/html/
    $ make

You can either run `make install` in `docs/html/` to install the docset into
your home directory, or you can do whatever you wish with the
`SimpleGeo.docset` that was created there.

## Embedding `SimpleGeo.framework` in a Cocoa Application

In order to embed `SimpleGeo.framework` into a Cocoa application, you'll have
to add [`YAJL.framework`](https://github.com/gabriel/yajl-objc/downloads) to
your project and follow Apple's instructions for [Embedding a Private Framework
in Your Application
Bundle](http://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPFrameworks/Tasks/CreatingFrameworks.html#//apple_ref/doc/uid/20002258-106880).

The build directory for `SimpleGeo.framework` has been configured as
`../SimpleGeo-build` to facilitate linking it into your application. You can
also copy it wholesale into your project that it's copied into "frameworks" as
part of your application target.

[SimpleApp](https://github.com/simplegeo/SimpleApp) is an example of a Cocoa
application built using this framework.
