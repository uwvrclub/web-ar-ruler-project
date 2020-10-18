# UW VR Club Workshop: AR Ruler with WebAR & A-Frame

## Presentation

### Welcome

Hello everyone! Thank you for coming to today's WebAR workshop! My name is Daekun, and I will be leading the workshop today. During the workshop, if you have any question at any point, please feel free to reach out to Falah, Saquib, Towseef, and Kira through the Discord chat. Today, we will be building an AR Ruler, similar to what you see on iOS Measure app, using WebAR and A-Frame.

### What’s UW VR?

UW VR is a student organization at the University of Waterloo dedicated to increasing awareness about careers in the field of Virtual Reality and Augmented Reality, encouraging project development among students, and hosting cool events around new experiences in VR. We started in 2018 as Canada's first ever student VR community, and our current team, consisting of Falah, Saquib, Towseef, Kira and myself, carry the same passion that grew the club to where it stands today. All of us have had extensive experience in the field, at places like Facebook's Oculus, Electronic Arts, and Spatial.

### AR/VR Brief Overview

We often use the term AR/VR to describe the field of 3D interactive technology. As many of you may know, AR stands for Augmented Reality, and VR stands for Virtual Reality. Another term for these fields is Mixed Reality.

As of now, VR is mostly focused on the gaming and educational market.

AR...

Potential...

### What we’re building today (30 second demo)

Moving onto the more exciting part! As I mentioned before,we will be building an AR ruler using WebAR and A-Frame. Before we get into the nitty-gritty parts of building this app, let's first see what it does and how it looks like.

(Demo part. Go watch it!)

### WebAR High-level Overview

**Entities** are things/objects in our world. We can attach different components (explained below) to an entity to define its behaviour. You, me, a book, a flying spaghetti monster: these are all just entities in the world of A-Frame. The only thing that makes them different and do things differently is the component attached to them. *Note:* An entity can have children entities under them.

**Components** are a chunk of data and functions. For instance, if you want to have an entity jump around the room, then you can attach a JumpAround component, give it some data like how fast the entity should jump around and which direction, and give it a function that updates every frame where the entity should jump to.

**Scene** is the root of all the entities of the world – just like a movie "scene". Under the hood, scene is really just another entity that's given a special name because it's the big parent entity of all. So, you can attach components to it. But there are only a handful of components you can attach to the scene, like `embedded`, `fog`, and `vr-mode-ui`. No need to know what these components are right now. Just know that **scenes are entities**.

Another important thing do know is **HTML DOM** (Document Object Model). They are objects that exist in a web page. Have you seen HTMLcode bits like `<html></html>` or `<p>Hello!</p>` before? These are examples of HTML DOMs. For instance, `<p>Hello!</p>` would be a DOM that represents a paragraph in a page.

If you're confused by any of these, don't worry. We will make sure to cover these topics as we go in the workshop. 


## Hands-on Mini-project

### Warmup Example: Show a T-Rex Dinosaur

#### Scene Setup

Here, we will be making a marker and show a GLTF model of 3D T-Rex on it! Open `aframe-ar/first.html` in your favourite text editor. In my case, I will be using Visual Studio Code.

We start by setting up the basic HTML document structure. You can ignore the stuff between `<!--` and `-->`, since they're just comments in the code to help you follow it.

```html
<!DOCTYPE html>
<html>
    <!-- <head> is where we do all the importing stuff -->
    <head>
        <!-- Put the loading code here -->
    </head>
    <!--<body> is where the contents go to-->
    <body style="margin : 0px; overflow: hidden;">
        <!-- Put the content code here -->
    </body>
</html>
```

As discussed before, things like `<head>` and `<body>` represent the HTML DOMs. `<head>` is where we import things like other people's code, images, and store metadata. `<body>` is where we put our actual content in. You can see that after `<body` there are some more code beside it. That is what's called an **attribute**, and they give properties to these DOMs, which could vary from the color, text alignment, or custom style description. This is important, since attributes are how we attach components to entities later.

Then, let's import the A-Frame and AR.js (an extension to A-Frame that handles the AR part) code.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <!-- Put the content code here -->
    </body>
</html>
```

The lines that we added import *JavaScript* code. They tell our page what to do, and without them, the page would be a dead list of characters, just like a Word document. JavaScript code can make the web page come alive. If you don't get it, this part isn't too important for now, so don't worry.

Next, we finally make use of A-Frame. Let's start by adding a scene.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <!-- This is where the entities in the scene goes. -->
        </a-scene>
    </body>
</html>
```

Here, you can see that we are also adding two components to the scene: `embedded` and `arjs`. `embedded` makes sure that the scene (i.e. the stream from camera) takes up the whole screen. `arjs` is, well, gets AR working in the scene!

Then, we probably need a camera in the scene to actually see what's going on. Let's add that.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <!-- Camera entity -->
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

We added an entity with a `camera` component. It's that simple. The simplicity of adding functionality to entities is what makes A-Frame so powerful!

#### Open In Web-browser

Let's open this page in our web browser now. We will use python's built-in web server. First, save your file in an empty folder somewhere as `first.html`. Then, open your terminal, which can be done by
* `Start Menu -> cmd` on Windows.
*  `/Applications/Utilities/Terminal` on Mac.
* You probably already know how to open termianl if you have Linux).

Run the following commands.

```
cd /project/folder/location
python3 -m http.server
```

A lot of people will probably be stuck on this, so please, pleeeeeease let us know if you're stuck so that we don't leave you behind!

Now, in your web browser (Chrome for me), go to the following link: [http://localhost:8000/first.html](http://localhost:8000/first.html). If you are seeing a camera/webcam view on the page, congrats! You've successfully setup an AR scene.

#### Marker Tracking

Alright, we have a camera in the scene now. How are we going to put a T-Rex here? With A-Frame, we need a **marker** in the real world to map your real world to the A-Frame scene. Hopefully you printed the markers that I asked you to print! If not, you can go to marker.pdf under the Github Repo and print that. If you don't have access to a printer, then you could use your phone or tablet and open the PDF file there on your screen.

These squares with thick black borders are what AR.js will detect and place the T-Rex on. I will demonstrate how these markers were made.

1. Go to [https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html)
2. Click "Upload" and upload whichever image you would like to put in the center of the marker.
    * Tip: Something with a few clear letters or symbols generally work the best.
3. Click "Download Marker", and it will proceed to download something like `marker_name.patt`. This file is what you will **place under the project folder (`aframe-ar`) to detect the marker.**
4. Click "Download Image". This file is what you will **print to display in front of the camera.**

Now, go back to `first.html`. We will add a marker entity that tracks Marker A that we created.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <!-- This is a marker entity that tracks Marker A -->
            <a-marker type="pattern" preset="custom" url="marker-a.patt"> <!-- Replace marker-a.patt with whichever name you gave the marker file. -->
                <!-- A child entity can go here! -->
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

`<a-marker>` is really just an entity with a `marker` component. A-Frame gives it a special name because of it's used quite often, and it is useful to give it a different name than other entities. Finally, let's put a T-Rex model under the marker as its **child**.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <a-marker type="pattern" preset="custom" url="marker-a.patt">
                <a-entity
                    position="0 0 0"
                    scale="0.05 0.05 0.05"
                    gltf-model="https://arjs-cors-proxy.herokuapp.com/https://raw.githack.com/AR-js-org/AR.js/master/aframe/examples/image-tracking/nft/trex/scene.gltf"
                ></a-entity>
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

This is a great example of how components work in A-Frame. To create a T-Rex model, we add a `position` component to specify where it should be with respect to the marker, `scale` to adjust how big the model should be, and `gltf-model` to put the actual 3D model to the entity.

Go back to [http://localhost:8000/first.html](http://localhost:8000/first.html) and refresh it to see your first AR app working. Place Marker A in front of the webcam and a T-Rex will appear in front of you! You can also use your phone to show Marker A and achieve the same thing.


### Main Project: AR Ruler!

Whew, we finally went through all that. Great job! And you ask: That was just the WARMUP??? Well, don't be too scared, because the code that you wrote so far is basically half of the main AR Ruler project!

#### Setup HTML code

So, open up `second.html` and copy over the code from `first.html`. Let's get rid of the T-Rex now since we won't be needing it.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <a-marker type="pattern" preset="custom" url="marker-a.patt">
                <!-- Got rid of T-Rex! -->
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

As I showed in the demo, our ruler will use two markers and measure the distance between the two. So let's begin by adding another marker entity that tracks Marker B.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <a-marker type="pattern" preset="custom" url="marker-a.patt">
                <!-- Children of Marker A -->
            </a-marker>
            <!-- New marker! -->
            <a-marker type="pattern" preset="custom" url="marker-b.patt">
                <!-- Children of Marker B -->
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

Now, just for our sake of seeing if the markers are being tracked or now, let's add little balls to the centres of the markers, red for Marker A, and blue for Marker B.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <a-marker type="pattern" preset="custom" url="marker-a.patt">
                <!-- Added red sphere -->
                <a-sphere color="red" radius="0.1"></a-sphere>
            </a-marker>
            <a-marker type="pattern" preset="custom" url="marker-b.patt">
                <!-- Added blue sphere -->
                <a-sphere color="blue" radius="0.1"></a-sphere>
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

Lastly, we will need some way to show the distance between the two markers. There's many ways to achieve this, but here, we will add a text entity to Marker A. Again, a text entity is really just an entity with a text component attached to it.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <a-marker type="pattern" preset="custom" url="marker-a.patt">
                <a-sphere color="red" radius="0.1"></a-sphere>
                <!-- Text label to show the distance between the two markers -->
                <a-text position="0 1 0" scale = "1 1 1" align="center" value="Hello World"></a-text>
            </a-marker>
            <a-marker type="pattern" preset="custom" url="marker-b.patt">
                <a-sphere color="blue" radius="0.1"></a-sphere>
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

Try opening [http://localhost:8000/second.html](http://localhost:8000/second.html) and bring Marker A and Marker B in front of the webcam. If you're seeing red and blue spheres on Marker A and Marker B, and a text label that says "Hello World" on Marker A, congrats! That's (almost) all of the HTML part of the project.

#### JavaScript Magic: Main Distance Logic

Now that we have the HTML part down, let's make these entities come alive with some JavaScript magic. First, we add another `<script>` **tag** in `<head>`.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script>
            // This is a comment. Anything after two slashes ("//") are ignored as comments.
            // This is where we will put our JavaScript code in.
        </script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <a-marker type="pattern" preset="custom" url="marker-a.patt">
                <a-sphere color="red" radius="0.1"></a-sphere>
                <a-text position="0 1 0" scale = "1 1 1" align="center" value="Hello World"></a-text>
            </a-marker>
            <a-marker type="pattern" preset="custom" url="marker-b.patt">
                <a-sphere color="blue" radius="0.1"></a-sphere>
            </a-marker>
            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
```

In A-Frame, the way we define behaviours of entities is components. Here, we want to measure the distance between the two markers and show that to the text label. So, let's make a new custom component of our own called `ruler-component`. It will have a `tick` function that will be called every frame by A-Frame.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script>
            AFRAME.registerComponent('ruler-manager', {
                tick: function () {
                    // This is where we do per-frame operation.
                    // In our case, measuring the distance between the two markers, and showing the distance on the text label.
                }
            });
        </script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <!-- Contents is omitted for now -->
        ...
    </body>
</html>
```

Next, we want to calculated the distance between the two markers. To do that, we need some way to get the positions of the markers. To do THAT, we need to be able to access the markers. In fact, we need ways to access the text component and the camera as well. So, let's give all of them some IDs so that we can refer to them in the JavaScript code, and then we can get the marker entities.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script>
            AFRAME.registerComponent('ruler-manager', {
                tick: function () {
                    var markerA = document.getElementById("marker-a");
                    var markerB = document.getElementById("marker-b");
                }
            });
        </script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <a-scene embedded arjs>
            <a-marker id="marker-a" type="pattern" preset="custom" url="marker-a.patt"> <!-- ID here -->
                <a-sphere color="red" radius="0.1"></a-sphere>
                <a-text id="distance-label" position="0 1 0" scale = "1 1 1" align="center" value="Hello World"></a-text> <!-- ID here -->
            </a-marker>
            <a-marker id="marker-b" type="pattern" preset="custom" url="marker-b.patt"> <!-- ID here -->
                <a-sphere color="blue" radius="0.1"></a-sphere>
            </a-marker>
            <a-entity camera id="camera"></a-entity> <!-- ID here -->
        </a-scene>
    </body>
</html>
```

To calculate the distance, we use the [distanceTo](https://threejs.org/docs/#api/en/math/Vector3.distanceTo) function, and print that to our console to check if our code is working.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script>
            AFRAME.registerComponent('ruler-manager', {
                tick: function () {
                    var markerA = document.getElementById("marker-a");
                    var markerB = document.getElementById("marker-b");

                    // Calculate the distance between the markers
                    var distance = markerA.object3D.position.distanceTo(markerB.object3D.position);
                    console.log(distance);
                }
            });
        </script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <!-- Contents is omitted for now -->
        ...
    </body>
</html>
```

Let's go back to [http://localhost:8000/second.html](http://localhost:8000/second.html), and refresh. Open the console (on Chrome, `top right corner's three-dot menu -> More Tools -> Developer Tools -> Console`). Try putting the two markers in front of the camera, and you should be able to see some numbers being printed to the console. As you pull the markers far apart, the number will increase.

But, you may notice that the numbers seem a little bit random. It definitely isn't in centimeters, inches, feet, meters, etc. ... So we need to scale the distance by some factor. To calculate this, put down the markers on the ground, measure the distance between the centres of the markers in centimeters, and check the A-Frame distance between the two markers by pointing the camera towards them. Then, `SCALE_FACTOR = real_distance_in_cm / a_frame_distance`. Let's multiply `distance` by the scale factor.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script>
            // We define the scale factor here.
            // Obtained using the formula above.
            var SCALE_FACTOR = 7.9;

            AFRAME.registerComponent('ruler-manager', {
                tick: function () {
                    var markerA = document.getElementById("marker-a");
                    var markerB = document.getElementById("marker-b");

                    var distance = markerA.object3D.position.distanceTo(markerB.object3D.position);
                    distance *= SCALE_FACTOR; // Multiply the distance by the scale factor.
                    console.log(distance);
                }
            });
        </script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <!-- Contents is omitted for now -->
        ...
    </body>
</html>
```

Go back to [http://localhost:8000/second.html](http://localhost:8000/second.html), refresh, and check that the distance makes more sense now.

#### Link UI and JavaScript Code

Finally the main logic of the app is working! We can measure a distance between two points using the markers. Let's display the distance on the text label we created before. To do that, we get the text entity and assign `value` attribute as the distance we got.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script>
            var SCALE_FACTOR = 7.9;

            AFRAME.registerComponent('ruler-manager', {
                tick: function () {
                    var markerA = document.getElementById("marker-a");
                    var markerB = document.getElementById("marker-b");

                    var distance = markerA.object3D.position.distanceTo(markerB.object3D.position);
                    distance *= SCALE_FACTOR;
                    console.log(distance);

                    var distanceLabel = document.getElementById("distance-label");
                    distanceLabel.setAttribute("value", distance.toFixed(1)); // .toFixed(1) limits the number to 1 decimal point
                }
            });
        </script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <!-- Contents is omitted for now -->
        ...
    </body>
</html>
```

Remember how we set `value="Hello World` for the text entity? Here, we are changing that initial value with the new distance value to change the text of the label.

Go back to [http://localhost:8000/second.html](http://localhost:8000/second.html), refresh, and check that the distance is being displayed on the text label on Marker A. But you will notice that the text label is quite difficult to see because it's staying perpendicular to the marker all the time. Let's make the text label face the camera all the time.

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.0/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script>
            var SCALE_FACTOR = 7.9;

            AFRAME.registerComponent('ruler-manager', {
                tick: function () {
                    var markerA = document.getElementById("marker-a");
                    var markerB = document.getElementById("marker-b");

                    var distance = markerA.object3D.position.distanceTo(markerB.object3D.position);
                    distance *= SCALE_FACTOR;
                    console.log(distance);

                    var distanceLabel = document.getElementById("distance-label");
                    distanceLabel.setAttribute("value", distance.toFixed(1));

                    var camera = document.getElementById("camera");
                    distanceLabel.object3D.lookAt(camera.object3D.position); // Make the label face the camera all the time.
                }
            });
        </script>
    </head>
    <body style="margin : 0px; overflow: hidden;">
        <!-- Contents is omitted for now -->
        ...
    </body>
</html>
```

Go back to [http://localhost:8000/second.html](http://localhost:8000/second.html), refresh, and play around with the markers. The label should face the camera, and it will be easier to check the distance now.

### Conclusion

Awesome!! You've created an AR ruler of your own. It was a long journey, but you've learned so much: the fundamentals of web programming, A-Frame and AR.js, and making A-Frame entities be interactable using JavaScript. There's so many more applications than an AR ruler, like a AR poster, or a marker-based WebAR map. Because your app will be on a web page, you will be able to reach out to so many more people than a traditional mobile AR app.

If you have any questions, please feel free to ask any of the mentors or myself. We will be hanging around in the Discord chat for a while, so if you got stuck at any point, please do reach out to us!