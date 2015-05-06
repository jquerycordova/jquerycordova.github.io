---
layout: template
title: Home
---

<hr id="about">
## What is jquery.cordova?

jQuery.cordova is a set of jQuery plugins for using native device functions on
your hybrid apps. It's based on `cordova.js` but <strong>jQuery.cordova</strong>
presents a nice jQuery-style interface.

See [How do I create an hybrid app easily?](#how-do-i-create-an-hybrid-app-easily)

## Usage

NOTE: The majority of the plugins work on a real device, and not in the emulator
nor the desktop browser. You also need to add the required Cordova plugin to your app
for each specific functionality.



    <head>
      <script src="cordova.js"></script>
      <script src="jquery.js"></script>
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


<h2 id="api" class="page-header">API</h2>

The API consists of a set of jQuery plugins. You use them like `$("#element").pluginname()`.

### Plugins

#### $(selector).camera(options)

Allows an HTML element to receive a `success` event when a photo 
is taken with the device's camera.

<blockquote>
  <p>
    Requires the <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#Camera"> Cordova camera plugin</a><br>
    Run <code>$ cordova plugin add org.apache.cordova.camera</code> 
    on a local Phonegap/Cordova project or add 
    <code>&lt;gap:plugin name="org.apache.cordova.camera" /%gt;</code> to you `config.xml`
  </p>
</blockquote>


__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [getPicture](http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#cameraOptions)
  * `triggerEvent` - (Selector) - An event name on which to launch the camera.
     The event is listend on the element designated by the `triggerElement`. **Default**: `click`.
  * `triggerElement` - (Selector) - A jQuery selector for an element on which 
    to listen the `triggerEvent`. **Default**: The element/s this plugin acts upon.

__Events__

* `success` - Emitted when the user takes a picture. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `imageData` - Base64 encoding of the image data, or the image file URI, depending on cameraOptions in effect. (String).
* `fail` - Emitted when the user cancels the picture. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `msg` - A message that explains why the operation fails or if it was cancelled. 

__Methods__

* **$(selector).camera('getPicture', options)** - Calls `navigator.camera.getPicture()`.
  * `options` - The same options that `navigatore.camera.getPicture()` accepts.
 

__Example__

    $(function() {
      $("#camera").camera().on("success", function(event, imageData) {
        var src = "data:image/jpeg;base64," + imageData;
        $(this).attr("src", src);
      });
    });

#### $(selector).galleryimage(options)

Allows an HTML element to receive a `success` event when the users selects
an image from the device's gallery.

<blockquote>
  <p>
    Requires <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#Camera"> Cordova camera plugin</a><br>
    <code>org.apache.cordova.camera</code>
  </p>
</blockquote>


__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [getPicture](http://cordova.apache.org/docs/en/3.3.0/cordova_camera_camera.md.html#cameraOptions)
  * `sourceType` - Which camera function to use. 

__Events__

* `success` - Emitted when the user takes a picture. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument
    to your callback.
  * `imageData` - Base64 encoding of the image data, or the image file URI, depending on cameraOptions in effect. (String).
* `fail` - Emitted when the user cancels the picture. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `msg` - A message that explains why the operation fails or if it was cancelled. 

__Methods__

* **$(selector).galleryimage('getPicture', options)** - Calls `navigator.camera.getPicture()`.
  * `options` - The same options that `navigatore.camera.getPicture()` accepts.

__Example__

    $(function() {
      $("#image").galleryimage().on("success", function(event, imageData) {
        var src = "data:image/jpeg;base64," + imageData;
        $(this).attr("src", src);
      });
    });



#### $.accelerometer(options)


Allows an HTML element to receive a `success` event periodically with current
accelerometer data.

<blockquote>
  <p>
    Requires <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_accelerometer_accelerometer.md.html#Accelerometer"> Cordova device-motion plugin</a><br>
    <code>org.apache.cordova.device-motion</code>
  </p>
</blockquote>


__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [watchAcceleration](http://cordova.apache.org/docs/en/3.3.0/cordova_accelerometer_accelerometer.md.html#accelerometer.watchAcceleration)
  * `frequency`: How often to retrieve the Acceleration in milliseconds. (Number) (Default: 10000).

__Events__

* `success` - Emitted when the user takes a picture. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument
    to your callback.
  * `acceleration` - (Object) Contains Accelerometer data captured at a specific point in time.
    * `x` -  Amount of acceleration on the x-axis. (in m/s^2) (Number)
    * `y` -  Amount of acceleration on the y-axis. (in m/s^2) (Number)
    * `z` -  Amount of acceleration on the z-axis. (in m/s^2) (Number)
    * `timestamp` - Creation timestamp in milliseconds. (DOMTimeStamp)  
* `fail` - Emitted when the watch fails. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `msg` - A message that explains why the operation fails or if it was cancelled. 

__Methods__

* **$(selector).accelerometer('watchAcceleration', options)** - Calls `navigator.accelerometer.watchAcceleration()`.
  * `options` - The same options that `navigatore.accelerometer.watchAcceleration()` accepts.
    * `frequency`: How often to retrieve the Acceleration in milliseconds. (Number) (Default: 10000).

__Example__

    $(function() {
      $("#image").galleryimage().on("success", function(event, acceleration) {
        $(this).html("Acceleration x: " + acceleration.x);
      });
    });


#### $.compass(options)

Allows an HTML element to receive a `success` event periodically with current
device orientation data.

<blockquote>
  <p>
    Requires <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_compass_compass.md.html#Compass"> Cordova device-orientation plugin</a><br>
    <code>org.apache.cordova.device-orientation</code>
  </p>
</blockquote>


__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [watchHeading](http://cordova.apache.org/docs/en/3.3.0/cordova_compass_compass.md.html#compass.watchHeading)
  * `frequency`: How often to retrieve the Heading data in milliseconds. (Number) (Default: 100).
  * `filter`: The change in degrees required to trigger a success event. (Number).

__Events__

* `success` - Emitted when interval is done. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument
    to your callback.
  * `heading` - (Object) Contains device heading data captured at a specific point in time.
    * `magneticHeading` -  Degrees 0-360, with 0 being the north (Number)
* `fail` - Emitted when the watch fails. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `msg` - A message that explains why the operation fails or if it was cancelled. 

__Methods__

* **$(selector).compass('watchHeading', options)** - Calls `navigator.compass.watchHeading()`.
  * `options` - The same options that `navigator.compass.watchHeading()` accepts.
    * `frequency`: How often to retrieve the heading data in milliseconds. (Number) (Default: 10000).
    * `filter`: The change in degrees required to trigger a success event. (Number).

__Example__

    $(function() {
      $("#image").compass().on("success", function(event, heading) {
        $(this).html("Device is headed at  " + heading.magneticHeading " degrees from North");
      });
    });



#### $.contacts(options)

Allows an HTML element to receive a `success` event with current
contacts data.

<blockquote>
  <p>
    Requires <a href="http://cordova.apache.org/docs/en/3.3.0/cordova_contacts_contacts.md.html#Contacts"> Cordova contacts plugin</a><br>
    <code>org.apache.cordova.contacts</code>
  </p>
</blockquote>


__Arguments__

* `options` - Object. Mostly, the options you can pass to Cordova's [contact.find()](http://cordova.apache.org/docs/en/3.3.0/cordova_contacts_contacts.md.html#contacts.find)
  * `contactFields` - (Array).
  * `contactFieldOptions`.
    * `filter`.
    * `multiple`.
__Events__

* `success` - Emitted when contacts are retrieved is done. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument
    to your callback.
  * `contacts` - (Array) An array with contacts information. Every contact is an Object with multiple properties.
* `fail` - Emitted when the watch fails. The event handler receives this arguments:
  * `event` - The standard jQuery event object that is always the first argument to your callback.
  * `msg` - A message that explains why the operation fails or if it was cancelled. 

__Methods__

* **$(selector).accelerometer('watchHeading', options)** - Calls `navigator.compass.watchHeading()`.
  * `options` - The same options that `navigator.compass.watchHeading()` accepts.
    * `frequency`: How often to retrieve the heading data in milliseconds. (Number) (Default: 10000).

__Example__

    $(function() {
      $("#image").compass().on("success", function(event, heading) {
        $(this).html("Device is headed at  " + heading.magneticHeading " degrees from North");
      });
    });



#### $.audiocapture(options)

**This plugin may not work on some devices if the operating system does not have
a default audio recording app installed**.


## How do I create an hybrid app easily?

#### Add the libraries to your index.html file

1. Add **jQuery** and **cordova.js** and **jquery.cordova.js** to your directory (*).
1. Add a `<script>` tag inside your `index.html` referencing `jquery.cordova.js`.
1. Create an HTML element and transform it into a jquery.cordova widget. e.g. `$("#el").camera()`.
1. Create a `config.xml` file in the same directory where `index.html` resides.

_(*) **cordova.js** is added automagically if you upload the code to Phonegap Build_.


#### Convert the HTML into an hybrid app.

* Sign up at [Phonegap Build](http://build.phonegap.com) and create an app inside.
* Upload your HTML/JS/CSS and the `config.xml` files in a zip with the **Update code** button. <em>It will add cordova.js for you</em>
* Download the Android binary for example and test in your device..

#### Debugging

* If Android, debug the app by connecting the device to your desktop via USB and with Chrome Inspect by entering `chrome://inspect` in the address bar.
* If iOS, debug by connecting your device via USB and using Safari Dev tools.

*__PhoneGap__ is a registered trademark of Adobe*.