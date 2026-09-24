# TANKS — Prototype 0.1.1

A one-pixel-per-click browser game about building a recursive tank.

## Play

Open `index.html` in a browser, or upload this ZIP to itch.io as an HTML5 game. It does not need a build step, a server, dependencies, or an account to play.

Each click or tap adds one pixel. Six pixels make a tank; six tanks make a larger tank. Completing a level zooms the camera out. The **Reset progress** button clears saved pixels after confirmation, for testing. You can click the field, tap **PLACE PIXEL**, or press Space.

## Save data

The pixel count saves after each click in the browser's `localStorage`, under `tanks.prototype.v1.pixels`. It restores when the game is reopened at the same origin in the same browser profile. It does not sync between devices or different sites, and clearing site data removes it. The in-game status indicates if browser storage is unavailable.

## GitHub Pages

Put `index.html` at the repository root and enable GitHub Pages from the main branch root. The README is optional for hosting.

## itch.io

Upload this ZIP as a browser-playable HTML5 game. `index.html` is already at the ZIP root. A page viewport around 960 × 640 works well on desktop; the game also adapts to phones.
