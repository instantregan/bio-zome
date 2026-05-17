# bio-zome — Claude context

A single-file HTML viewer for Bluesky photos (defaults to `@bioreconstruct.bsky.social`). The whole app is `index.html` — embedded CSS and vanilla JS, no build step, no dependencies, no server.

## Hard constraints — do not break these

- **One HTML file.** Everything lives in `index.html`. No splitting into JS/CSS files, no `<script src>` to external libs, no npm, no bundler. The pitch of the project is "double-click to use." A build step kills it.
- **Opens from `file://`.** The supported launch is double-clicking the file or a `file://` bookmark. No local server should be required. This works because Bluesky's public AppView (`public.api.bsky.app`) sends `Access-Control-Allow-Origin: *`, which accepts the `null` origin that `file://` pages send. Don't add features that break this (e.g. WebSockets, Service Workers requiring secure context, modules with bare specifiers).
- **No auth, no API keys.** Reads only — `app.bsky.feed.getAuthorFeed` and friends on `public.api.bsky.app`. If a feature would need a logged-in session, push back rather than building it.
- **No tracking, no analytics, no remote logging.** It's a viewer. localStorage is fine for per-handle position and the current handle.

## What it does

`getAuthorFeed?actor=<handle>&limit=100&filter=posts_with_media`, paginating via cursor. Flattens each post's image array so a 4-image post becomes 4 nav steps. Renders `record.text` as the caption, plus per-image `alt` text quoted underneath. `embed.images#view` and `embed.recordWithMedia#view → media.images#view` are both handled; videos and pure-text posts are filtered out.

## Editing

- All structure, style, and behavior is in `index.html`. Edit in place.
- Test by opening `index.html` directly in a browser (or `file://` bookmark). No reload daemon, no HMR — just refresh the tab. State persists in localStorage if you want to test resume behavior.
- Key map and progressive disclosure are in the `#help` strip at the bottom of the stage and the `keydown` handler. Keep them in sync when adding shortcuts.

## What to avoid suggesting

- Migrating to React / Vue / Svelte / any framework.
- A bundler or TypeScript step.
- A local dev server as the default launch method (we tried it; the friction made the user ask for the simpler path).
- Scraping HTML pages instead of using the public API.
- Anything that requires the user to log into Bluesky.

If a feature seems to genuinely require any of the above, raise it as a tradeoff before implementing — not a default.
