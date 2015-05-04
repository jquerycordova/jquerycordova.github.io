---
layout: template
title: Home
---

## What is cordova.jquery?

jQuery.cordova is a set of jQuery plugins for using native device functions on
your hybrid apps.

See [How do I create an hybrid app easily?](#how-do-i-create-an-hybrid-app-easily)


## Usage

    <head>
      <script src="cordova.js"></script>
      <script src="jquery.cordova.js"></script>
    </head>
    <body>
      <!-- the elements you will transform
        into device native functionality capable -->
      <img style="height:400px" class="camera"></img>
      <img style="height:400px" class="camera"></img>
      <img style="height:400px" class="camera"></img>
      
      <script>
        $(function() {
          // Make the elements receive the device events
          $(".camera").camera();
          // Set the image src on success
          $(".camera").on("success", function(event, imageData) {
            var src = "data:image/jpeg;base64," + imageData;
            $(this).attr("src", src);
          });
        });
      </script>
      
    </body>

## Installation

### Download

* [jquery.cordova.js](oskosk.github.com/jquery.cordova/dist/jquery.cordova.js)
* [jquery.cordova.min.js](oskosk.github.com/jquery.cordova/dist/jquery.cordova.js)

### Add jquery.cordova to your scripts in the HTML
  
    <head>
      <script src="jquery.cordova.js"></script>
    </head>
    <body>
      <img style="height:400px" id="picture">
      <script>
        $(function() {
          $("#picture").camera();
          $("#picture").on("success", function(event, imageData) {
            var src = "data:image/jpeg;base64," + imageData;
            $(this).attr("src", src);
          });
        });
      </script>
    </body>
<h2 class="page-header">API</h2>

Every __jquery.cordova__ widget is used as you use every jQuery plugin.

<p>
  NOTE: The majority of the plugins work on a real device, and not in the emulator
  nor the desktop browser. You also need to add the required Cordova plugin to your app
  for each specific functionality.
</p>

#### $(selector).camera(options)

Allows an HTML element to receive an `success` event when a photo 
is taken with the device's camera.

<blockquote>
  <p>
    Requires <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#Camera"> Cordova camera plugin</a>
  </p>
    <code>
      org.apache.cordova.camera
    </code>
</blockquote>


__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [getPicture](http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#cameraOptions)

__Events__

* `success` - Emitted when the user takes a picture.
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `imageData` - Base64 encoding of the image data, or the image file URI, depending on cameraOptions in effect. (String).
* `fail` - Emitted when the user cancels the picture.
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `msg` - A message that explains why the operation fails or if it was cancelled. 

__Example__

    <div id="camera"></div>

    <script type="text/javascript">
      $(function() {
        $("#camera").camera().on("success", function(imageData) {
          var src = "data:image/jpeg;base64," + imageData;
          $(this).attr("src", src);
        });
      });
    </script>
 
#### $(selector).galleryimage(options)

Allows an HTML element to receive an `success` event when the users selects
an image from the device's gallery.

<blockquote>
  <p>
    Requires <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#Camera"> Cordova camera plugin</a>
  </p>
    <code>
      org.apache.cordova.camera
    </code>
</blockquote>


__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [getPicture](http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#cameraOptions)
  * `sourceType` - Which camera function to use. 

__Events__

* `success` - Emitted when the user takes a picture.
  * `event` - The standard j!uery event object that is always the first argument to your callback.
  * `imageData` - Base64 encoding of the image data, or the image file URI, depending on cameraOptions in effect. (String).
* `fail` - Emitted when the user cancels the picture.
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `msg` - A message that explains why the operation fails or if it was cancelled. 

__Example__

    <div id="image"></div>

    <script type="text/javascript">
      $(function() {
        $("#image").galleryimage().on("success", function(imageData) {
          var src = "data:image/jpeg;base64," + imageData;
          $(this).attr("src", src);
        });
      });
    </script>

#### $.audiocapture(options)

**This plugin may not work on some devices if the operating system does not have
a default audio recording app installed**.

#### $.accelerometer(options)

#### $.compass(options)

#### $.contacts(options)




## How do I create an hybrid app easily?

### Add the libraries to your index.html file

* Add `cordova.js` to your directory and via a `<script>` tag inside your `index.html` (*).
* Add `jquery.cordova.js` to your html.
* Create an HTML element and transform it into a jquery.cordova widget (e.g. `("#el").camera()`).
* Create a config.xml file in the same directory where `index.html` resides.

_(*) `cordova.js` is also added automagically if you upload the code to Phonegap Build_.


### Convert the HTML into an hybrid app.

* Sign up at [Phonegap Build](http://build.phonegap.com) and create an app inside.
* Upload your HTML/JS/CSS and the `config.xml` files in a zip with the **Update code** button. <em>It will add cordova.js for you</em>
* Download the `apk` for instance (Android binary).
* See the magic.

*__PhoneGap__ is a registered trademark of Adobe*.