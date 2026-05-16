# Neon Strike — PWA

A Progressive Web App version of the game. Once deployed to any HTTPS host,
users can install it to their home screen and play offline.

## What's in this folder

- `index.html` — the game itself (with PWA registration added)
- `manifest.json` — tells the phone how to install the app (name, icons, orientation)
- `sw.js` — service worker that caches assets for offline play
- `icon-192.png`, `icon-512.png`, `icon-180.png` — app icons
- `favicon.png` — browser tab icon

## Deploying — three easy options

PWAs **must be served over HTTPS** (or `localhost` for testing). All the
options below give you HTTPS for free.

### Option 1: Netlify Drop (fastest, no account needed for testing)

1. Go to https://app.netlify.com/drop
2. Drag this entire folder onto the page
3. You'll get a URL like `https://random-name.netlify.app` in seconds
4. Open the URL on your phone

### Option 2: GitHub Pages (good for ongoing development)

1. Create a new GitHub repo, upload these files
2. Settings → Pages → Source: deploy from `main` branch, `/` root
3. Your site will be at `https://<username>.github.io/<repo-name>/`

### Option 3: Cloudflare Pages or Vercel

Sign up, connect a GitHub repo, push, done. Both have generous free tiers.

## Installing on your phone

### Android (Chrome)
1. Open the deployed URL
2. Chrome will show an "Install app" prompt at the bottom — tap it.
   Or: tap the three-dot menu → "Install app" / "Add to Home screen"
3. Game appears on home screen like any other app

### iOS (Safari)
1. Open the deployed URL in Safari (must be Safari, not Chrome)
2. Tap the Share button (square with arrow up)
3. Scroll down and tap "Add to Home Screen"
4. Confirm. Icon appears on home screen.

> **iOS note:** Web Audio API respects the physical Silent/Mute switch.
> If you hear no sound, flip the side switch off.

## Testing offline

After installing, turn on airplane mode and re-open the app. It should
launch and run normally — that's the service worker at work.

## When you update the game

If you change `index.html`, increment the cache version in `sw.js`:

```js
const CACHE_VERSION = 'neon-strike-v2';  // was v1
```

This forces the service worker to fetch fresh files instead of serving
stale cached ones. Without this, returning users would see the old version
indefinitely.

## What's NOT in here (but might be nice later)

- **High score persistence** — add via `localStorage`
- **Haptic feedback on hits** — `navigator.vibrate(50)` works on most phones
- **Analytics** — Plausible or simple-analytics if you want install counts
- **App store distribution** — wrap this folder in Capacitor to ship to
  Apple App Store / Google Play (see Capacitor docs)
