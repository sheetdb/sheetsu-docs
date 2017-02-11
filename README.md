# Official [Sheetsu.com](https://sheetsu.com) documentation

Welcome to the official API documentation for Sheetsu.com, Google Spreadsheets as a REST APIs. We're happy you are here!

Feel free to check out the [live documentation page](https://docs.sheetsu.com).

If you'd like to make an edit to any of these pages, please [submit a pull request](https://github.com/sheetsu/docs/pulls). Take a look below, for instructions how to run this page locally. We use [Slate](https://lord.github.io/slate/) to power our docs.

Getting Started
------------------------------

### Prerequisites

You're going to need:

 - **Linux or OS X** — Windows may work, but is unsupported.
 - **Ruby, version 2.2.5 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

1. Fork this repository on Github.
2. Clone *your forked repository* (not our original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/docs.git`
3. `cd docs`
4. Initialize and start Slate. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567. Whoa! That was fast!

Now that Slate is all set up on your machine, you'll probably want to learn more about [editing Slate markdown](https://github.com/lord/slate/wiki/Markdown-Syntax), or [how to publish your docs](https://github.com/lord/slate/wiki/Deploying-Slate).

If you'd prefer to use Docker, instructions are available [in the wiki](https://github.com/lord/slate/wiki/Docker).
