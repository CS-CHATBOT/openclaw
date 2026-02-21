# OpenClaw Customizations: Automation & Security

This document details the custom modifications applied to this OpenClaw setup to enhance automation while maintaining a secure environment.

## 🚀 Automation Suite

### 1. Mandatory Auto-Attach
The Chrome extension is hardcoded to automatically attach its debugger to every browser tab upon creation or browser startup.
- **Benefit**: Zero manual clicks needed to start automating a page.
- **Logic**: Located in `background.js`, enforcing a connection to the local relay immediately.

### 2. Automated Token Pairing (Auto-Pairing)
- **Change**: The mandatory `gatewayToken` is now generated **strictly at runtime** by the container and injected into the extension.
- **Why**: Ensures maximum security and zero configuration. The system is completely autonomous and ignores any externally provided tokens.
- **Implementation**: 
    - `setup-identity.sh`: Always generates a fresh random token on the first run, ignoring environment variables.
    - `setup-extension.sh`: Patches `background.js` at startup with this autonomous token.
- **Benefit**: The extension is "born" paired with your Gateway.

### 3. Automatic Extension Loading
The `openclaw` profile launcher is modified to automatically load the extension folder.
- **Implementation**: Updated `src/browser/chrome.ts` to detect the `assets/chrome-extension` directory and append the `--load-extension` flag to the browser launch arguments.

---

## 🛡️ Security & Privacy

### Why the Token is Mandatory
Because the extension automatically attaches to **all** tabs, it exposes your browser to the local relay port. To prevent unauthorized local apps or malicious websites from "hijacking" this connection, we enforce a strict **Token Authentication** protocol.
- **Secure Bridge**: Only connections with the correct `gatewayToken` are accepted by the relay.
- **Protection**: This ensures that even in an "Auto-Attach" state, only your specific OpenClaw instance can control the browser.

### Best Practices
- **Dedicated Profile**: Use a separate Chrome User Profile for OpenClaw activities to isolate your personal logins and sensitive data.
- **F12 Usage**: Note that Chrome's DevTools (F12) will be blocked on tabs where OpenClaw is attached. Detach the extension manually if you need to inspect a page.

---

## 📂 Key Files
- `OpenClaw-setup/Dockerfile`: Handles build-time token injection.
- `OpenClaw-setup/.env`: Source of the `OPENCLAW_GATEWAY_TOKEN`.
- `openclaw/assets/chrome-extension/background.js`: Extension automation logic.
- `openclaw/src/browser/chrome.ts`: Browser launch automation.
