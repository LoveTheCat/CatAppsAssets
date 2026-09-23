# CatAppsAssets

Public static assets for CatApps.

This repository is intentionally **public** and is the canonical delivery location for static files that must be retrievable without authentication by browsers or external services.

## Scope

Allowed:
- favicons and public application icons
- public images used by CatApps
- static public HTML when a plain unauthenticated file is genuinely required
- other non-secret static assets that must have a stable public HTTPS URL

Not allowed:
- source code or private application configuration
- credentials, tokens, secrets, private URLs or user data
- patient/clinic confidential data
- files that require access control
- runtime databases or application state

## Layout

- `images/favicons/<AppName>.png` — GAS/web favicons
- `images/<category>/...` — other public images
- `html/...` — exceptional public static HTML

Create new directories only when needed.

## Favicon standard

GAS HtmlService apps use `HtmlOutput.setFaviconUrl()` with a public HTTPS PNG from this repository.

Example:

```js
.setFaviconUrl('https://raw.githubusercontent.com/LoveTheCat/CatAppsAssets/master/images/favicons/LoveLog.png')
```

The asset must be a real PNG and must be safe to expose publicly. Application code remains in each application's own repository.

## Ownership

CatAppsAssets is the SSOT and public delivery surface for CatApps public static assets. CatAppsDoctor is a diagnostic/recovery application and must not be used as a general asset host.

### Asset integrity rules

- Binary assets must be structurally valid before they are committed or referenced by a CatApp. A filename extension and MIME type alone are not validation.
- PNG favicons must pass: PNG signature, IHDR parse, complete chunk-boundary walk, CRC validation for every chunk, and terminal IEND with no truncation. A malformed or truncated PNG is rejected even if some viewers can decode it.
- Canonical favicon profile: 64×64 px, PNG, 8-bit RGBA (color type 6), non-interlaced. Re-encoding is allowed to reach this profile, but visual content should not be changed merely for encoding normalization.
- For GAS favicons, verify the public raw URL returns the intended file over HTTPS before release. CatRegistry.png is the known-good reference asset for delivery-path diagnostics; it is not a substitute for validating a new asset.
- Asset replacement must preserve the original source separately when recovery is necessary; do not create cache-busting duplicate filenames as a substitute for integrity validation.
