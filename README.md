<!--
  SOURCE OF TRUTH. This file is maintained in the private Reco monorepo at
  src/browser-guard/public-repo/README.md and synced to the root of the public
  RecoLabs/browser-guard repo by the "browser-guard release ZIPs" GitHub Action.
  Edit it there, not in the public repo — a direct edit in the public repo is
  overwritten on the next release.
-->

![Reco Browser Guard — login event tracking, app usage analysis, and shadow IT discovery](cover.jpg)

# Reco Browser Guard — Downloads

Distribution repository for the **Reco Browser Guard** browser extension for
**Google Chrome** and **Microsoft Edge**.

Every [GitHub Release](../../releases) carries the built artifacts for one
version — this repo does **not** contain the extension's source code:

| Asset                                | Purpose                                                              |
| ------------------------------------ | -------------------------------------------------------------------- |
| `chrome-mv3.crx` / `updates.xml`     | Chrome self-hosted CRX + auto-update feed (MDM force-install)         |
| `edge-mv3.crx` / `edge-updates.xml`  | Edge self-hosted CRX + auto-update feed (MDM force-install)           |
| `browser-guard-<version>-chrome.zip` | Chrome manual-install build (unpacked)                                |
| `browser-guard-<version>-edge.zip`   | Edge manual-install build (unpacked)                                  |

All channels share **one permanent extension ID:**
`pliigefhlibccjajneblehcejkajlhoe`.

## Choose an installation method

| Method                             | Best for                                  | Auto-updates | Section                                              |
| ---------------------------------- | ----------------------------------------- | ------------ | ---------------------------------------------------- |
| **Chrome Web Store**               | General availability on Chrome            | Yes (Google) | [Chrome Web Store](#method-1--chrome-web-store)      |
| **MDM force-install (CRX)**        | Managed fleets (IT-administered rollout)  | Yes (feed)   | [MDM force-install](#method-2--mdm-force-install)   |
| **Manual install (ZIP)**           | Store-independent / hotfix / single user  | No (manual)  | [Manual install](#method-3--manual-install-zip)     |

> If your organization is centrally managed, prefer the **Chrome Web Store** or
> **MDM force-install** method — both auto-update. The **manual ZIP** path is the
> store-independent hotfix option and does not auto-update. Your Reco contact
> will tell you which method applies to your organization.

---

## Method 1 — Chrome Web Store

The standard install for Chrome users. Google delivers updates automatically.

1. Open the Reco Browser Guard listing on the Chrome Web Store (ask your Reco
   contact for the listing link).
2. Click **Add to Chrome** → **Add extension**.

For managed fleets that track the store, the MDM force-install update URL is
`https://clients2.google.com/service/update2/crx` (see Method 2).

---

## Method 2 — MDM force-install

For IT administrators rolling out to a managed fleet. Chrome/Edge install the
extension automatically from the self-hosted feed in this repo and keep it up to
date whenever a new release is published — no policy change needed per version.

Add the matching entry to your `ExtensionInstallForcelist` policy
(`extension_id;update_url`):

| Browser | Preference domain    | Forcelist entry                                                                                              |
| ------- | -------------------- | ------------------------------------------------------------------------------------------------------------ |
| Chrome  | `com.google.Chrome`  | `pliigefhlibccjajneblehcejkajlhoe;https://github.com/RecoLabs/browser-guard/releases/latest/download/updates.xml`      |
| Edge    | `com.microsoft.Edge` | `pliigefhlibccjajneblehcejkajlhoe;https://github.com/RecoLabs/browser-guard/releases/latest/download/edge-updates.xml` |

To install from the Chrome Web Store instead of the self-hosted CRX, keep the
same extension ID and change only the Chrome update URL to
`https://clients2.google.com/service/update2/crx`.

> **Do not point the same managed fleet at both** the self-hosted feed and the
> Chrome Web Store — pick one update source per fleet. Reco provides full
> managed-config (registration token, gateway URL, etc.) documentation
> separately.

---

## Method 3 — Manual install (ZIP)

The store-independent / hotfix path: install or update Browser Guard without
waiting on Chrome Web Store review. Manually-loaded extensions do **not**
auto-update — you re-load a new ZIP to upgrade.

Grab the latest version from the [**Releases** page](../../releases/latest) and
download the ZIP that matches your browser:

| Browser | Asset                                |
| ------- | ------------------------------------ |
| Chrome  | `browser-guard-<version>-chrome.zip` |
| Edge    | `browser-guard-<version>-edge.zip`   |

### Install on Chrome

1. **Unzip** the downloaded `browser-guard-<version>-chrome.zip` into a folder
   you will keep (Chrome loads the extension from this folder — don't delete it).
2. Open `chrome://extensions` in the address bar.
3. Turn on **Developer mode** (toggle, top-right).
4. Click **Load unpacked** and select the unzipped folder.
5. Reco Browser Guard now appears in your extensions list and starts running.

### Install on Edge

1. **Unzip** the downloaded `browser-guard-<version>-edge.zip` into a folder you
   will keep (Edge loads the extension from this folder — don't delete it).
2. Open `edge://extensions` in the address bar.
3. Turn on **Developer mode** (toggle, left sidebar).
4. Click **Load unpacked** and select the unzipped folder.
5. Reco Browser Guard now appears in your extensions list and starts running.

### Updating to a new version

1. Download the new version's ZIP for your browser from
   [Releases](../../releases/latest) and unzip it (overwrite the same folder, or
   use a new one).
2. Open `chrome://extensions` / `edge://extensions`.
3. If you unzipped over the same folder, click the **Reload** (↻) icon on the
   Browser Guard card. If you used a new folder, remove the old entry and
   **Load unpacked** the new one.

The extension keeps its registration across a reload, so no re-registration is
needed for a routine version bump.

---

## Verify the install

- The Browser Guard card on the extensions page shows the version you installed
  and the ID `pliigefhlibccjajneblehcejkajlhoe`.
- If your organization provisioned a gateway/registration token, the extension
  registers automatically and begins monitoring; otherwise open its **Options**
  page to complete registration.

## Support

Contact your Reco representative for the gateway URL, registration token, and any
installation help. This repository contains release artifacts only — please do
not open issues here.
