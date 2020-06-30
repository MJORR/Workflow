# Theme Development using Understrap

The aim of this workflow is to provide a good starting point for website development.

For a local environment download and set up [Local by Flywheel](https://local.getflywheel.com/)

## Install

Install Wordpress and Understrap parent theme via dashboard/themes.

Install Understrap child theme via ZIP or git clone.

```
https://github.com/understrap/understrap-child.git
```

Install ACF via dashboard/plugins.

## Add brand colours, site gradient, menu changes and additional styles to SCSS

Edit:  _child_theme_variables.scss

```
//
// Color system
//

$primary: #20B22B;
$secondary: #0A5B12;
$warning: #F41106;

//transparent gradients
$primary-rgba: rgba(32, 178, 43, 0.5);
$secondary-rgba: rgba(10, 91, 18, 0.5);

```

Open terminal and navigate to child theme folder, build files with:

```
gulp watch
```

## Add Swiper - mobile touch slider

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
gulp.src( `${paths.node}swiper/**/*.js` )
.pipe( gulp.dest( `${paths.dev}/js/swiper` ) );

```
3. Add js to scripts via gulpfile.js within scripts task

```
// Add swiper
`${paths.dev}/js/swiper/js/swiper.js`,

```

4. Import scss via child-theme.scss

```
// import swiper //
@import "../src/sass/swiper/swiper";   

```

5. Add the required components within swiper.scss

```
//IMPORT_COMPONENTS
@import "./components/navigation/navigation";
```



6. Init new slider within custom-javascript.js.   See more layouts here: https://swiperjs.com/demos/

```
(function($){

    $(function() {

        /* Image Slider - Swiper */
        var imageSlider = new Swiper('.image-slider', {
        autoplay: {
            delay: 2000,
            disableOnInteraction: false
        },
        loop: true,
        spaceBetween: 30,
        slidesPerView: 5,
        breakpoints: {
            // when window is <= 580px
            580: {
                slidesPerView: 1,
                spaceBetween: 10
            },
            // when window is <= 768px
            768: {
                slidesPerView: 2,
                spaceBetween: 20
            },
            // when window is <= 992px
            992: {
                slidesPerView: 3,
                spaceBetween: 20
            },
            // when window is <= 1200px
            1200: {
                slidesPerView: 4,
                spaceBetween: 20
            },

        }
        });
		
    });

})(jQuery);  

```
Use 'gulp copy-assets' to copy the files.

Use 'gulp scripts' to compile the scripts.

## Add GDPR cookie consent

1. Navigate to 'src' folder.

```
git clone https://github.com/ketanmistry/ihavecookies.git
```

2. Add js to scripts via gulpfile.js within scripts task.

```
// Add jquery.ihavecookies.js
`${paths.dev}/ihavecookies/jquery.ihavecookies.js`,

```
3. Add the following styles to  '_child_theme.scss'.

<details>
  <summary>Click to expand!</summary>

```
/* Cookie Dialog */
#gdpr-cookie-message {
    position: fixed;
    right: 30px;
    bottom: 30px;
    max-width: 375px;
    background-color: $secondary;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 6px 6px rgba(0,0,0,0.25);
    margin-left: 30px;

    h4 {
        color: white;
        font-size: 18px;
        font-weight: 500;
        margin-bottom: 10px;
    }

    h5 {
        color: white;
        font-size: 15px;
        font-weight: 500;
        margin-bottom: 10px;
    }

    p {
        color: white;
        font-size: 15px;
        line-height: 1.5em;
    }

    ul {
        color: white;
        font-size: 15px;
        line-height: 1.5em;
    }

    p:last-child {
        margin-bottom: 0;
        text-align: right;
    }

    li {
        width: 49%;
        display: inline-block;
    }

    a {
        color: white;
        text-decoration: none;
        font-size: 15px;
        padding-bottom: 2px;
        border-bottom: 1px dotted rgba(255,255,255,0.75);
        transition: all 0.3s ease-in;
    }

    a:hover {
        color: white;
        border-bottom-color: var(--red);
        transition: all 0.3s ease-in;
    }

    button:disabled {
        opacity: 0.3;
    }
}  

```
</details>

## Add Masonry and ImageLoaded
Imageloaded activates masonry layout once files have loaded

```
npm install masonry-layout --save
npm install imagesloaded --save

```
1. Copy js to src via gulpfile.js within copy-assets task

```
// Copy Masonry-Layout JS files
    gulp.src( `${paths.node}masonry-layout/dist/masonry.pkgd.min.js` )
    .pipe( gulp.dest( `${paths.dev}/js/masonry` ) );
    
// Copy imagesLoaded JS files
    gulp.src( `${paths.node}imagesloaded/imagesloaded.pkgd.js` )
    .pipe( gulp.dest( `${paths.dev}/js/imageloaded` ) );
    
```
2. Add js to scripts via gulpfile.js within scripts task

```
// Add masonry
   `${paths.dev}/js/masonry/masonry.pkgd.js`,
   
// Add imagesloaded
   `${paths.dev}/js/imageloaded/imageloaded.pkgd.js`,
   
```
3. Initialize with jQuery add to custom-javascript.js

```
// Masonry 
jQuery(function($){
   
    // init Masonry
    var $grid = jQuery('.gallery-wrapper').masonry({
        // set itemSelector so .grid-sizer is not used in layout
        itemSelector: '.grid-item',
        // use element for option
        columnWidth: '.grid-sizer',
        percentPosition: true,
        transitionDuration: 0,
    });
    
    // layout Masonry after each image loads
    $grid.imagesLoaded().progress( function() {
        $grid.masonry('layout');
    });
});
```

4.  Add CSS to custom_theme.scss

```
/* Masonry */
.gallery-wrapper {
    overflow: hidden;
}
  
.grid-item {
    padding-bottom: 30px;
}
```
5. Add album partial. 

## Add Lightbox

Add fancyapps to src folder
```
https://github.com/fancyapps/fancybox.git
```
Gulp file 
```
// Add fancybox
`${paths.dev}/fancybox/dist/jquery.fancybox.js`,
```

