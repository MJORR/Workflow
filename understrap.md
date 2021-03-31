# Theme Development using Understrap

The aim of this workflow is to provide a good starting point for website development.

For a local environment download and set up [Local by Flywheel](https://local.getflywheel.com/)

## Install

Install Wordpress and Understrap parent theme via dashboard/themes.

Install Understrap child theme via ZIP or git clone.

```
git clone https://github.com/understrap/understrap-child.git
```

Within theme folder:

```
sudo npm install gulp && sudo npm install --save del && sudo gulp build
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

Check Gulp version

```
gulp --version
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

Note: make sure edit is in correct file.

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

## To Do List


```
// Braw custom css 
body {
    background-color: #f7f7f5;
    font-family: 'Open Sans', sans-serif;
}

h1, h2, h3, h4{
    /*font-family: 'Montserrat', sans-serif;
    font-weight: 700;*/
    font-family: 'Poppins', sans-serif;
}

.braw-media {
    color: white;
}

/* navbar */
.navbar {
    z-index: 15;
    transition: 0.7s ease;
    background: white;
    
     .nav-white {
        background-color: white;
    }
    
    .collapsed {
    background: transparent;
    }
    
    .collapsed.nav-white {
        background-color: white;
    }
}

/*  burger  */
.navbar {
    
    .navbar-toggler {
        background: none;
        border: none;
      }
      
      .navbar-toggler:active,
      .navbar-toggler:focus {
        outline: 0;
      }
      
      .navbar-toggler .icon-bar {
        display: block;
        width: 32px;
        height: 5px;
        margin: 5px 0;
        transition: all 0.4s;
      }
      
      .navbar-toggler .icon-bar:nth-of-type(1) {
        transform: rotate(45deg) translate(8px, 6px);
        //background: white;
        background: $primary;
        width: 28px;
        border-radius: 3px;
      }
      
      .navbar-toggler .icon-bar:nth-of-type(2) {
        transform: rotate(720deg);
        opacity: 1;
        filter: alpha(opacity=1);
      }
      
      .navbar-toggler .icon-bar:nth-of-type(3) {
        transform: rotate(135deg) translate(-8px, 6px);
        //background: white;
        background: $primary;
        width: 28px;
        border-radius: 3px;
      }
      
      .navbar-toggler.collapsed .icon-bar:nth-of-type(1) {
        transform: rotate(0);
        background: white;
        border-radius: 0;
        width: 32px;
      }
      
      .navbar-toggler.collapsed .icon-bar:nth-of-type(2) {
        opacity: 1;
        filter: alpha(opacity=100);
        transform: rotate(0);
        background: white;
        border-radius: 0;
        width: 32px;
      }
      
      .navbar-toggler.collapsed .icon-bar:nth-of-type(3) {
        transform: rotate(0);
        background: white;
        border-radius: 0;
        width: 32px;
      }
}   

.site-gradient {
    background: $primary;
    background: linear-gradient(150deg, $gradient-dark 30%, $secondary 100%);
}

.background-image {
    background-repeat:no-repeat;
    background-position: center center;
    background-size: cover;
}

/* Card Columns 
.card-columns {
    column-count: 1!important;
overflow: visible;
}

@media (min-width: 576px) {
.card-columns {
    column-count: 2!important;
}
}

@media (min-width: 768px) {
.card-columns {
    column-count: 2!important;
}
}

@media (min-width: 992px) {
.card-columns {
    column-count: 3!important;
}
} */

/* Cookie Dialog */
#gdpr-cookie-message {
    position: fixed;
    right: 30px;
    bottom: 30px;
    max-width: 375px;
    background-color: #f7f7f5;
    padding: 20px;
    border-radius: 3px;
    box-shadow: 0 6px 6px rgba(0,0,0,0.25);
    margin-left: 30px;
    z-index: 1000;

    h4 {
        color: $primary;
        font-size: 18px;
        margin-bottom: 10px;
    }

    h5 {
        color: $primary;
        font-size: 14px;
        margin-bottom: 10px;
    }

    p {
        font-size: 14px;
        line-height: 1.5em;
    }

    ul {
        font-size: 14px;
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
        text-decoration: none;
        font-size: 15px;
        padding-bottom: 2px;
        border-bottom: 1px dotted rgba(255,255,255,0.75);
        transition: all 0.3s ease-in;
    }

    a:hover {
        color: $primary;
        border-bottom-color: var(--red);
        transition: all 0.3s ease-in;
    }

    button {
        background-color: $primary;
        color: #fff;
        border: none;
        border-radius: 4px;
        padding: 6px 10px;
        margin: 5px;
    }

    button:hover {
        opacity: 0.8;
    }

    button:disabled {
        opacity: 0.3;
    }
}

/* footer */
#wrapper-footer-full {
    a {
        color: white;
    }
    img {
        width: 72px;
        margin-bottom: 20px;
        margin-left: 12px;
    }
    ul {
        color: white;
        margin-left: -10px;
    }
    .menu:nth-of-type(1) {
        margin-bottom: 0;
    }
}

/* admin bar */
.admin-bar .fixed-top {
  top: 32px;
}

@media screen and (max-width: 782px) {
  .admin-bar .fixed-top {
    top: 46px;
  }
}

```

Add work flow for Braw Media child theme

Add checklist

Add settings or content import.
