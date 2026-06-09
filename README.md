# ListenBrainz Widgets

Two self-hosted widgets for your [ListenBrainz](https://listenbrainz.org) listening history:
a live **Now Playing** card you can embed on your site, and a shareable **Weekly Top 5 Albums**
image for social media. Both are single HTML files with no build step — set your username,
deploy to GitHub Pages, and you're done. A landing page (`index.html`) links to both.

---

## Now Playing Widget

`listenbrainz-now-playing.html` — an auto-refreshing card that shows your current or most
recent track, with album art and an animated equalizer. Designed to be embedded as an iframe
on any website.

### Setting your username

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

Leave `DEFAULT_USERNAME` empty and append `?user=yourname` to the iframe `src`. Useful if you
want to reuse one hosted file for multiple profiles:

```html
<iframe src="https://yourusername.github.io/listenbrainz-widget/listenbrainz-now-playing.html?user=yourname" ...></iframe>
```

If both are set, the `?user=` URL parameter wins.

### Matching the background color to your site

The widget background is controlled by two CSS variables near the top of the `<style>` block:

```css
/* Background colors — set these to match your site's background.
   --bg-0 should match your page's main background color.
   --bg-1 is used for the subtle gradient and should be slightly lighter. */
--bg-0: #1e2129;
--bg-1: #252b38;
```

Change `--bg-0` to your site's background color and `--bg-1` to a slightly lighter shade of the
same color. If your site has a light background, use light values (e.g. `--bg-0: #f5f5f5`).

### Deploying to GitHub Pages

1. Push the files to a GitHub repository
2. Go to **Settings → Pages** in your repo
3. Under **Build and deployment**, set Source to **Deploy from a branch**
4. Set Branch to `main` and folder to `/ (root)`, then click **Save**
5. After ~1 minute your widgets will be live at `https://yourusername.github.io/your-repo-name/`

### Embedding the iframe

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

### How it works

- Polls the [ListenBrainz API](https://listenbrainz.org/api/) every 20 seconds
- Shows **Now Playing** with an animated equalizer if a track is active
- Falls back to **Last Played** with a timestamp if nothing is currently playing
- Clicking the card opens your ListenBrainz profile in a new tab
- Polling pauses automatically when the tab or iframe is not visible

---

## Weekly Top 5 Albums

`weekly-top5.html` — generates a shareable **1200×1200 PNG** of your top 5 most-played albums
for the week, complete with album cover art. Open the page, wait for your data to load, then
click **Download PNG**.

### Generating an image

Once deployed (see [Deploying to GitHub Pages](#deploying-to-github-pages) above), open:

```
https://yourusername.github.io/your-repo-name/weekly-top5.html
```

Wait for your top 5 albums to load with their cover art, then click **Download PNG**. The image
is rendered at 2× resolution and ready to post to Instagram, Mastodon, Bluesky, and more.

### Username

The generator uses the same `DEFAULT_USERNAME` hardcode and `?user=yourname` URL override as the
Now Playing widget. It fetches data from the ListenBrainz weekly stats API and pre-loads all album
art before rendering so the exported PNG is crisp and complete.
