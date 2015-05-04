---
layout: template
title: Home
---

## What is cordova.jquery?

<p>jQuery.cordova is a set of jQuery plugins for using native device functions on
your hybrid apps.</p>

* Add `jquery.cordova.js` to your html
* Create an HTML element and transform it into a jquery.cordova widget.
* Drop your HTML/JS/CSS files in <a href="http://build.phonegap.com">Phonegap Build</a>. <em>It will add cordova.js for you</em>
* See the magic.

## Usage

    <head>
      <!-- cordova.js is automatically added for you if you use Phonegap Build-->
      <script src="cordova.js"></script>
      <!-- jquery.cordova.js includes all the widgets-->
      <script src="jquery.cordova.js"></script>
    </head>
    <body>
      <!-- the elements you will transform into device native functionality capable -->
      <img style="height:400px" class="camera"></img>
      <img style="height:400px" class="camera"></img>
      <img style="height:400px" class="camera"></img>
      
      <script>
        $(function() {
          $(".camera").camera();
        });
      </script>
      
</body>

## Installation

### Download

* [jquery.cordova.js for the browser](oskosk.github.com/jquery.cordova/dist/jquery.cordova.js)
* [jquery.cordova.min.js](oskosk.github.com/jquery.cordova/dist/jquery.cordova.js)

### Via npm / using browserify

For using with browserify:

    $ npm install jquery.cordova

## Usage in the browser

    <script src="jquery.cordova.js"></script>
    <img style="height:400px" class="camera"></img>
    <script>
    $(function() {
      $(".camera").camera();
    });
    </script>

### Usage with browserify

<pre>
<code class="language-javascript">
var cordova = require("jquery.cordova");
</code>
</pre>

<h2 class="page-header">API</h2>

Every widget in __jquery.cordova__ is used as any jQuery plugin.


#### $.camera(options)

<blockquote>
  <p>
    Requires <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#Camera"> Cordova camera plugin</a>
  </p>
</blockquote>

Convert an `<img>` into a container for a photo from the device's camera.

__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [getPicture](http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#cameraOptions)
  * `sourceType` - Which camera function to use. 

__Events__

* `success` - Emitted when the user takes a picture.
  * `imageData` - Base64 encoding of the image data, or the image file URI, depending on cameraOptions in effect. (String).
* `fail` - Emitted when the user cancels the picture.

__Example__

    <div id="camera"></div>

    <script type="text/javascript">
      $(function() {
        $("#camera").camera().on("success", function(imageData) {
          $(this).attr("src", imageData);
        });
      });
    </script>
 


### $.contacts(options)
