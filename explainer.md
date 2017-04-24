# Picture in Picture API explained

## Objectives

Many users want to continue consuming media while they interact with other content, sites, or applications on their device. A common UI affordance for this type of activity is Picture in Picture (PIP), where the video is contained in a separate miniature window that is viewable above all other activities. Most desktop and mobile OSs have announced or released platform-level support for PIP, as have many browsers. The proposed Picture in Picture API allows websites to initiate and control this behavior.

## Use Cases

### Mandatory

*   A website wants to initiate a Picture in Picture experience from its own media or site controls.
*   A website wants to be notified when the user initiates Picture in Picture on a video from the browser UI in order to update its UI.

### For future considerations or candidates for first API

*   A website wants to be notified when the user initiates Picture in Picture from the browser UI in order to decide whether it wants to grant this request.
*   A website wants to customise the visible information in the Picture in Picture window.
*   A website wants to add user actions available in the Picture in Picture window.
*   A website wants to determine the size and position of the Picture in Picture window.

## Requirements

### Mandatory

*   The API will notify the website when it enters and leave Picture in Picture mode.
*   The API will allow the website to trigger Picture in Picture via a user gesture on a video element.
*   The API will allow the website to exit Picture in Picture.
*   The API will allow the website to check if Picture in Picture can be triggered for a given video.

### For future considerations or candidates for first API

*   The API will take a hint for the preferred window size and position which could be ignored by the user agent.
*   The API may be extended to allow an arbitrary element of the DOM to enter Picture in Picture.
*   The API may be extended to allow custom actions in the window UI.

## Proposed API

The proposed API is very similar to the Fullscreen API as they have similar properties. The API only applies on `HTMLVideoElement` at the moment but is meant to be extensible. In order to extend it, the `HTMLVideoElement` extension should apply to the `Element` interface instead.

```
dictionary PictureInPictureOptions {
  optional unsigned int width;
  optional unsigned int height;
  optional unsigned int top;
  optional unsigned int start;
};

partial interface HTMLVideoElement {
  Promise<void> requestPictureInPicture(PictureInPictureOptions? options);

  // On the fullscreen API, they live on the Document.
  attribute EventHandler onenterpictureinpicture;
  attribute EventHandler onleavepictureinpicture;
};

partial interface Document {
  readonly attribute boolean pictureInPictureEnabled;

  Promise<void> exitPictureInPicture();
};

partial interface DocumentOrShadowRoot {
  readonly attribute Element? pictureInPictureElement;
};
```


## Interaction with HTMLMediaElement

When a video is played in Picture in Picture, the states should transition as if it was played inline. That means that the events should fire at the same time, calling methods should have the same behaviour, etc. However, the user agent might transition out of Picture in Picture when the video element enters a state that is considered not compatible with Picture in Picture.

It is recommended that the video frames are not rendered in the page and in the Picture in Picture window but if they are, they must be kept in sync.

## Interaction with remote playback

The [Remote Playback specification](https://w3c.github.io/remote-playback/) defines a *local playback device* and a *local playback state*. For the purpose of Picture in Picture, the playback is local and regardless of whether it is played in page or in Picture in Picture.

## One Picture in Picture window

Operating systems with a PIP API usually restricts PIP to only one window. Whether only one window is allowed in PIP will be left to the implementation and the platform. However, because of the one PIP window limitation, the specification assumes that a given `Document` can only have one PIP instance.

What happens when there is a PIP request while a window is already in PIP will be left as an implementation details: the current PIP window could be closed, the PIP request could be rejected or even two PIP instances can be created. Regardless, the user agent will have to fire the appropriate events in order to notify the website of the PIP status changes.

## Feature Policy

An entry for Picture in Picture in the [Feature Policy specification](https://wicg.github.io/feature-policy/) could be added in order for embedders to prevent iframes to trigger Picture in Picture.

## Similar APIs

### Safari API

Safari iOS 9 has support for Picture in Picture since iOS 9 on iPads and support on Safari macOS was added with macOS 10.

The API allows the developer to:



*   Check if Picture in Picture is supported (`webkitSupportsPresentationMode()`)
*   Check if the video is currently played in Picture in Picture (`webkitPresentationMode()`)
*   Request the video to be played in Picture in Picture (`webkitSetPresentationMode()`)
*   Be notified when Picture in Picture state changes with the `webkitpresentationmodechanged` event.

Safari introduced a concept of *presentation mode* that supports the following states: `inline`, `fullscreen`, and `Picture in Picture`.

Safari does not seem to provide a mechanism for websites to be aware of a failure when entering Picture in Picture. It might mean that Safari will require the website to check if Picture in Picture is supported before entering.
