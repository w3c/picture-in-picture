# Implementation Status
This document shows the current implementation status of Picture-in-Picture on the different browsers.

# Chrome

Work is still in progress in [Chrome Canary](http://chrome.com/canary):

* The API has shipped in Chrome 70 for **Linux, macOS, and Windows** and Chrome 72 for **Chrome OS**.
* Know where to [report Picture-in-Picture bugs](https://bugs.chromium.org/p/chromium/issues/entry?components=Blink>Media>PictureInPicture).
* Root [Issue 806249](http://crbug.com/806249) and blocking issues are most authorative on status.

Feature/Platform                       | Desktop | Android |
-------------------------------------- | :-----: | :-----: |
`video.requestPictureInPicture()`      | 68      |         |
`video.onenterpictureinpicture`        | 68      |         |
`video.onleavepictureinpicture`        | 68      |         |
`video.disablePictureInPicture`        | 68      |         |
`document.pictureInPictureEnabled`     | 68      |         |
`document.pictureInPictureElement`     | 68      |         |
`document.exitPictureInPicture()`      | 68      |         |
`PictureInPictureWindow.width\|height` | 68      |         |
`PictureInPictureWindow.onresize`      | 68      |         |
`video.autoPictureInPicture`           | 👷      |         |
Media Session controls support         | 74      |         |

Tip: Chrome channel releases are tracked at [https://googlechromelabs.github.io/current-versions/](https://googlechromelabs.github.io/current-versions/).

## Notes
* Desktop includes Chrome OS, Linux, Mac, and Windows.
* [Issue 854935](http://crbug.com/854935): Closed captions in Picture-in-Picture are not supported.
* It is possible to disable auto PiP behaviour on Android 8+ by specifing `disablePictureInPicture` content attribute on the video tag prior entering full screen.

# Microsoft Edge
* Shipped in [Edge 79](https://www.microsoft.com/en-us/edge)

# Safari
Shipped in Safari 13.
https://developer.apple.com/documentation/safari_release_notes/safari_13_1_release_notes
https://bugs.webkit.org/show_bug.cgi?id=182688

# Firefox
Picture-in-Picture is a feature not exposed as a JavaScript API.
https://bugzilla.mozilla.org/show_bug.cgi?id=1463402

Mozilla position: [defer](https://github.com/mozilla/standards-positions/issues/72)

# Polyfill
https://github.com/gbentaieb/pip-polyfill/
