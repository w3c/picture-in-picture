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
`video.disablePictureInPicture`        | 68      | 68      |
`document.pictureInPictureEnabled`     | 68      | 68      |
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

# Microsoft Edge
Under consideration.
https://developer.microsoft.com/en-us/microsoft-edge/platform/status/pictureinpicture/

# Safari
No public signals. 
https://bugs.webkit.org/show_bug.cgi?id=182688

# Firefox
No public signals. 
https://bugzilla.mozilla.org/show_bug.cgi?id=1463402

Mozilla position: https://github.com/mozilla/standards-positions/issues/72

# Polyfill
https://github.com/gbentaieb/pip-polyfill/
