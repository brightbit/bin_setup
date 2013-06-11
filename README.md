Bin Setup
=========

By [Brightbit](http://brightbit.com).

Make new developers like you.

**Bin Setup** aims to easily setup your Rails 3.2/4.0 app on a new machine. It also helps reset your app back to a clean state. It will reset redis, memcache and your postgres database.

## Installation

Create a bin/setup (or script/setup) file in your Rails project. From the root of your project run:

```bash
# Rails 4:
echo 'bash -c "$(curl -s https://raw.github.com/brightbit/bin_setup/master/bin/setup)"' > bin/setup

# Rails 3:
echo 'bash -c "$(curl -s https://raw.github.com/brightbit/bin_setup/master/bin/setup)"' > script/setup
```

## Usage

#### Running bin/setup:

```bash
bin/setup
```


Which should look something like this:

```bash
$ bin/setup
Installing libraries...
Flushing Memcache...
Flushing Redis...
Reloading the database...
All done!
10.477s total, 5.11s user, 1.28s system, 61% cpu
$
```

This will run `bundle install` (and install bundler if it doesn't exist) and many other commands to bootstrap your app. Documentation is currently lacking so please [browse the source](https://github.com/brightbit/bin_setup/blob/master/bin/setup) to get an idea of what's going on.

**Note:** If you have any problems tail the log: `tail -f log/setup.log`

**Note:** Since Rails 3 uses a `script` directory instead of `bin`, you will need to run `script/setup` instead of `bin/setup`. You could create a `bin` directory and pretend you're using Rails 4 if you'd like.

#### Installing dependencies:

```bash
WITH_DEP=true bin/setup
```

#### Skip resetting the DB:

```bash
KEEP_DB=true bin/setup
```

## Information
### Conventions

Bin setup assumes you are using:
* Mac OS X (Probably Mountain Lion+) (Debian/Ubuntu pull requests are welcomed)
* [Homebrew](http://mxcl.github.io/homebrew/) for installing packages (e.g. postgres, redis, memcache)
* [Bundler](http://gembundler.com/) with binstubs at vendor/bundle/bin. It installs and runs bundle install (setting your binstubs up for you).
* [Brewdler](https://github.com/andrew/brewdler) - It installs and runs brewdle.
* [Direnv](https://github.com/zimbatm/direnv) - It installs for you. You'll need a .envrc in place pointing to your bundler binstubs (for now).
* [Dotenv](https://github.com/bkeepers/dotenv) - It copies .env.example to .env and compares the two. Alerts devs if they are missing .env vars.
* Heroku - And that you have your apps named the same as the current directory with -staging, -qa and -production on then end (e.g. bin_setup-production). If you don't it should fail silently.

It also assumes you:
* Have more than 512MB of RAM (alluding to the next point)
* Don't mind auto running homebrew's lightweight configs of postgres, memcache and redis
* Have a Gemfile, Brewfile, .env.example and .envrc checked into your repo
* Don't have a .env file checked in
* Have a working db/seeds.rb that will be ran via `rake db:seed`
* You like snickers.

### Todo

* Document .env.example and how to set it up (gitignore, Dotenv)
* Add databases.rake override files (3.2 and 4.0) for resetting the DB while rails is running
* Add a .envrc to the project if one doesn't exist
* Add a .env.example to the project if one doesn't exist
* Make it happy with pow (it already is but I think you have to symlink .powenv to .env)
* Allow for customized Heroku app names

### Bug reports

If you discover any bugs, feel free to create an issue on GitHub. Please add as much information as
possible to help us fixing the possible bug. We also encourage you to help even more by forking and
sending us a pull request.

https://github.com/brightbit/bin_setup/issues

## Maintainers

* Eric Boehs (https://github.com/ericboehs)

## License

MIT License. Copyright 2013 Brightbit. http://brightbit.com

You are not granted rights or licenses to the trademarks of Brightbit.
