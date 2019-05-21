# Picture-in-Picture V2 Explained

Many users want to continue consuming media while they interact with other
content, sites, or applications on their device. A common UI affordance for
this type of activity is Picture-in-Picture (PIP), where the video is
contained in a separate miniature window that is viewable above all other
activities. Most desktop and mobile OSs have announced or released
platform-level support for PIP, as have many browsers. The proposed
Picture-in-Picture API allows websites to initiate and control this behavior.

## Background: Picture-in-Picture V1

Picture-in-Picture launched for HTMLVideoElement early in 2019. The API was
designed to be extensible, like the Fullscreen API but at the moment is only
defined for video elements. The implementation takes the video layer and moves
it into a window that follows display rules specific to Picture-in-Picture
(always on top, fixed aspect ratio, etc.).

## What's Missing from V1?

Various websites expressed frustration around the limitations of the API. The
feature requests fell into two categories: customising the look & feel and
customising the user experience. The former can technically be done using canvas
elements but the latter requires a different model that would require user
interaction and therefore no longer be compatible with Android, iOS and macOS
APIs.

## Goals

  1. **Allow sites to Picture-in-Picture arbitary content**
  2. **A site should be able to choose whether that content is interactive.** If
the platform (e.g. Android) does not support interactive content then the site
should be able to easily fallback to non-interactive content

## Non-Goals

The Picture-in-Picture window is not a popup. Therefore, the content should not
live beyond the lifetime of the page.

## Sample Usage

Here's how a page might request Picture-in-Picture for it's media controls and
then move the video element to the new window. When the window is closed it will
then move the video element back to the page.

```html
<video id=video>
<div id=controls>
```

```js
const controls = document.getElementById('controls');
const video = document.getElementById('video');

const pipWindow = await controls.requestPictureInPicture({
  aspectRatio: 1,
  interactive: true
});

pipWindow.document.body.appendChild(video);

pipWindow.addEventListener('leavepictureinpicture', () => {
  document.body.appendChild(video);
});
```

The `aspectRatio` will be used to determine the size of the Picture-in-Picture
window.

## Alternatives Considered

We considered using window.open with additional `picture-in-picture` and
`interactive` options. However to expose that `interactive` or
`picture-in-picture` is not supported in `window.open()` would require us
to change this API to throw an additional exception which could cause
compatability issues. The new Picture-in-Picture window also does not have
a URL whereas `window.open()` has an argument for a URL so this may cause
confusion. Finally, `window.open`'s window also has a different lifetime
than the Picture-in-Picture window.

We also considered providing a URL to a document level API. However, this
causes security concerns as well as having a poor user experience due to having
to load the URL.

## Open Questions

The new `requestPictureInPicture` API has different parameters and a different algorithm
so we should consider renaming it
([#129](https://github.com/WICG/picture-in-picture/issues/129)).

# Acknowledgements

mounirlamouri@ wrote the original version of this proposal.
