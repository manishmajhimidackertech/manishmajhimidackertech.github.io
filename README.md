# manishmajhimidackertech.github.io

Personal showcase site, served by GitHub Pages at
<https://manishmajhimidackertech.github.io/>.

It is a single static page (`index.html`, no build step) that shows off my browser games, with real gameplay
screenshots, a feature rundown and a "What's new" section for each:

- [Tunnel Arcade](https://github.com/manishmajhimidackertech/Tunnel-Arcade): endless 3D
  tunnel flyer with slow-motion pickups and tilt steering (Three.js PWA)
- [Hostile Horizon](https://github.com/manishmajhimidackertech/Hostile-Horizon): side-scrolling aerial combat with eight
  maps, six aircraft and seven bosses (Three.js PWA)

## Files

```
index.html             the whole page: markup, CSS and a few lines of JS for the screenshot galleries
assets/favicon.svg     site icon
assets/tunnel-arcade.svg, hostile-horizon.svg
                       app icons copied from each game repo
assets/shots/          gameplay screenshots as WebP, full size (1280x720) and -640 thumbnails
assets/og-image.jpg    1200x630 link preview for social media and chat apps
```

To add or swap a screenshot, save a 1280x720 WebP as `assets/shots/<name>.webp` plus a 640x360
`assets/shots/<name>-640.webp`, then add a thumbnail button with `data-shot="<name>"` to the game's gallery in
`index.html`.

## Publishing

1. **Settings → Pages → Build and deployment → Source: Deploy from a branch**, then pick the branch that
   holds `index.html` and the `/ (root)` folder.
2. The site goes live at `https://manishmajhimidackertech.github.io/` within a minute or two.

`.nojekyll` turns off Jekyll processing, so files are served exactly as they are.

## Making the "Play" links work

The Play buttons point to each game's own project site
(`https://manishmajhimidackertech.github.io/<Repo>/`). Each game repo already has a Pages workflow; in
each one go to **Settings → Pages → Source: GitHub Actions**, then push to `main` (or run the workflow
manually) to deploy it.
