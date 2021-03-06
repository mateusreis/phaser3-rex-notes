## Introduction

Camera to display game objects, built-in object of phaser.

- Author: Richard Davey

## Usage

### Get camera

Each scene has one or more cameras.

- Main camera
    ```javascript
    var camera = scene.cameras.main;
    ```
- Add new camera
    ```javascript
    var camera = scene.cameras.add(x, y, width, height);
    ```

- Add existed camera
    ```javascript
    scene.cameras.addExisting(camera);
    ```

### Remove camera

```javascript
scene.cameras.remove(camera);
```

### Destroy camera

```javascript
camera.destroy();
```

### Set view port

```javascript
camera.setViewport(x, y, width, height);
```

```javascript
camera.setPosition(x, y);
// camera.x = x;
// camera.y = y;
```

```javascript
camera.setSize(width, height);
// camera.width = width;
// camera.height = height;
```

- Position
    - Top-left
        ```javascript
        var x = camera.x;
        var y = camera.y;
        ```
    - Center
        ```javascript
        var centerX = camera.centerX;
        var centerY = camera.centerY;
        ```
- Width & height
    ```javascript
    var width = camera.width;
    var height = camera.height
    ```

### Visible

A visible camera will render and perform input tests.
An invisible camera will not render anything and will skip input tests.

```javascript
camera.setVisible(value);
// camera.visible = value
```

```javascript
var visible = camera.visible;
```

### Scroll camera

```javascript
camera.setScroll(x, y)
```

```javascript
camera.scrollX = scrollX;
camera.scrollY = scrollY;
```

```javascript
camera.centerToBounds();
```

```javascript
camera.centerToSize();
```

#### Follow game object

- Start following
    ```javascript
    camera.startFollow(gameObject);
    // camera.startFollow(gameObject, roundPx, lerpX, lerpY, offsetX, offsetY);  // 
    ```
    roundPx : set true to round the camera position to integers
- Stop following
    ```javascript
    camera.stopFollow();
    ```
- Set follow offset
    ```javascript
    camera.setFollowOffset(x, y);
    ```
- Set lerp
    ```javascript
    camera.setLerp(x, y);
    ```

#### Scroll factor

See [Scroll factor](gameobject.md#scroll-factor) in game object.

#### Set bounds

```javascript
camera.setBounds(x, y, width, height)
```

### Zoom

```javascript
camera.setZoom(v);
// camera.zoom = v;
// var zoom = camera.zoom;
```

### Rotation

Spin camera around center.

```javascript
camera.setRotation(rad);
// camera.setAngle(degree);
// camera.rotation = rad;
```

### Effects

#### Fade-in / fade-out

```javascript
camera.fadeIn(duration);   // duration in ms
// camera.fadeIn(duration, red, green, blue, callback, context);
// red/green/blue: the value to fade the red/green/blue channel from. A value between 0 and 255.
```

```javascript
camera.fadeOut(duration);   // duration in ms
// camera.fadeOut(duration, red, green, blue, callback, context);
```

##### Events

```javascript
camera.on('camerafadeincomplete', camera, fade);
```

```javascript
camera.on('camerafadeoutcomplete', camera, fade);
```

#### Flash

```javascript
camera.flash(duration);   // duration in ms
// camera.flash(duration, red, green, blue, force, callback, context);
```

##### Events

```javascript
camera.on('cameraflashstart', camera, flash, duration, red, green, blue);
```

```javascript
camera.on('cameraflashcomplete', camera, flash);
```

#### Shake

```javascript
camera.shake(duration);   // duration in ms
// camera.shake(duration, intensity, force, callback, context);  // callback: invoked when completed
```

##### Events

```javascript
camera.on('camerashakestart', camera, shake, duration, intensity);
```

```javascript
camera.on('camerashakecomplete', camera, shake);
```

### Set background color

```javascript
camera.setBackgroundColor(color);
```

### Ignore game object

Ignored game objects won't show at that camera.

```javascript
camera.ignore(gameObject);  // a game object, or an array of game objects
```

### Camera Controllor

#### Create controllor

```javascript
// var cursors = scene.input.keyboard.createCursorKeys();
var config = {
    camera: camera,

    left: cursors.left,    // { isDown, isUp }
    right: cursors.right,  // { isDown, isUp }
    up: cursors.up,        // { isDown, isUp }
    down: cursors.down,    // { isDown, isUp }
    zoomIn: null,          // { isDown, isUp }
    zoomOut: null,         // { isDown, isUp }

    zoomSpeed: 0.01,

    acceleration: null,
    // acceleration: {
    //    x: 0,
    //    y: 0
    // }

    drag: null,
    // drag: {
    //    x: 0,
    //    y: 0
    // }

    maxSpeed: null
    // maxSpeed: {
    //    x: 0,
    //    y: 0
    // }
};
var controls = new Phaser.Cameras.Controls.SmoothedKeyControl(config);
// var controls = new Phaser.Cameras.Controls.FixedKeyControl(config);
```

#### Update

```javascript
scene.update = function (time, delta) {
    controls.update(delta);
}
```

#### Start / stop

```javascript
controls.start();
```

```javascript
controls.stop();
```

#### Other methods

```javascript
controls.setCamera(camera);
```