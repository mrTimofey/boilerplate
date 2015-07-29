# Node.js Boilerplate

Frontend Node.js based boilerpalte.

It can be used for fast frontend project development.

Modules involved:
* Request handling: [Express](http://expressjs.com)
* Templating: [Jade](http://jade-lang.com)
* Styles: [Stylus](http://learnboost.github.io/stylus/) with [kouto-swiss](http://kouto-swiss.io)
* Client scripts: [Browserify](http://browserify.org), [Bower](http://bower.io), [Debowerify](https://github.com/eugeneware/debowerify), [Watchify](https://github.com/substack/watchify), [jshint](http://jshint.com)
* Utility: [Livereload](https://github.com/napcs/node-livereload), [Parallelshell](https://github.com/keithamus/parallelshell), [Serve-favicon](https://github.com/expressjs/serve-favicon)

## Installation and configuration

Open console and change current directory to the project than execute

```
npm install
```

Create files "assets/js/main.js" and "assets/styles/main.styl".

Default configuration is stored in "config.deafult.json".
You can create "config.json" file and rewrite any option from default configuration.

Configuration options are:
* appPort - application port
* livereloadPort - port for livereload server

## Starting and CLI

Open console and change current directory to the project than execute

```
npm run start
```

This will run all related tasks and your project will be available at 3000 port by default.
Port 35729 will be used for livereload server by default.

To run jshint execute

```
npm run jshint
```

## Views

All views files must be stored inside "views" directory. Their names will be used in routing.

Example: "/about/career" request will be handled with "views/about/career.jade" view.

If corresponding view file is not found then you will see error page with 404 status.

For the front page create "home.jade" view.

## Assets and static files

Project assets and statics are stored in "assets" directory with obviously named directories inside.

Use *script(src=__js)* and *link(rel="stylesheet" href=__css)* to include compiled scripts and styles within your views.

Use function *static(path)* in your views for static URLs. Path argument must not contain leading slash.

## Views helpers

* range([from], to) - generates an array of numbers from first parameter to second; first parameter can be omitted so it will be equal to 1 by default. Examples:
  * range(3, 5) -> [3, 4, 5]
  * range(5) -> [1, 2, 3, 4, 5]

## Views data

You can pass variables to views using files named same as views but inside "data" directory. Available variables are *module.exports* object properties.

Data files from home to each segment in URI will be merged. If some object property has same name with upper level data object then this property will be rewritten. 

Example: "/about/career" request will be handled with data defined in *module.exports* inside files "home.js", "about.js", "about/career.js" in "data" directory.
If there is a property *title* both in "home.js" and "about.js" then *title* from "about.js" will be availabe in view.

## Livereload

To enable livereload feature just include *script(src=__livereload)* in view.

## Bower components

You can use bower to install client-side dependencies.
To include them in your scripts you can use *require* function provided by browserify.
Debowerify allows you to include bower components by using just *require(<component name>)* without path
(e.g. *require('jquery')*) 

Use "./some-script.js" to include local script files inside "assets/js" directory.
