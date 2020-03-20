# Buildpack: Erlang

This is a [buildpack](http://doc.scalingo.com/buildpacks) for Erlang apps. It
uses [Rebar](https://github.com/basho/rebar) or
[Rebar3](https://github.com/rebar/rebar3).

Which build tool to use is automatically detected. Rebar is currently the
default.  If either `rebar3` or `rebar.lock` are present, Rebar3 will be used.

### Configure your Scalingo App

```sh
$ scalingo create my-app
```

Nothing else.

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your
application is now sourced from a dotfile called `.preferred_otp_version`. It
needs to be the branch or tag name from the http://github.com/erlang/otp
repository, and further, needs to be one of the versions that precompiled
binaries are available for.

When you fail to specify the version, the version marked with a `*` will be
used. this may vary per stack.

Currently supported OTP versions:

scalingo-14:

* OTP-20.1 *

scalingo-18:

* OTP-22.2.7 *

To select the version for your app:

```sh
$ echo OTP-22.2.7 > .preferred_otp_version
$ git commit -m "Select 22.2.7 as preferred OTP version" -a
```

### Build your Scalingo App

```sh
$ git push scalingo master
```

You may need to write a new commit and push if your code was already up to date.

NOTE: You need to have either an ebin/ directory or rebar.config checked into
Git in order for Heroku to identify this project as an Erlang app it can build.
