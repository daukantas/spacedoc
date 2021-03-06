# Usage

## Installation

```bash
npm install spacedoc --save-dev
```

## Setup

Before running the parser, call `Spacedoc.config()` with an object of configuration settings. Refer to the [full API](api.md) to see every option.

```js
const Spacedoc = require('spacedoc');

Spacedoc.config({
  adapters: ['sass', 'js'],
  input: './pages/*.md',
  output: './build',
  template: './template.pug'
});
```

## Initializing

The plugin can be used standalone or with the [Gulp](https://github.com/gulpjs/gulp) build system.

To use the library standalone, call `Spacedoc()` with the option `src` being a glob of files, and `dest` being an output folder.

```js
Spacedoc({
  input: 'docs/*.md',
  output: 'dist'
});
```

The `Spacedoc()` function returns a stream. You can listen to the `finish` event to know when the processing is done.

```js
const stream = Spacedoc({
  input: 'docs/*.md',
  output: 'dist'
});
stream.on('finish', function() {
  // ...
});
```

You can also omit the `src` and `dest` settings when calling `.config()`, and use the same method in the middle of a Gulp stream (or any Node stream that happens to use [Vinyl](https://github.com/gulpjs/vinyl) files). The function takes in a glob of Markdown files, and transforms them into compiled HTML files.

```js
gulp.src('./pages/*.md')
  .pipe(Spacedoc())
  .pipe(gulp.dest('./build'));
```

## Command Line Use

Spacedoc can be installed globally and used from the command line. For now, only the `sass` and `js` adapters can be used.

```
  Usage: Spacedoc [options]

  Options:

    -h, --help               output usage information
    -V, --version            output the version number
    -s, --source <glob>      Glob of files to process
    -t, --template <file>    Pug template to use
    -a, --adapters <items>   Adapters to use
    -d, --dest <folder>      Folder to output HTML to
    -m, --marked <file>      Path to a Marked renderer instance
```

## Next

[Read the full API documentation, which includes all configuration settings.](api.md)
