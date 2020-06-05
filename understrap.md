# Template Development using Understrap

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

Edit:  _child_theme.scss

```
// custom css

:root {
    --bg-1: url(../images/woods.jpg) ;
  }


.navbar-light {

    box-shadow: 0 8px 8px rgba(0,0,0,0.1);

    .navbar-nav {
        .nav-link{
            color: $secondary;
            font-size: 1.2rem;
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

.site-footer {
    .navbar-light {
        box-shadow: none;
    }
}

.site-gradient {
    background: $primary;
    background: linear-gradient(0deg, $primary 0%, $secondary 100%);
}

.site-gradient-image {
    background: linear-gradient($secondary-rgba, $primary-rgba), var(--bg-1) center center;
    background-size: cover;
    color: white;
    min-height: 75vh;
}

.font-light-200 {
    font-weight: 200 !important;
    letter-spacing:0.05em
}

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

    button {
        background-color: $warning;
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

```

Open terminal and navigate to child theme folder, build files with:

```
gulp watch
```

## Add Swiper - mobile touch slider

1. NPM install from theme folder.

```
npm install swiper -g
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
5. Init new slider within custom-javascript.js.   See more layouts here: https://swiperjs.com/demos/

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
Use 'gulp dist' to copy the files to the /dist folder for distribution.

Use 'gulp scripts' just to compile the scripts.

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
3. Open src/ihavecookies/example.css copy the following styles.

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
5. Init new slider within custom-javascript.js.   See more layouts here: https://swiperjs.com/demos/

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
Use 'gulp dist' to copy the files to the /dist folder for distribution.

Use 'gulp scripts' just to compile the scripts.
