Presentation is in index.html.

It can be viewed on the web on the [github pages branch](http://tednaleid.github.io/intro-to-elixir/).

To recompile it you'll have to have ruby and sass installed as well as node

first:

    npm install

then, if you don't have ruby/sass, install rvm, then `rvm use ruby-2.2.1` (or greater) and `gem install sass`

Then you should be able to run the vanilla grunt task to get things to compile:

    grunt

To watch/auto-recompile, start the watch task:

    grunt watch

The presentation is in `index.html` you don't need to connect to any port or anything on localhost
