# manishmajhimidackertech.github.io

Personal showcase site, served by GitHub Pages at
<https://manishmajhimidackertech.github.io/>.

It is a single static page (`index.html`, no build step) that links to my projects:

- [Tunnel Trouble 3D](https://github.com/manishmajhimidackertech/Tunnel-Arcade): endless tunnel flyer (Three.js PWA)
- [Hostile Horizon](https://github.com/manishmajhimidackertech/Hostile-Horizon): side-scrolling aerial combat (Three.js PWA)

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
