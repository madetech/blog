# Making Multiple Browserify Bundles with Gulp.

### Introduction

Recently I was writing an npm module, and I wanted to include some examples of how to use the module in the repo. For me, this required having a `gulp watch` function which compiled several different files that all included the same module into several different bundles in several different places. Finding examples of doing this were very rare and/or incomplete online, so I'm writing a full breakdown of what I did for anyone having the same issues that I was.

So, I wanted the structure to look like this.

```
src/
  \_ index.es6
  \_ my_lib.es6
  \_ other_lib_file.es6
  \_ a_third_lib_file.es6
examples/
  \_ basic.es6
  \_ square.es6
  \_ matrices.es6
dist/
  \_ examples/
       \_ basic/
            \_ index.html
            \_ bundle.js
       \_ square/
            \_ index.html
            \_ bundle.js
       \_ matrices/
            \_ index.html
            \_ bundle.js
...
(The lib/ and test/ folders, etc., aren't important here.)
```

Where each of the `.es6` files  in `examples/` will include my module (in `src/`), and be bundled into the corresponding directory in `dist/examples/`. This would mean that my `gulp watch` command would have to watch several different files individually, and compile them to corresponding `bundle.js` files.

I'm going to go through my gulpfile and describe how it works. Please also note at this point that I'm using babelify to convert the es6 to commonJS, but this example should work fine without babelify. Also, as of yet I'm not doing any uglifying.

### The `gulpfile.js`

```
var gulp = require('gulp');
var babel = require('gulp-babel');
var rename = require('gulp-rename')
var sourcemaps = require('gulp-sourcemaps');

var watchify = require('watchify');
var babelify = require('babelify');
var browserify = require('browserify');

var source = require('vinyl-source-stream');
var buffer = require('vinyl-buffer')

var merge = require('utils-merge')
var glob = require('glob')

// Makes the bundle, logs errors, and saves to the destination.
function makeBundle(src, watcher, dst) {

  // This must return a function for watcher.on('update').
  return function() {

    // Logs the compilation.
    console.log('Compiling ' + src + ' -> ' + dst)

    // Bundles the example!, which then:
    return watcher.bundle()

      // Logs errors
      .on('error', function(err){
        console.log(err.message);
        this.emit('end');
      })

      // Uses our new bundle as the source for the sourcemaps.
      .pipe(source(dst))
      .pipe(buffer())

      // Creates the sourcemaps.
      .pipe(sourcemaps.init({ loadMaps: true }))
      .pipe(sourcemaps.write('.'))

      // And writes them to the destination too.
      .pipe(gulp.dest(''))
  }
}

// Watchifies the examples and their local import trees for bundling.
function makeWatcher(src, dst) {
  var args = merge(watchify.args, { entries: [src],
                                    debug: true,
                                    fullPaths: true,
                                    extensions: [".es6", ".js"] });

  // The `watcher` watches, compiles from es6, and browserifies the entries given in `args`.
  var watcher = watchify(browserify(args)).transform(babelify)

  // `bundle` becomes a function that will be called on update.
  var bundle = makeBundle(src, watcher, dst);

  // Listens for updates.
  watcher.on('update', bundle);
  return bundle();
}

// Watches the example files.
gulp.task('watch', function (done) {

  // Find all source files in the `examples/` directory.
  var files = glob.sync('examples/**/*.es6');

  // filesWithWatchers will be an array of simple objects that each contain a
  // filename and a boolean that determines whether the file is currenty being watched.
  var filesWithWatchers = [];

  for (var i = 0; i < files.length; i++) {
    filesWithWatchers.push({ file: files[i], watching: false });
  }
  // Loop over all the files in the directory.
  filesWithWatchers.forEach(function (entry, i, entries) {

    // Don't let this loop finish.
    entries.remaining = entries.remaining || entries.length;

    // Get the destination for this bundle.
    var bundleDest = ('dist/' + entry.file).split('.')[0] + '/bundle.js';

    // Make a watcher unless the entry already has one.
    if (!entry.watching) {
      makeWatcher(entry.file, bundleDest);
      entry.watching = true;
    }
  });

  return;
});
```

### How it works

The `gulp.task('watch'` function is what we call with `gulp watch` on the command line.

For each of the files in `examples/`, we call the `makeWatcher` function which goes away and makes a `watchify`/`browserify`/`babelify` bundler (called `watcher`) for that file.

The `makeBundle` function returns a function which has the `watcher` make the bundle. It also then checks for errors and compiles our sourcemaps.

The `makeWatcher` function saves the function returned by the `makeBundle` function into a variable called `bundle`. This is then passed to the `watcher.on('update'`, so that the example is rebundled whenever a file in the example's import tree is changed. `makeWatcher` then called `bundle()` to make an initial bundle for the example regardless of whether anything has changed.

Hopefully that wasn't too bad! I'm still relatively new to this way of working, so any questions or comments would be much appreciated.