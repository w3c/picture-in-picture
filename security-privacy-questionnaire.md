# Security and Privacy Questionnaire

This document answers the [W3C Security and Privacy
Questionnaire](https://www.w3.org/TR/security-privacy-questionnaire/) for the
Picture-in-Picture specification.

**Does this specification deal with personally-identifiable information?**

No.

**Does this specification deal with high-value data?**

No.

**Does this specification introduce new state for an origin that persists across
browsing sessions?**

No.

**Does this specification expose persistent, cross-origin state to the web?**

No.

**Does this specification expose any other data to an origin that it doesn’t
currently have access to?**

No.

**Does this specification enable new script execution/loading mechanisms?**

No.

**Does this specification allow an origin access to a user’s location?**

No.

**Does this specification allow an origin access to sensors on a user’s
device?**

No.

**Does this specification allow an origin access to aspects of a user’s local
computing environment?**

[`pictureInPictureEnabled`](https://w3c.github.io/picture-in-picture/#dom-document-pictureinpictureenabled)
will reflect the state of the  "Picture-in-Picture" setting on the system or 
user agent.

**Does this specification allow an origin access to other devices?**

No.

**Does this specification allow an origin some measure of control over a user
agent’s native UI?**

An origin can create a floating video window always on top containing a video.

**Does this specification expose temporary identifiers to the web?**

No.

**Does this specification distinguish between behavior in first-party and
third-party contexts?**

No.

**How should this specification work in the context of a user agent’s
"incognito" mode?**

The feature should not behave differently in "incognito" mode.

**Does this specification persist data to a user’s local device?**

No.

**Does this specification have a "Security Considerations" and
"Privacy Considerations" section?**

https://w3c.github.io/picture-in-picture/#security-considerations

**Does this specification allow downgrading default security characteristics?**

No.
