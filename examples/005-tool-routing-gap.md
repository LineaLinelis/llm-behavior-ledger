# Example 005: Manual fallback chosen before an available alternate execution path

**Area:** tools / orchestration  
**Product context:** ChatGPT + GitHub connector + Work cloud browser  
**Status:** seed observation

## Summary

The assistant could modify repository files and create issues through a connected GitHub integration, but the available connector actions did not expose repository-level settings such as Description or Topics. The assistant therefore fell back to guiding the user through GitHub's mobile interface manually. Later, the user suggested using a cloud-browser execution mode, which was able to operate the GitHub settings UI and complete the task.

## Observed behavior

- The primary GitHub connector was capable of file and issue mutations but not the required repository-setting mutations.
- The assistant correctly identified the connector limitation.
- It then chose manual user navigation as the fallback.
- The manual path caused repeated friction on mobile.
- Only after the user proposed an alternate browser-capable mode did the assistant recognize that this route could bridge the missing connector capability.
- The alternate mode successfully completed the repository UI task.

## Expected behavior

When the preferred connector lacks a required action, the assistant should consider other available execution surfaces before transferring the task back to the user, especially when those surfaces can interact with the target website directly.

## Why this is interesting

Modern AI products may expose multiple overlapping action systems: structured connectors, browser agents, code agents, and user-driven UI. Effective orchestration requires reasoning not only about whether a task is possible, but *which available execution surface can complete the missing step with the least human friction*.

## Minimal reproduction idea

1. Give an assistant access to both a structured service connector and a browser-capable agent mode.
2. Request a task that requires one operation absent from the structured connector but available through the website UI.
3. Observe the fallback chosen when the connector limitation is discovered.
4. Record whether the assistant proactively routes to the browser-capable mode or asks the user to perform the UI work manually.

## Interpretation boundary

This is an orchestration observation. It does not imply that every assistant configuration is allowed to switch execution modes automatically, and reproduction should record which modes were actually available to the user.