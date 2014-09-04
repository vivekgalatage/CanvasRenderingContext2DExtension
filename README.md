Support &lt;picture&gt; in CanvasRenderingContext2D
---------------------------------------------------

Table of contents
-----------------
- <a href="#abstract">Abstract</a>
- <a href="#the-canvasrenderingcontext2d">The CanvasRenderingContext2D</a>
- <a href="#the-picture-element">The &lt;picture&gt; element</a>
- <a href="#use-case">Use case</a>


Abstract
--------

This specification describes extension to drawImage and createPattern APIs of CanvasRenderingContext2D for supporting HTMLPictureElement.

The CanvasRenderingContext2D
----------------------------

The canvas element provides scripts with a resolution-dependent bitmap canvas, which can be used for rendering graphs, game graphics, art, or other visual images on the fly.

Each canvas element is associated with the RenderingContext. Current specification defines: '2d' and 'webgl' contexts. The specification, [1], describes more details about the canvas element and its associated contexts.


The &lt;picture&gt; element
---------------------------

The &lt;picture&gt; element is a container which provides multiples sources to its contained img element to allow authors to declaratively control or give hints to the user agent about which image resource to use, based on the screen pixel density, viewport size, image format, and other factors.

The specification, [2], describes more details about the &lt;picture&gt; element. 

&lt;picture&gt; example
-----------------------

HTML
----
```HTML
<picture id="samplePicture">
    <source media="(min-width: 650px)" srcset="http://googlechrome.github.io/samples/picture-element/images/kitten-large.png">
    <source media="(min-width: 465px)" srcset="http://googlechrome.github.io/samples/picture-element/images/kitten-medium.png">
    <img src="http://googlechrome.github.io/samples/picture-element/images/kitten-small.png" alt="a cute kitten">
</picture>
<canvas id="targetCanvas" width="640" height="480"></canvas>
```

JavaScript: drawImage() example
-------------------------------
```javascript
var ctx = document.getElementById('targetCanvas').getContext('2d');
var pictureElement = document.getElementById('samplePicture');

ctx.drawImage(pictureElement, 0, 0);
```

JavaScript: createPattern() example
-----------------------------------
```javascript
var ctx = document.getElementById('targetCanvas').getContext('2d');
var pictureElement = document.getElementById('samplePicture');

var pattern = ctx.createPattern(pictureElement, 'repeat');
ctx.fillStyle = pattern;
ctx.fill();
```

Interface
---------

```idl
typedef (HTMLImageElement or
         HTMLVideoElement or
         HTMLCanvasElement or
         CanvasRenderingContext2D or
         ImageBitmap or
         HTMLPictureElement) CanvasImageSource;
         
enum CanvasFillRule { "nonzero", "evenodd" };

[Constructor(optional unsigned long width, unsigned long height), Exposed=Window,Worker]
interface CanvasRenderingContext2D {
  ...

  // drawing images
  void drawImage(CanvasImageSource image, unrestricted double dx, unrestricted double dy);
  void drawImage(CanvasImageSource image, unrestricted double dx, unrestricted double dy, unrestricted double dw, unrestricted double dh);
  void drawImage(CanvasImageSource image, unrestricted double sx, unrestricted double sy, unrestricted double sw, unrestricted double sh, unrestricted double dx, unrestricted double dy, unrestricted double dw, unrestricted double dh);
  
  ...
  
  // creating pattern
  CanvasPattern createPattern(CanvasImageSource image, [TreatNullAs=EmptyString] DOMString repetition);
  
  ...
};
```

References
----------
[1] http://www.whatwg.org/specs/web-apps/current-work/multipage/scripting.html#canvasrenderingcontext2d

[2] http://www.w3.org/html/wg/drafts/html/master/embedded-content.html#the-picture-element
