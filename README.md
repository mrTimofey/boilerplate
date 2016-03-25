# Frontizer

Node.js based tool for effective frontend development.

Includes stylus, browserify, es6, jade for now. Fututre builds will allow you to choose your own build stack.

## Usage

First install this module:

```
npm i -g frontizer
```

Create a folder for your new project and enter it.

Initialize your new project with `frontizer init` than run it with `frontizer start`.

Just type `frontizer` to see all available commands and their arguments.

## Assets

Assets folder contains all statics and source files for your project. Main files are used as a starting points
for compiling, browserifying and publishing. Published files are placed inside *assets/compiled* directory.

### Client JavaScript and ECMAScript 6

Either ordinary JavaScript or ECMAScript 6 can be used simultaneously.
All files with *.es6* extension will be precompiled by Babel.

## Views

Views folder contains your templates. Each file here represents it's own route which is the same as a file name.
The one exception is *home.jade* which represents a home page.

View based routing examples:

* home.js - /
* foo/bar.jade - /foo/bar
* foo/home.jade - /foo

### Predefined variables

* *__css* contains ready to use <link> tags with compiled css links
* *__js* same for JavaScript
* *__livereload* contains link to a JavaScript file necessary for livereloading

### Helper functions

* range([from], to) - generates an array of numbers from first parameter to second; first parameter can be omitted so it will be equal to 1 by default. Examples:
  * range(3, 5) -> [3, 4, 5]
  * range(5) -> [1, 2, 3, 4, 5]
* static('file-name') - prepends static assets root to the file name
  * static('example.jpg') -> '/assets/static/example.jpg'
* linkTo('view-name') - returns a proper link to the view (there are different for static build and application)
  * linkTo('home') -> '/', static builds: 'home.html'
  * linkTo('my/page') -> '/my/page', static builds: 'my.page.html'

## Data

You can provide any data to your views by creating data files. They will be fetched in the same way as view.
*exports* object fields will be variables in views.

Data shared with corresponding view also includes data from upper levels home files.
For example, route /foo/bar will uses *views/foo/bar.jade* view and tries to fetch and merge files:

1. data/home.js
2. data/foo.js
3. data/foo/bar.js

Obviously, *data/home.js* file will be fetched on every route so you can use it to provide global data and defaults.

Any duplicated data field names will be overwritten by lower level data.

## NPM modules

* Request handling: [Express](http://expressjs.com)
* Templating: [Jade](http://jade-lang.com)
* Styles: [Stylus](http://learnboost.github.io/stylus/) with [kouto-swiss](http://kouto-swiss.io)
* Client JavaScript:
	[Browserify](http://browserify.org),
	[Watchify](https://github.com/substack/watchify),
	[Babelify](https://github.com/babel/babelify) with
	[ES2015 preset](https://github.com/babel/babel/tree/master/packages/babel-preset-es2015)
* Utility:
	[Livereload](https://github.com/napcs/node-livereload),
	[Serve-favicon](https://github.com/expressjs/serve-favicon),
	[jstransformer-stylus](https://github.com/jstransformers/jstransformer-stylus),
	[ncp](https://github.com/AvianFlu/ncp)