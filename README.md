# [gulp](https://github.com/wearefractal/gulp)-inline-css [![Build Status](https://travis-ci.org/jonkemp/gulp-inline-css.svg?branch=master)](https://travis-ci.org/jonkemp/gulp-inline-css)

> Inline your CSS properties into the `style` attribute in an html file. Useful for emails.

Inspired by the grunt plugin [grunt-inline-css](https://github.com/jgallen23/grunt-inline-css). Uses the [inline-css](https://github.com/jonkemp/inline-css) module.

## What's new in 3.0?

- Uses Promises with [inline-css](https://github.com/jonkemp/inline-css) version 2.0

## How It Works

This gulp plugin takes an html file and inlines the CSS properties into the style attribute.

`/path/to/file.html`:
```html
<html>
<head>
  <style>
    p { color: red; }
  </style>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <p>Test</p>
</body>
</html>
```

`style.css`
```css
p {
  text-decoration: underline;
}
```

Output:
```html
<html>
<head>
</head>
<body>
  <p style="color: red; text-decoration: underline;">Test</p>
</body>
</html>
```

## What is this useful for ?

- HTML emails. For a comprehensive list of supported selectors see
[here](http://www.campaignmonitor.com/css/)
- Embedding HTML in 3rd-party websites.
- Performance. Downloading external stylesheets delays the rendering of the page in the browser. Inlining CSS speeds up this process because the browser doesn't have to wait to download an external stylesheet to start rendering the page.


## Install

Install with [npm](https://npmjs.org/package/gulp-inline-css)

```
npm install --save-dev gulp-inline-css
```


## Usage

```js
var gulp = require('gulp'),
    inlineCss = require('gulp-inline-css');

gulp.task('default', function() {
    return gulp.src('./*.html')
        .pipe(inlineCss())
        .pipe(gulp.dest('build/'));
});
```

With options:

```js
var gulp = require('gulp'),
    inlineCss = require('gulp-inline-css');

gulp.task('default', function() {
    return gulp.src('./*.html')
        .pipe(inlineCss({
	        	applyStyleTags: true,
	        	applyLinkTags: true,
	        	removeStyleTags: true,
	        	removeLinkTags: true
        }))
        .pipe(gulp.dest('build/'));
});
```

Options are passed directly to [inline-css](https://github.com/jonkemp/inline-css).


## API

### inlineCss(options)


#### options.extraCss

Type: `String`  
Default: `""`

Extra css to apply to the file.


#### options.applyStyleTags

Type: `Boolean`  
Default: `true`

Whether to inline styles in `<style></style>`.


#### options.applyLinkTags

Type: `Boolean`  
Default: `true`

Whether to resolve `<link rel="stylesheet">` tags and inline the resulting styles.


#### options.removeStyleTags

Type: `Boolean`  
Default: `true`

Whether to remove the original `<style></style>` tags after (possibly) inlining the css from them.


#### options.removeLinkTags

Type: `Boolean`  
Default: `true`

Whether to remove the original `<link rel="stylesheet">` tags after (possibly) inlining the css from them.


#### options.url

Type: `String`  
Default: `filePath`

How to resolve hrefs.

#### options.preserveMediaQueries

Type: `Boolean`  
Default: `false`

Preserves all media queries (and contained styles) within `<style></style>` tags as a refinement when `removeStyleTags` is `true`. Other styles are removed.

#### options.applyWidthAttributes

Type: `Boolean`  
Default: `false`

Whether to use any CSS pixel widths to create `width` attributes on elements.

#### options.applyTableAttributes

Type: `Boolean`  
Default: `false`

Whether to apply the `border`, `cellpadding` and `cellspacing` attributes to `table` elements.

## License

MIT © [Jonathan Kemp](http://jonkemp.com)
