https://medium.com/@jack.yin/exclude-directory-pattern-in-gulp-with-glob-in-gulp-src-9cc981f32116

```javascript
gulp.task('default', function() {
  return gulp.src([
      'src/**/*',         //select all files
      '!src/**/_*/',      //exclude folders starting with '_'
      '!src/**/_*/**/*',  //exclude files/subfolders in folders starting with '_'
    ])
    .pipe(gulp.dest('dist'));
});
```