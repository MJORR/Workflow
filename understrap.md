# Template Development using Understrap

For a local environment download and set up [Local by Flywheel](https://local.getflywheel.com/)

## Install

Install Wordpress and Understrap parent theme via dashboard/themes.

Install Understrap child theme via ZIP or git clone.

```
https://github.com/understrap/understrap-child.git
```

Install ACF via dashboard/plugins.

## Add brand colours, fix menu and add site gradient to SCSS

Edit:  _child_theme_variables.scss


```
$primary: #20B22B;
$secondary: #0A5B12;
$warning: #F41106;

.navbar-light {
    .navbar-nav {
        .nav-link{
            color: $secondary;
            font-size: 1.1rem;
            text-transform: uppercase;
        }
        .nav-link:hover {
            color: $primary;
        }
    }
    .navbar-toggler-icon {
        background-image: url("data:image/svg+xml,%3csvg viewBox='0 0 30 30' xmlns='http://www.w3.org/2000/svg'%3e%3cpath stroke='rgba(0,112,202, 0.5)' stroke-width='4' stroke-linecap='round' stroke-miterlimit='10' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e"); 
    }
    .navbar-toggler{
        border: none;
    }   
}

.site-gradient {
    background: $primary;
    background: linear-gradient(0deg, $primary 0%, $secondary 100%);
}
```

Open terminal and navigate to child theme folder, build files with:



```
gulp watch
```

## Add Swiper - mobile touch slider (Recommended)

1. NPM install from theme folder.

```
npm install swiper
```
2. Copy scss and js to src via gulpfile.js within copy-assets task
```
// Copy all Swiper SCSS files
gulp.src( `${paths.node}swiper/**/*.scss` )
.pipe( gulp.dest( `${paths.dev}/sass/swiper` ) );

// Copy all Swiper JS files
gulp.src( `${paths.node}swiper/src/swiper.js` )
.pipe( gulp.dest( `${paths.dev}/js/swiper` ) );

```
3. Add js to scripts via gulpfile.js within scripts task

```
 // Add swiper
 `${paths.dev}/js/swiper`

```
4. Import scss via child-theme.scss

```
// import swiper //
@import "../src/sass/swiper/swiper";   

```
Use gulp watch to update.
