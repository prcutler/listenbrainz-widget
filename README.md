# ListenBrainz Now Playing Widget

A self-hosted "Now Playing" card that shows your current or most recent track from [ListenBrainz](https://listenbrainz.org). Designed to be hosted on GitHub pages and it embedded as an iframe on any website.

---

## Quick start

1. Fork or clone this repo
2. Set your username (see below)
3. Deploy to GitHub Pages (see below)
4. Embed the iframe on your site

---

## Setting your username

**Option A — hardcode it** (recommended for a personal widget)

Open `listenbrainz-now-playing.html` and find this line near the top of the `<script>` block:

```js
const DEFAULT_USERNAME = "";
```

Replace the empty string with your ListenBrainz username:

```js
const DEFAULT_USERNAME = "yourname";
```

**Option B — pass it in the URL**

Leave `DEFAULT_USERNAME` empty and append `?user=yourname` to the iframe `src`. Useful if you want to reuse one hosted file for multiple profiles:

```html
<iframe src="https://yourusername.github.io/listenbrainz-widget/listenbrainz-now-playing.html?user=yourname" ...></iframe>
```

If both are set, the `?user=` URL parameter wins.

---

## Matching the background color to your site

The widget background is controlled by two CSS variables near the top of the `<style>` block:

```css
/* Background colors — set these to match your site's background.
   --bg-0 should match your page's main background color.
   --bg-1 is used for the subtle gradient and should be slightly lighter. */
--bg-0: #1e2129;
--bg-1: #252b38;
```

Change `--bg-0` to your site's background color and `--bg-1` to a slightly lighter shade of the same color. If your site has a light background, use light values (e.g. `--bg-0: #f5f5f5`).

---

## Deploying to GitHub Pages

1. Push the file to a GitHub repository
2. Go to **Settings → Pages** in your repo
3. Under **Build and deployment**, set Source to **Deploy from a branch**
4. Set Branch to `main` and folder to `/ (root)`, then click **Save**
5. After ~1 minute your widget will be live at:

```
https://yourusername.github.io/your-repo-name/listenbrainz-now-playing.html
```

---

## Embedding the iframe

```html
<iframe
  src="https://yourusername.github.io/your-repo-name/listenbrainz-now-playing.html"
  width="460"
  height="180"
  style="border:none; border-radius:20px; overflow:hidden;"
  title="Now Playing on ListenBrainz"
  loading="lazy">
</iframe>
```

Sizing notes:
- The card is capped at **440px wide** — `460px` gives a little breathing room
- `180px` height fits the card with no scrollbar
- `border-radius` on the iframe clips the widget corners to match the card's rounded edges

---

## How it works

- Polls the [ListenBrainz API](https://listenbrainz.org/api/) every 20 seconds
- Shows **Now Playing** with an animated equalizer if a track is active
- Falls back to **Last Played** with a timestamp if nothing is currently playing
- Clicking the card opens your ListenBrainz profile in a new tab
- Polling pauses automatically when the tab or iframe is not visible

Assisted by Claude (I know, I know).
