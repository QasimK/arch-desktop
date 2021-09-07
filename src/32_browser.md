# Web Browser

It's unfortunate, but Firefox is all that's left... slowly dying...

```terminal
pacmatic -S --needed firefox-i18n-en-gb
```

We already set the environment variable:

```
MOZ_ENABLE_WAYLAND=1
```

## Default Config

Use a `user.js` file to create some about:config defaults.

This is a good starting point: <https://github.com/pyllyukko/user.js>

## Search engines

Use a `search.json.mozlz4` file to set your search engines.

Use <https://mycroftproject.com> to find search engines.

Use the <https://addons.mozilla.org/firefox/addon/mozlz4-edit/> plugin to modify the file if necessary.

## Suggested Addons

Privacy:

* uBlock Origin
* ClearURLs
* Smart Referer
* LocalCDN
* CanvasBlocker

Usability:

* Firefox Multi-Account Containers
* Temporary Containers
* Don't Fuck With Paste
* Drag-Select Link Text
* Privacy Pass
* Url to QrCode
* Page Translator Revised

Websites:

* SponsorBlock for YouTube
* Old Reddit Redirect
* Smart Amazon Smile

Apps:

* KeePassXC-Browser

Totally Optional:

* Feed Indicator
* Greasemonkey
* Stylus
