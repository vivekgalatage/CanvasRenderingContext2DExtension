Support &lt;picture&gt; element in CanvasRenderingContext2D
===========================================================

Abstract
--------

This specification describes extension to drawImage and createPattern APIs of CanvasRenderingContext2D for supporting HTMLPictureElement.


The &lt;picture&gt; element
---------------------------

The &lt;picture&gt; element is a container which provides multiples sources to its contained img element to allow authors to declaratively control or give hints to the user agent about which image resource to use, based on the screen pixel density, viewport size, image format, and other factors.

The specification, [1], describes more details about the &lt;picture&gt; element. 

&lt;picture&gt; example
-----------------------

<b>HTML</b>
```HTML
<picture id="samplePicture">
    <source media="(min-width: 650px)" srcset="http://googlechrome.github.io/samples/picture-element/images/kitten-large.png">
    <source media="(min-width: 465px)" srcset="http://googlechrome.github.io/samples/picture-element/images/kitten-medium.png">
    <img src="http://googlechrome.github.io/samples/picture-element/images/kitten-small.png" alt="a cute kitten">
</picture>
<canvas id="targetCanvas" width="640" height="480"></canvas>
```

<b>JavaScript: drawImage() example</b>
```javascript
var ctx = document.getElementById('targetCanvas').getContext('2d');
var pictureElement = document.getElementById('samplePicture');

ctx.drawImage(pictureElement, 0, 0);
```

<b>JavaScript: createPattern() example</b>
```javascript
var ctx = document.getElementById('targetCanvas').getContext('2d');
var pictureElement = document.getElementById('samplePicture');

var pattern = ctx.createPattern(pictureElement, 'repeat');
ctx.fillStyle = pattern;
ctx.fill();
```

References
----------
[1] http://www.w3.org/html/wg/drafts/html/master/embedded-content.html#the-picture-element
