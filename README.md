Heroku buildpack: Heroku Toolbelt
=========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that
allows one to run Heroku Toolbelt in a dyno alongside application code.
It is meant to be used in conjunction with at least the
[minimal ruby](https://github.com/dpiddy/heroku-buildpack-ruby-minimal) as well
as other buildpacks as part of a
[multi-buildpack](https://github.com/ddollar/heroku-buildpack-multi).


Usage
-----

Example usage:

    $ ls -a
    .buildpacks  Gemfile  Gemfile.lock  Procfile  config/  config.ru

    $ heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git

    $ heroku config:add HEROKU_TOOLBELT_API_EMAIL=my-fake-email@gmail.com

    $ heroku config:add HEROKU_TOOLBELT_API_PASSWORD=`heroku auth:token`

    $ cat .buildpacks
    https://github.com/heroku/heroku-buildpack-toolbelt.git
    https://github.com/heroku/heroku-buildpack-ruby.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Multipack app detected
    =====> Downloading Buildpack: https://github.com/gregburek/heroku-buildpack-toolbelt
    =====> Detected Framework: heroku-toolbelt
    -----> Fetching and vendoring Heroku Toolbelt into slug
    -----> Moving the netrc generation script into app/.profile.d
    -----> heroku toolbelt installation done
    =====> Downloading Buildpack: https://github.com/heroku/heroku-buildpack-ruby.git
    =====> Detected Framework: Ruby/Rack
    -----> Using Ruby version: ruby-1.9.3
    -----> Installing dependencies using Bundler version 1.3.2
    ...

    $ heroku run 'vendor/heroku-toolbelt/bin/heroku auth:token'
    Running `vendor/heroku-toolbelt/bin/heroku auth:token` attached to terminal... up, run.3706
    abcdef0123456789abcdef0123456789abcdef01


Notes
------

Some PATH manipulation may be needed, expecially if you are using the
heroku-buildpack-ruby-minimal solely to provide a ruby execution environment
for the heroku cli gem. 

