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
