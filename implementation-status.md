# Implementation Status
This document shows the current implementation status of Picture-in-Picture on the different browsers.

<a href="#chrome"><img width=64 src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/chrome/chrome_128x128.png" alt="Chrome browser logo"></a><a href="#microsoft-edge"><img width=64 src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/edge/edge_128x128.png" alt="Microsoft Edge browser logo"></a><a href="#safari"><img width=64 src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/safari/safari_128x128.png" alt="Safari browser logo"></a><a href="#firefox"><img width=64 src="https://raw.githubusercontent.com/alrra/browser-logos/master/src/firefox/firefox_128x128.png" alt="Firefox browser logo"></a>

# Chrome

Work is in progress in [Chrome Canary](http://chrome.com/canary):

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

Tip: Chrome channel releases are tracked at [https://googlechromelabs.github.io/current-versions/](https://googlechromelabs.github.io/current-versions/).

## Notes
* Desktop includes Chrome OS, Linux, Mac, and Windows.
* [Issue 746182](http://crbug.com/746182): MediaStreams (WebRTC) are not supported yet.
* [Issue 854935](http://crbug.com/854935): Closed captions in Picture-in-Picture are not supported.

# Microsoft Edge
https://dev.windows.com/en-us/microsoft-edge/platform/status/pictureinpicture

# Safari
https://bugs.webkit.org/show_bug.cgi?id=182688

# Firefox
https://bugzilla.mozilla.org/show_bug.cgi?id=1463402

# Polyfill
https://github.com/gbentaieb/pip-polyfill/
