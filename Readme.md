
# component

  Component package manager.

## Installation

     $ npm install -g component

## Installing packages

  To install one or more packages, simply pass their github
  repo names as arguments to `component install`. Dependencies
  are resolved and the component contents are downloaded into
  `./components` by default. View `component help install` for details.

```
$ component install component/tip
  
   install : component/tip@master
       dep : component/emitter@master
   install : component/emitter@master
       dep : component/jquery@master
   install : component/jquery@master
     fetch : component/tip:index.js
     fetch : component/tip:tip.css
     fetch : component/tip:tip.html
     fetch : component/emitter:index.js
     fetch : component/jquery:index.js
  complete : component/emitter
  complete : component/jquery
  complete : component/tip
```

## Usage

 Via `--help`:

```

Usage: component <command> [options]

Options:

  -h, --help     output usage information
  -V, --version  output the version number

Commands:

  install <name ...>      install one or more components
  create <dir>            create a component skeleton
  search [query]          search with the given query
  convert <file ...>      convert html files to js modules
  register <user>/<proj>  register a component so others can find it
  info <name> [prop]      output json component information
  changes <name>          output changelog contents
  docs <name>             output readme contents
  open <name>             open component github repo
  build                   build the component
  ls                      list installed components

```

## Features

  - no registry publishing or account required, uses github repositories
  - fast (~2x faster than uncached npm at the time of comparison)
  - extensible sub-commands via `component-YOURCOMMAND` git-style
  - component skeleton creation command
  - installs dependencies from the command-line or ./component.json
  - avoid name squatting through github's naming conventions
  - build your components with `--standalone` to share them with non-component(1) users
  - write components that include their own styles, images, scripts, or any combo
  - write commonjs style scripts

## Using Github as a registry

  By using GitHub as the registry, `component(1)` is automatically
  available to you without further explicit knowledge or work
  creating a registry account etc.

  A nice side-effect of this namespaced world is that dependencies
  are explicit and self-documenting. No longer do you need to query
  the registry for a "repo" property that may not exist, it's simply
  built in to the package name, for example ["visionmedia/page.js"](https://github.com/visionmedia/page.js) rather
  than the unclear "page".

  Another benefit of this is that there are zero name collisions, for example
  you may use "component/tip" for a dependency of "foo", and "someuser/tip"
  as a dependency of "bar", providing `require('tip')` in each. This prevents
  obscure or irrelevant naming such as "progress", "progress2", "progress-bar",
  "progress-component" found in npm.

## Creating a component

  The `component-create(1)` command can create a component
  project skeleton for you by filling out the prompts. Once
  this repo is published to Github, you're all done!

```
name: popover
description: Popover UI component 
does this component have js? yes
does this component have css? yes
does this component have html? yes

     create : popover
     create : popover/index.js
     create : popover/template.html
     create : popover/popover.css
     create : popover/Makefile
     create : popover/Readme.md
     create : popover/.gitignore
     create : popover/component.json

```

  A `Makefile` is created for you in order to create a build of the component,
  complete with installed dependencies simply execute `make`.

## Templates

  Because `component(1)` has no notion of a "template", even simple HTML files
  should be converted to a `require()`-able module. It is recommended that public
  components shared within the community use regular HTML templates, and regular
  CSS stylesheets to maximize contributions, however if you wish to use alternate
  technologies just make sure to compile them before publishing them to Github.

  For the recommended use-case of regular HTML, the `component-convert(1)` command
  will translate a regular HTML file to its `require()`-able JavaScript counterpart.

## Developing component(1) sub-commands

  `component(1)` and sub-commands are structured much like `git(1)`,
  in that sub-commands are simply separate executables. For example
  `$ component info pkg` and `$ component-info pkg` are equivalent.

  Because of this you'll likely want `PATH="./bin:$PATH"` in your
  profile or session while developing component, otherwise `./bin/component`
  will have a hard time finding the sub-commands.

## Running tests

Make sure dependencies are installed:

```
$ npm install
```

Then run:

```
$ make test
```

## Shout-outs

  The concept of components themselves are nothing new, Drupal
  for example has been doing this for years, however it seemed the concept was never
  really translated to the client. My hope is that other communities will re-implement this
  simple tool in their language of choice so that we can all consume components
  easily.

## Screencasts

 - [App integration introduction](https://vimeo.com/48054442)

## Links

 - [Mailing List](https://groups.google.com/group/componentjs)
 - component ["spec"](https://github.com/component/spec/wiki)
 - join `#components` on freenode
 - [List](https://github.com/component/component/wiki/Components) of components
 - [F.A.Q](https://github.com/component/component/wiki/F.A.Q)

## License 

(The MIT License)

Copyright (c) 2012 TJ Holowaychuk &lt;tj@vision-media.ca&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.