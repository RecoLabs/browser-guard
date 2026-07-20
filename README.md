<!--
  SOURCE OF TRUTH. This file is maintained in the private Reco monorepo at
  src/browser-guard/public-repo/README.md and synced to the root of the public
  RecoLabs/browser-guard repo by the "browser-guard release ZIPs" GitHub Action.
  Edit it there, not in the public repo — a direct edit in the public repo is
  overwritten on the next release.
-->

![Reco Browser Guard — login event tracking, app usage analysis, and shadow IT discovery](cover.jpg)

# Reco Browser Guard — Downloads

Manually-installable builds of the **Reco Browser Guard** browser extension for
**Google Chrome** and **Microsoft Edge**.

This repo hosts **only the built release ZIPs** — one Chrome ZIP and one Edge ZIP
per version, attached to each [GitHub Release](../../releases). It does **not**
contain the extension's source code.

> **When to use this.** These downloads are the **store-independent manual-install
> / hotfix path**: install or update Browser Guard without waiting on Chrome Web
> Store review. For fleet-wide managed rollout, prefer the Chrome Web Store
> listing or an MDM force-install policy — your Reco contact will tell you which
> applies to your organization.

## Download

Grab the latest version from the [**Releases** page](../../releases/latest). Each
release includes:

| Browser | Asset                              |
| ------- | ---------------------------------- |
| Chrome  | `browser-guard-<version>-chrome.zip` |
| Edge    | `browser-guard-<version>-edge.zip`   |

Download the ZIP that matches your browser, then follow the matching steps below.

## Install on Chrome

1. **Unzip** the downloaded `browser-guard-<version>-chrome.zip` into a folder you
   will keep (Chrome loads the extension from this folder — don't delete it).
2. Open `chrome://extensions` in the address bar.
3. Turn on **Developer mode** (toggle, top-right).
4. Click **Load unpacked** and select the unzipped folder.
5. Reco Browser Guard now appears in your extensions list and starts running.

## Install on Edge

1. **Unzip** the downloaded `browser-guard-<version>-edge.zip` into a folder you
   will keep (Edge loads the extension from this folder — don't delete it).
2. Open `edge://extensions` in the address bar.
3. Turn on **Developer mode** (toggle, left sidebar).
4. Click **Load unpacked** and select the unzipped folder.
5. Reco Browser Guard now appears in your extensions list and starts running.

## Updating to a new version

Manually-loaded extensions do **not** auto-update. To move to a newer build:

1. Download the new version's ZIP for your browser from
   [Releases](../../releases/latest) and unzip it (overwrite the same folder, or
   use a new one).
2. Open `chrome://extensions` / `edge://extensions`.
3. If you unzipped over the same folder, click the **Reload** (↻) icon on the
   Browser Guard card. If you used a new folder, remove the old entry and
   **Load unpacked** the new one.

The extension keeps its registration across a reload, so no re-registration is
needed for a routine version bump.

## Verify the install

- The Browser Guard card on the extensions page shows the version you installed.
- If your organization provisioned a gateway/registration token, the extension
  registers automatically and begins monitoring; otherwise open its **Options**
  page to complete registration.

## Support

Contact your Reco representative for the gateway URL, registration token, and any
installation help. This repository contains release artifacts only — please do
not open issues here.
