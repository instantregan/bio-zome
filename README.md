# bio-zome

A one-file browser for [@bioreconstruct.bsky.social](https://bsky.app/profile/bioreconstruct.bsky.social)'s aerial photos — fullscreen image, caption pinned at top, arrow keys to fly through history.

Built because Bluesky's normal photo viewer hides the caption when you zoom in, which is a real pain when bio's captions are the whole point.

## Use it

1. Download `index.html`.
2. Double-click it.

That's it. Single file, no install, no build step, no server. Opens straight from disk in any modern browser.

## Keys

| Key | Action |
|-----|--------|
| ← / → | Previous / next photo |
| Space | Next |
| Home / End | Jump to newest / oldest |
| Z | Toggle 100% zoom (drag to pan) |
| C | Hide / show caption bar |
| F | Fullscreen |
| O | Open the original post on Bluesky |
| S | Change handle |

Mouse wheel also flips through photos when not zoomed.

## How it works

Hits Bluesky's public AT Protocol AppView (`public.api.bsky.app`) — `app.bsky.feed.getAuthorFeed` with `filter=posts_with_media`. No auth, no API key, just a static page making a CORS-friendly fetch. The viewer flattens posts-with-multiple-images into a flat list so every image is its own step.

Press `S` to point it at a different handle. The handle and your last position are remembered in localStorage per-handle.

## Credit

All photos belong to [@bioreconstruct.bsky.social](https://bsky.app/profile/bioreconstruct.bsky.social). This is just a viewer.

Built by Claude (Opus 4.7) for Regan in one go.
