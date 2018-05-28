# Picture-in-Picture API explained

![Screenshot of Presentation Mode Web API in Safari](/images/safari-pip.png)

## Objectives

Many users want to continue consuming media while they interact with other content, sites, or applications on their device. A common UI affordance for this type of activity is Picture-in-Picture (PIP), where the video is contained in a separate miniature window that is viewable above all other activities. Most desktop and mobile OSs have announced or released platform-level support for PIP, as have many browsers. The proposed Picture-in-Picture API allows websites to initiate and control this behavior.

## Use Cases

### Mandatory

*   A website wants to initiate a Picture-in-Picture experience from its own media or site controls.
*   A website wants to be notified when the user initiates Picture-in-Picture on a video from the browser UI in order to update its UI.
*   A website wants to inject an action into the Picture-in-Picture window by providing information used for the action in order to give its users control over the PiP’d media.
*   A website wants to be notified when the user interacts with the action in order to handle it.

### For future considerations or candidates for first API

*   A website wants to be notified when the user initiates Picture-in-Picture from the browser UI in order to decide whether it wants to grant this request.
*   A website wants to customise the visible information in the Picture-in-Picture window.
*   A website wants to add user actions available in the Picture-in-Picture window.
*   A website wants to determine the size and position of the Picture-in-Picture window.

## Requirements

### Mandatory

*   The API will notify the website when it enters and leave Picture-in-Picture mode.
*   The API will allow the website to trigger Picture-in-Picture via a user gesture on a video element.
*   The API will allow the website to exit Picture-in-Picture.
*   The API will allow the website to check if Picture-in-Picture can be triggered.
*   The API will notify the website if a custom action is interacted with via user gesture.

### For future considerations or candidates for first API

*   The API will take a hint for the preferred window size and position which could be ignored by the user agent.
*   The API may be extended to allow an arbitrary element of the DOM to enter Picture-in-Picture.
*   The API may be extended to allow custom actions in the window UI.

## Proposed API

The proposed API is very similar to the Fullscreen API as they have similar properties. The API only applies on `HTMLVideoElement` at the moment but is meant to be extensible. In order to extend it, the `HTMLVideoElement` extension should apply to the `Element` interface instead.

```
partial interface HTMLVideoElement {
  Promise<PictureInPictureWindow> requestPictureInPicture();
  Promise<void> setPictureInPictureControls(FrozenArray<CustomActionMetadata> action);

  // On the fullscreen API, they live on the Document.
  attribute EventHandler onenterpictureinpicture;
  attribute EventHandler onleavepictureinpicture;
  attribute EventHandler pictureinpicturecontrolsclick;

  [CEReactions]
  attribute boolean disablePictureInPicture;
};

partial interface Document {
  readonly attribute boolean pictureInPictureEnabled;

  Promise<void> exitPictureInPicture();
};

partial interface DocumentOrShadowRoot {
  readonly attribute Element? pictureInPictureElement;
};

interface PictureInPictureWindow {
  readonly attribute long width;
  readonly attribute long height;

  attribute EventHandler onresize;
};

interface CustomActionMetadata {
  attribute DOMString id;
  attribute DOMString label; // Description of the action.
  attribute FrozenArray<MediaImage> artwork;
};

dictionary MediaImage {
  required USVString src;
  DOMString sizes = "";
  DOMString type = "";
};
```

## Example

```html
<video id="video" src="https://example.com/file.mp4"></video>

<button id="pipButton"></button>

<script>
  // Hide button if Picture-in-Picture is not supported or disabled.
  pipButton.hidden = !document.pictureInPictureEnabled || video.disablePictureInPicture;

  const pipControls = [
    {
      id: 'thumbs-up',
      label: 'Thumbs up',
      icons: [ { src: 'http://dummyimage.com/96x96', sizes: '96x96', type: 'image/png' }, ...]
    }, {
      id: 'thumbs-down',
      label: 'Thumbs down',
      icons: [ { src: 'http://dummyimage.com/96x96', sizes: '96x96', type: 'image/png' }, ...]
    }
  ];

  await video.setPictureInPictureControls(pipControls);

  pipButton.addEventListener('click', function() {
    // If there is no element in Picture-in-Picture yet, let's request
    // Picture-in-Picture for the video, otherwise leave it.
    if (!document.pictureInPictureElement) {
      video.requestPictureInPicture()
      .then(pipWindow => {
        updateVideoSize(pipWindow.width, pipWindow.height);
        pipWindow.addEventListener('resize', function(event) {
          updateVideoSize(pipWindow.width, pipWindow.height);
        });
      })
      .catch(error => {
        // Video failed to enter Picture-in-Picture mode.
      });
    } else {
      document.exitPictureInPicture()
      .catch(error => {
        // Video failed to leave Picture-in-Picture mode.
      });
    }
  });

  function updateVideoSize(width, height) {
    // TODO: Update video size based on pip window width and height.
  }

  video.addEventListener('enterpictureinpicture', function() {
    // Video element entered Picture-In-Picture mode.
  });

  video.addEventListener('leavepictureinpicture', function() {
    // Video element left Picture-In-Picture mode.
  });

  video.addEventListener('pictureinpicturecontrolsclick', event => {
    switch (event.id) {
      'thumbs-up': ...
      'thumbs-down': ...
    };
  });
</script>
```

## Interaction with HTMLMediaElement

When a video is played in Picture-in-Picture, the states should transition as if it was played inline. That means that the events should fire at the same time, calling methods should have the same behaviour, etc. However, the user agent might transition out of Picture-in-Picture when the video element enters a state that is considered not compatible with Picture-in-Picture.

It is recommended that the video frames are not rendered in the page and in the Picture-in-Picture window but if they are, they must be kept in sync.

## Interaction with remote playback

The [Remote Playback specification](https://w3c.github.io/remote-playback/) defines a *local playback device* and a *local playback state*. For the purpose of Picture-in-Picture, the playback is local and regardless of whether it is played in page or in Picture-in-Picture.

## One Picture-in-Picture window

Operating systems with a PIP API usually restricts PIP to only one window. Whether only one window is allowed in PIP will be left to the implementation and the platform. However, because of the one PIP window limitation, the specification assumes that a given `Document` can only have one PIP instance.

What happens when there is a PIP request while a window is already in PIP will be left as an implementation details: the current PIP window could be closed, the PIP request could be rejected or even two PIP instances can be created. Regardless, the user agent will have to fire the appropriate events in order to notify the website of the PIP status changes.

## Feature Policy

An entry for Picture-in-Picture in the [Feature Policy specification](https://wicg.github.io/feature-policy/) could be added in order for embedders to prevent iframes to trigger Picture-in-Picture.

## Video Restrictions

Even though the API only applies on `HTMLVideoElement` at the moment, there is one way today to play a `HTMLCanvasElement` in Picture-in-Picture by using [`canvas.captureStream()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/captureStream).

```html
<canvas id="canvas"></canvas>

<button id="pipButton"></button>

<script>
  pipButton.addEventListener('click', function() {
    const video = document.createElement('video');
    video.srcObject = canvas.captureStream(60 /* fps */);
    video.requestPictureInPicture();
  });
</script>
```

## Similar APIs

### Safari API

Safari iOS 9 has support for Picture-in-Picture since iOS 9 on iPads and support on Safari macOS was added with macOS 10.

The API allows the developer to:

*   Check if Picture-in-Picture is supported (`webkitSupportsPresentationMode()`)
*   Check if the video is currently played in Picture-in-Picture (`webkitPresentationMode()`)
*   Request the video to be played in Picture-in-Picture (`webkitSetPresentationMode()`)
*   Be notified when Picture-in-Picture state changes with the `webkitpresentationmodechanged` event.

Safari introduced a concept of *presentation mode* that supports the following states: `inline`, `fullscreen`, and `picture-in-picture`.

Safari does not seem to provide a mechanism for websites to be aware of a failure when entering Picture-in-Picture. It might mean that Safari will require the website to check if Picture-in-Picture is supported before entering.
