# README #

##What is Waldo?##
Waldo is an extension for WordPress and other PHP-based applications that dynamically generates responsive CSS background image styles.

##Why Responsive Images?##
Mobile-first web development is the industry standard these days, and images are one of the leading causes of page bloat and slow loading times, especially on mobile devices and cellular networks. When compressed and appropriately sized images are served, page size and load time decrease drastically.

##Why Waldo?##
The state of handling responsive images with regards to web development is in flux, and there is no definitive solution to serving responsive full-cover background images. Waldo presents a solution to this problem, and it does so without utilizing JavaScript or (invalid) inline-styles.

##Dependencies##
The default configuration and usage guidelines for Waldo are based on WordPress 4.4+ with Advanced Custom Fields 5.3+.

###ACF Image Object###
This is built to handle ACF's Image Object which returns an associative array. If you are not using ACF the min-required array is:
```php
array(1) {
    ["sizes"]=>array(12) {
        ["small"]=>string(75) "http://localhost/site/wp-content/uploads/2013/10/image_url-150x150.jpg"
        ["medium"]=>string(75) "http://localhost/site/wp-content/uploads/2013/10/image_url-300x225.jpg"
        ["large"]=>string(76) "http://localhost/site/wp-content/uploads/2013/10/image_url-1024x768.jpg"
        ["xlarge"]=>string(76) "http://localhost/site/wp-content/uploads/2013/10/image_url-1024x768.jpg"
    }
}
```

###WordPress Image Sizes###

Also include the following image sizes in your functions.php:
```php
add_image_size('small', width, height);
add_image_size('xlarge', width, height);
```
Waldo uses a set of common breakpoints to determine the best image size and the above are missing, and essential to be set depending on your site.

##Configuration##
Add the image sizes supported by your theme and their associated min-width media query values in the *waldo\_sizes* array found in *waldo.php*.

*This is important, as the methods in class Waldo() rely on these key/value pairs to properly fetch image references and build the image styles.*

*For more information on adding support for custom image sizes in WordPress, visit [here](https://developer.wordpress.org/reference/functions/add_image_size/).*

##How to Use Waldo##
1. Copy **waldo-master** over to your WordPress theme.
2. Include *waldo.php* somewhere in your *functions.php* file.
    ```php
    // load Waldo for dynamic responsive CSS background images

    include('waldo-master/waldo.php');
    ```
3. Enqueue *waldo.css* in your *functions.php* file. Ensure the root path of this file is the same as the root path of the theme directory. This file is dynamically generated when Waldo is called.
4. Integrate Waldo into your template files. Before each instance where Waldo is to generate background image styles, get the Advanced Custom Field image object, and store to a variable. Set variable $waldo_styles to the function *waldoStylesArray()* to build styles and save to array. Pass in the ACF image object, a unique name (string), the saved styles array, and a unique class name (string) for this section.
    ```php
    $image = get_field('acf_image_field_name');

    $waldo_styles = $waldo->waldoStylesArray($image, 'unique-section-name', $waldo_styles, 'unique-section-class-name');
    ```
5. Preload your site cache or click through the pages that utilize the affected template(s) and refresh to view updated responsive image styles.

##What it Does##
Waldo dynamically generates styles for background images based on media queries and associated optimal image size. Waldo *only* sets the background-image property, any other styles may be included in the regular stylesheet for the site.

##Follow Us!##
Follow [@paper_leaf](https://twitter.com/paper_leaf) on Twitter.

##Copyright & License##
*© 2016 Paper Leaf Design*

*License: [GNU General Public License - Version 3](https://github.com/paper-leaf/waldo/blob/master/LICENSE.txt)*

##But Why *'Waldo'*?##
Who's the character most well known for always being in the background?

So the question here really should be: "Where's Waldo?" Get it? :D
