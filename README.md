less-modules
============

A set of LESS modules commonly used in my projects.

LESS modules can be loaded in your LESS styles as a complete package:

    @import "less-modules/less/less-modules";

… or as standalone modules:

    @import "less-modules/less/caret";
    @import "less-modules/less/grid";
    @import "less-modules/less/responsive-background";
    @import "less-modules/less/sticky-footer";

## Caret
Draws an arrow using only CSS properties.

Example LESS:

    .dropdown-handle {
        .caret();
    }

    .next {
        .caret-right(#fff, 1.2em, 1em);
    }

## Grid
Creates a justified grid of inline blocks.

There is no need to bother with absolute units or calculating margins. Grid item width is defined in percents and
margins are automatically adjusted to fit the container so everything works, no matter what size the container is.

Example LESS:

    .gallery {
        .grid();
    }

Grid item width is 22% by default (which results in 4 items per line) and can be easily adjusted:

    .gallery {
        .grid (33%);
    }

To avoid unwanted spacing of grid items which would break the grid, grid's font size is set to 0 and then restored back
to root font size in items. `rem` unit is used together with `px` fallback which can be defined as the second parameter
to make the fallback match your design.

Example LESS using optional absolute root font size (defaults to 16px):

    .gallery {
        .grid(33%, 13px);
    }
    
Credits: http://www.barrelny.com/blog/text-align-justify-and-rwd

## Responsive Background
Generates CSS code with different backgrounds for phone (default), tablet, and desktop. Default breakpoint values
(tablet 768px, desktop 992px) and image naming conventions are compatible with Bootstrap 3.

Mobile first and retina optimized.

Assumes that following images exist:

    ../images/[ image ]_xs@2x.jpg (retina phone)
    ../images/[ image ]_sm@2x.jpg (retina tablet)
    ../images/[ image ]_lg@2x.jpg (retina desktop)

Path to images `../images/` is relative to final CSS and can be modified using the `@path` parameter.

Example LESS:

    .section {
        .responsive-background('bg_section');
    }

Resulting CSS:

    .section {
        background-image: url('../images/bg_section_xs@2x.jpg');
    }

    @media screen and (min-width: 768px) {
        .section {
            background-image: url('../images/bg_section_sm@2x.jpg');
        }
    }

    @media screen and (min-width: 992px) {
        .section {
            background-image: url('../images/bg_section_lg@2x.jpg');
        }
    }

Example LESS using optional parameters—tablet breakpoint, desktop breakpoint, image path:

    .header {
        .responsive-background('backgrounds/bg_header', 800px, 1024px, '../assets/images/');
    }

## Sticky Footer
Makes page footer stick to the bottom of the screen.

Apply sticky footer on default markup:

    <html>
        …
        <body>
            …
            <footer>
                …
            </footer>
        </body>
    </html>

Example LESS:

    .sticky-footer();

Footer height value is `10em` by default and can be easily adjusted to fit your design:

    .sticky-footer(200px);

Sticky footer components can be also applied independently on markup:

    .my-wrapper {
        .sticky-footer-wrapper();
    }

    .my-wrapper-inner {
        .sticky-footer-sub-wrapper(5em);
    }

    .my-footer {
        .sticky-footer-footer(5em);
    }

Credits: http://mystrd.at/modern-clean-css-sticky-footer/
