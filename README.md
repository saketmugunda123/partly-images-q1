# Partly Images case, Q1: image-mix simulator

One self-contained web page (`index.html`, no dependencies, no data leaves the browser). It re-runs the image-mix decision for 71.1M SKUs whenever a slider moves. Every result is shown for original equipment (OE) and aftermarket separately as well as in total.

## Put it on GitHub Pages

1. On github.com, create a new **public** repository, for example `partly-images-q1`. (On a free account, Pages only works from public repositories, and a Pages site is public on the internet either way.)
2. In the repository: **Add file → Upload files**, drop in `index.html` (and this README if you like), **Commit changes**.
3. **Settings → Pages**. Under "Build and deployment", set Source to **Deploy from a branch**, choose branch **main** and folder **/(root)**, **Save**.
4. After a minute or two the page is live at `https://YOUR-USERNAME.github.io/partly-images-q1/`. The address is shown at the top of Settings → Pages.

To link straight to a particular view, set the sliders and copy the address from the browser's address bar, which updates as they move. Examples (add to the end of the page address): `#reach=0.5&uplift=50` for the cautious case; `#oe=0.5&am=5` for low OE and high aftermarket share.

## What is adjustable

The three things the case does not give (the second has one slider for OE and one for aftermarket):

1. **Sales concentration**: how much of each category's sales the top 20% of SKUs make (56% to 98%; base 80%).
2. **Share of the market through Partly's customers**, set separately for original equipment (OE) and aftermarket (0.1% to 10% each; base 1.5% for both).
3. **Uplift strength**: how much of the case's sales uplift to believe (25% to 100%; base 100%).

Everything else is held at the base case: 2% take on the extra sales an image creates, 3-year image life, the case's costs and uplifts, "part type" in Option 4 read as the five categories, no cap on shoots. `src/engine.js` still accepts those as parameters if you want them back.

## How close it is to the full model

The page runs a lighter version of the simulation behind the written answer: a stratified sample of about 0.8 million SKUs, with brands buying Option 4 according to a brand-size distribution. `src/validate.js` compares it with saved runs of the full model. On the 13 runs that only move these settings, every image share is within 0.7 percentage points and cost within 3%. Base case here: cost $336M, 3-year revenue $5.09B, return 14.1x (full model: $334M, $5.09B, 14.2x).

## Rebuild

    cd src
    node validate.js   # compare with the full model, writes validation.json
    node build.js      # writes ../index.html

`src/engine.js` is the model, `src/template.html` the page.
