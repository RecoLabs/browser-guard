# Reco Browser Guard

Enterprise browser extension for security posture monitoring.

## Installation

This extension is distributed via MDM policy. See your IT administrator for deployment instructions.

Download the latest `.crx` package from the [Releases](https://github.com/RecoLabs/browser-guard/releases) page.

### MDM Force-Install Policy

```
pbfgnafbbeaneebmmmppeiogjldjlgdf;https://github.com/RecoLabs/browser-guard/releases/download/v1.0.0/updates.xml
```

---

## Publishing a New Version

### Option A: Command Line

```bash
cd src/browser-guard

# 1. Build the extension
npm run build

# 2. Pack into .crx (reuse the .pem key to keep the extension ID stable)
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --pack-extension=.output/chrome-mv3 \
  --pack-extension-key=.output/chrome-mv3.pem

# 3. Create a new release and upload the .crx
gh release create v1.1.0 \
  .output/chrome-mv3.crx \
  --repo RecoLabs/browser-guard \
  --title "Browser Guard v1.1.0" \
  --notes "Description of changes"

# 4. Create updates.xml pointing to the new version
cat > /tmp/updates.xml << 'EOF'
<?xml version='1.0' encoding='UTF-8'?>
<gupdate xmlns='http://www.google.com/update2/response' protocol='2.0'>
  <app appid='pbfgnafbbeaneebmmmppeiogjldjlgdf'>
    <updatecheck codebase='https://github.com/RecoLabs/browser-guard/releases/download/v1.1.0/chrome-mv3.crx'
                 version='1.1.0' />
  </app>
</gupdate>
EOF

# 5. Attach updates.xml to the new release
gh release upload v1.1.0 /tmp/updates.xml --repo RecoLabs/browser-guard

# 6. Update the previous release's updates.xml so existing installs auto-update
gh release upload v1.0.0 /tmp/updates.xml --repo RecoLabs/browser-guard --clobber
```

### Option B: GitHub UI (Manual)

1. **Build and pack** the extension locally (steps 1–2 above are still required)

2. **Go to** https://github.com/RecoLabs/browser-guard/releases

3. **Click "Draft a new release"**

4. **Create a new tag** — type the version (e.g., `v1.1.0`) in the "Choose a tag" dropdown and select "Create new tag on publish"

5. **Fill in the release details:**
   - Title: `Browser Guard v1.1.0`
   - Description: what changed in this version

6. **Attach files** — drag and drop (or click "Attach binaries"):
   - `chrome-mv3.crx` (from `.output/chrome-mv3.crx`)
   - `updates.xml` (see template below — update the version and codebase URL)

7. **Click "Publish release"**

8. **Update the previous release's `updates.xml`** to point to the new version:
   - Go to the previous release (e.g., v1.0.0)
   - Delete the old `updates.xml` asset (click the ✕ next to it)
   - Upload the new `updates.xml` (same file as step 6)

### updates.xml Template

Replace `VERSION` and `TAG` with the new version:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<gupdate xmlns='http://www.google.com/update2/response' protocol='2.0'>
  <app appid='pbfgnafbbeaneebmmmppeiogjldjlgdf'>
    <updatecheck codebase='https://github.com/RecoLabs/browser-guard/releases/download/TAG/chrome-mv3.crx'
                 version='VERSION' />
  </app>
</gupdate>
```

---

## How Auto-Update Works

Chrome periodically polls the `updates.xml` URL from the MDM policy. When it finds a version number higher than what's installed, it downloads and installs the new `.crx` automatically. No MDM policy change is needed — existing installs self-update.

## Important

- **Keep the `.pem` key safe** — it determines the extension ID. If lost, the ID changes and all MDM policies break.
- **Extension ID:** `pbfgnafbbeaneebmmmppeiogjldjlgdf`
- The `version` in `updates.xml` must match the `version` in the extension's `manifest.json`.
