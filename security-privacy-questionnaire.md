# Security and Privacy Questionnaire

This document answers the [W3C Security and Privacy Questionnaire]([https://w3ctag.github.io/security-questionnaire/](https://w3ctag.github.io/security-questionnaire/)) for the Picture-in-Picture specification.

**What information might this feature expose to Web sites or other parties, and for what purposes is that exposure necessary**

None.

**Is this specification exposing the minimum amount of information necessary to power the feature?**

Yes

**How does this specification deal with personal information or personally-identifiable information or information derived thereof?**

N/A

**How does this specification deal with sensitive information?**

N/A

**Does this specification introduce new state for an origin that persists
across browsing sessions?**

No

**What information from the underlying platform, e.g. configuration data, is
exposed by this specification to an origin?**

[`pictureInPictureEnabled`](https://wicg.github.io/picture-in-picture/v2/#dom-document-pictureinpictureenabled) will reflect the state of the "Picture-in-Picture"
setting on the system or user agent.

**Does this specification allow an origin access to sensors on a user’s device**

No

**What data does this specification expose to an origin? Please also document
what data is identical to data exposed by other features, in the same or different
contexts.**

None.

**Does this specification enable new script execution/loading mechanisms?**

No

**Does this specification allow an origin to access other devices?**

No

**Does this specification allow an origin some measure of control over a user
agent’s native UI?**

An origin can create a floating video window always on top containing a video or
arbitrary HTML element.

**What temporary identifiers might this this specification create or expose to
the web?**

None.

**How does this specification distinguish between behavior in first-party and
third-party contexts?**

It should behave the same.

**How does this specification work in the context of a user agent’s Private 
Browsing or "incognito" mode?**

The feature should not behave differently in "incognito" mode.

**Does this specification have a "Security Considerations" and "Privacy
Considerations" section?**

[https://wicg.github.io/picture-in-picture/v2/#security-considerations](https://wicg.github.io/picture-in-picture/#security-considerations)

**Does this specification allow downgrading default security characteristics?**

No

**What should this questionnaire have asked?**

N/A
