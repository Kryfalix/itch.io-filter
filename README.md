# itch-filter

<img alt="Static Badge" src="https://img.shields.io/badge/ANTI-AI-SLOP">

A small Chrome extension that filters game listings on itch.io by keyword.

I got tired of scrolling past things I never click on, so this hides them from the browse, search, tag and jam pages. Nothing fancy, no account, no server. It just looks at each game card and decides whether to show it.

## Install

It's not on the Chrome Web Store (yet), so for now:

1. Download or clone this repo.
2. Go to `chrome://extensions` and turn on Developer mode (top right).
3. Click "Load unpacked" and pick the project folder.
4. Open itch.io. The icon should show up in your toolbar.

If you update the files later, hit the reload button on the extension card.

## Using it

Click the toolbar icon. You get a few options:

- **Enabled** turns the whole thing on or off.
- **Set A / Set B** are two built-in keyword sets. Toggle each one separately.
- **Mode** is either Hide (the card disappears) or Blur (it's blurred until you hover over it).
- **Custom** is a collapsed section where you can add your own keywords, one per line. These always apply while the extension is enabled.

The small number next to the title is how many cards got filtered on the current page.

## How it works

A content script runs on itch.io pages and checks every `.game_cell` element. It looks at the title, the short description and the genre label, then matches them against the keyword lists. Matching is whole-word and case-insensitive, accents are ignored, and a trailing "s" is allowed, so `cat` also catches `cats`. A MutationObserver re-runs the check when new cards load, so infinite scroll works.

Settings are saved with `chrome.storage.sync`, so they follow you across Chrome profiles if sync is on.

## Limitations

- It only sees what's on the card. Tags that only appear on the game's own page aren't checked, so some games will slip through and a few might get hidden by mistake. Adding or removing custom keywords usually fixes it.
- If itch.io changes its markup, the card selector at the top of `content.js` will need updating.
- Only runs on `itch.io` and `*.itch.io`.

## Files

```
manifest.json   extension manifest (MV3)
content.js      filtering logic
popup.html      popup UI
popup.css
popup.js
icons/          toolbar and store icons
```

## Permissions

Just `storage` and access to itch.io. It doesn't collect, send or log anything.

## License

MIT. See `LICENSE` if I've added one yet, otherwise treat it as MIT anyway.
