# TANKS — Prototype 0.2

A one-pixel-per-click browser game about building a recursive tank.

## Play

Open `index.html` in a browser, or upload this ZIP to itch.io as an HTML5 game. It does not need a build step, a server, dependencies, or an account to play.

Each click or tap adds one pixel. Six pixels make a tank; six tanks make a larger tank. Completing a level zooms the camera out. The **Reset progress** button clears the active tank after confirmation, for testing. You can click the field, tap **PLACE PIXEL**, or press Space.

## Experiments

[Genetic Warfare — Gene Lab](genetic-warfare/) is a separate 3 × 3 pattern experiment. Its [draft GDD](genetic-warfare/GDD.md) records the 126 four-cell genes, provisional +1/−1 assignments, and the design questions still open. It does not alter TANKS.

## Save data

The current tank and saved tank library are stored in the browser's `localStorage`. An existing save from Prototype 0.1 becomes the **Working tank** automatically. Progress restores when the game is reopened at the same origin in the same browser profile. It does not sync between devices or different sites, and clearing site data removes it. The in-game status indicates if browser storage is unavailable.

## Tank library

Select **Save a copy to library**, name the tank, and it becomes the active tank. Each subsequent pixel updates that saved tank automatically. Select **Open** on another saved tank or the Working tank to resume it. Switching tanks preserves each tank’s progress. Reset clears the active tank after a warning; if it is a saved tank, its library entry is reset too.

## To do (ideas for later)

The current prototype deliberately stays at one pixel per click, one recursive six-part silhouette, and the goal of building the largest tank. These are ideas to evaluate after playtesting, not promised features:

- [ ] Try distinct tank silhouettes at higher levels while keeping the six-to-one recursive construction.
- [ ] Explore progression that eventually lets one action build a complete lower-level tank instead of one pixel.
- [ ] Explore automation and upgrades for building faster.
- [ ] Consider a prestige loop after the basic progression has a satisfying pace.
- [ ] Add more feedback to pixel placement and tank completion: animation, sound, and camera movement.
- [ ] Explore objectives beyond reaching the highest tank level; decide later whether combat belongs in the game.

## GitHub Pages

Put `index.html` at the repository root and enable GitHub Pages from the main branch root. The README is optional for hosting.

## itch.io

Upload this ZIP as a browser-playable HTML5 game. `index.html` is already at the ZIP root. A page viewport around 960 × 640 works well on desktop; the game also adapts to phones.
