# OpenClaw (Fork)

This repository is a fork of the official OpenClaw project, customized for more automation.

## Documentation
For general usage, setup, and core features, please refer to the official OpenClaw documentation:
👉 **[docs.openclaw.ai](https://docs.openclaw.ai)**

---

## Custom Changes in this Fork

### 🚀 Mandatory Browser Auto-Attach
The Chrome Extension in this fork has been modified to support seamless, automated workflows.

- **Always Connected**: The extension is hardcoded to automatically "attach" to every tab you open (or when the browser starts).
- **Zero Config**: The "Automation" toggle has been removed from the Options page because it is now forced by default.
- **Improved UX**: Eliminates the manual step of clicking the extension icon for every new tab, making the `chrome` profile as autonomous as the `openclaw` profile.

> [!IMPORTANT]
> Because auto-attach is mandatory, using Chrome DevTools (F12) on an active tab will be blocked by the extension. You must detach the extension or disable it briefly if you need to inspect the page manually.

---
