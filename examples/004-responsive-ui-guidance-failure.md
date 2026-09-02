# Example 004: Navigation guidance fails to update from screenshot evidence

**Area:** tools / vision / reasoning  
**Interface:** mobile web  
**Status:** seed observation

## Summary

A user asked for help locating a repository description setting on GitHub from an iPhone. The assistant initially relied on standard desktop documentation and directed the user to an `About` panel and gear icon. Screenshots showed that the responsive mobile layout did not expose those controls, but the guidance continued through several increasingly indirect navigation steps before the assistant abandoned the incorrect path.

## Observed behavior

- The assistant began with documentation-based navigation appropriate to a desktop layout.
- The user supplied screenshots showing that the expected control was not present.
- The assistant updated parts of its hypothesis, but still continued along UI paths that did not lead to the requested setting.
- A later screenshot showed the Settings page, where the assistant briefly directed the user to an already-selected `General` section.
- Only after further failure did the assistant explicitly conclude that the requested Description control was not located in that Settings path.

## Expected behavior

When live visual evidence conflicts with a generic UI description, the assistant should prioritize the current screenshot, explicitly discard the contradicted navigation hypothesis, and avoid asking the user to continue down a path that is no longer supported by evidence.

## Why this is interesting

This tests whether a multimodal assistant can maintain and revise a working model of a responsive interface, rather than repeatedly mapping desktop documentation onto a different layout.

## Minimal reproduction idea

1. Choose a website whose mobile/responsive layout differs substantially from its desktop documentation.
2. Ask the model where a specific control is located.
3. Provide a screenshot in which the expected documented control is absent.
4. Continue with screenshots after each navigation step.
5. Record whether the model explicitly invalidates earlier assumptions or keeps adapting them without abandoning the wrong path.

## Interpretation boundary

This observation does not establish whether the failure came from visual understanding, documentation priors, conversation inertia, or another mechanism. It records the navigation behavior only.