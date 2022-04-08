# CustomPixiJSFiles
Tests with Pixijs production builds (pixi.min.js)

Added <code>this.onPreDraw()</code> in Sprite and Graphics <code>render()</code> methods to set different filter uniforms reused in each object.
<br>Added <code>_onLoad()</code> and <code>_onError()</code> on ImageResource that's called when it's loaded or there's an error.
<br>Added the capability to load textures in lower (custom) resolution.

## Loading Textures at a lower resolution
```
//This must be set to true
PIXI.settings.CREATE_IMAGE_BITMAP = true;

var tex = PIXI.Texture.from('somefile.png');

//Create bitmap from the image source rather than using blob, 
//because when using blob you're still loading the full size.
tex.baseTexture.resource.bitmapFromImage = true;

//Set the bitmap resolution
tex.baseTexture.resource.resolution = 0.5; 
//Half of the original image resolution, 
//floating points are rounded.

//Set the bitmap resizing quality (higher is slower)
tex.baseTexture.resource.resizeQuality = PIXI.BITMAP_QUALITY.LOW;

//Make sure scale your sprite and spritesheet 
//because of the lower resolution texture.

var sprite = new PIXI.Sprite(tex);
sprite.scale.set( 1 / tex.(...).resolution );
```
