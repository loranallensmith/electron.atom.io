---
version: v1.4.12
category: API
redirect_from:
    - /docs/v0.24.0/api/screen/
    - /docs/v0.25.0/api/screen/
    - /docs/v0.26.0/api/screen/
    - /docs/v0.27.0/api/screen/
    - /docs/v0.28.0/api/screen/
    - /docs/v0.29.0/api/screen/
    - /docs/v0.30.0/api/screen/
    - /docs/v0.31.0/api/screen/
    - /docs/v0.32.0/api/screen/
    - /docs/v0.33.0/api/screen/
    - /docs/v0.34.0/api/screen/
    - /docs/v0.35.0/api/screen/
    - /docs/v0.36.0/api/screen/
    - /docs/v0.36.3/api/screen/
    - /docs/v0.36.4/api/screen/
    - /docs/v0.36.5/api/screen/
    - /docs/v0.36.6/api/screen/
    - /docs/v0.36.7/api/screen/
    - /docs/v0.36.8/api/screen/
    - /docs/v0.36.9/api/screen/
    - /docs/v0.36.10/api/screen/
    - /docs/v0.36.11/api/screen/
    - /docs/v0.37.0/api/screen/
    - /docs/v0.37.1/api/screen/
    - /docs/v0.37.2/api/screen/
    - /docs/v0.37.3/api/screen/
    - /docs/v0.37.4/api/screen/
    - /docs/v0.37.5/api/screen/
    - /docs/v0.37.6/api/screen/
    - /docs/v0.37.7/api/screen/
    - /docs/v0.37.8/api/screen/
    - /docs/latest/api/screen/
source_url: 'https://github.com/electron/electron/blob/master/docs/api/screen.md'
excerpt: "Retrieve information about screen size, displays, cursor position, etc."
title: "screen"
sort_title: "screen"
---

# screen

> Retrieve information about screen size, displays, cursor position, etc.

Process: [Main](http://electron.atom.io/docs/tutorial/quick-start#main-process), [Rendere)

You cannot require or use this module until the `ready` event of the `app`
module is emitted.

`screen` is an [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter).

**Note:** In the renderer / DevTools, `window.screen` is a reserved DOM
property, so writing `let {screen} = require('electron')` will not work.

An example of creating a window that fills the whole screen:

```javascript
const electron = require('electron')
const {app, BrowserWindow} = electron

let win

app.on('ready', () => {
  const {width, height} = electron.screen.getPrimaryDisplay().workAreaSize
  win = new BrowserWindow({width, height})
  win.loadURL('https://github.com')
})
```

Another example of creating a window in the external display:

```javascript
const electron = require('electron')
const {app, BrowserWindow} = require('electron')

let win

app.on('ready', () => {
  let displays = electron.screen.getAllDisplays()
  let externalDisplay = displays.find((display) => {
    return display.bounds.x !== 0 || display.bounds.y !== 0
  })

  if (externalDisplay) {
    win = new BrowserWindow({
      x: externalDisplay.bounds.x + 50,
      y: externalDisplay.bounds.y + 50
    })
    win.loadURL('https://github.com')
  }
})
```

## Events

The `screen` module emits the following events:

### Event: 'display-added'

Returns:

* `event` Event
* `newDisplay` [Display](http://electron.atom.io/docs/api/structures/display)

Emitted when `newDisplay` has been added.

### Event: 'display-removed'

Returns:

* `event` Event
* `oldDisplay` [Display](http://electron.atom.io/docs/api/structures/display)

Emitted when `oldDisplay` has been removed.

### Event: 'display-metrics-changed'

Returns:

* `event` Event
* `display` [Display](http://electron.atom.io/docs/api/structures/display)
* `changedMetrics` String[]

Emitted when one or more metrics change in a `display`. The `changedMetrics` is
an array of strings that describe the changes. Possible changes are `bounds`,
`workArea`, `scaleFactor` and `rotation`.

## Methods

The `screen` module has the following methods:

### `screen.getCursorScreenPoint()`

Returns `Object`:

* `x` Integer
* `y` Integer

The current absolute position of the mouse pointer.

### `screen.getPrimaryDisplay()`

Returns `Display` - The primary display.

### `screen.getAllDisplays()`

Returns `Display[]` - An array of displays that are currently available.

### `screen.getDisplayNearestPoint(point)`

* `point` Object
  * `x` Integer
  * `y` Integer

Returns `Display` - The display nearest the specified point.

### `screen.getDisplayMatching(rect)`

* `rect` [Rectangle](http://electron.atom.io/docs/api/structures/rectangle)

Returns `Display` - The display that most closely intersects the provided bounds.
