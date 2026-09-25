# TANKS / Genetic Warfare — prototype rulebook 0.3

**Genetic Warfare** is a separate experimental play mode under `modules/genetic-warfare/`. The basic TANKS game at the repository root keeps its own six-pixel construction and tank library. Neither mode changes the other's progress.

## The tank and its four segments

A tank is displayed on a 3 × 3 grid. Four overlapping 2 × 2 **source segments** sit at the top left, top right, bottom left, and bottom right. Each source segment has exactly three filled cells, so it is described by its one empty corner. Its four choices are top-left empty, top-right empty, bottom-left empty, and bottom-right empty.

The four sources are **overlaid by union**: a cell is visible if any source fills it. Mutating one source leaves the other three source choices unchanged, though their shared cells may change the resulting visible windows. In particular, overlap can turn a visible 2 × 2 window into a full square. A source is never mutated directly to a full square. Because every visible window contains its own three-filled source, the final grid never contains an unlisted window pattern. The union contains between five and nine filled cells; that number is the tank's build cost in clicks.

## Visible-window trait rulebook

Each of the four **visible** 2 × 2 windows is scored after all four sources are overlaid:

| Visible window | Opening trait points |
| --- | ---: |
| Top-left cell empty | 0 |
| Top-right cell empty | +1 |
| Bottom-right cell empty | −1 |
| Bottom-left cell empty | +2 |
| All four cells filled | −2 |

A completed tank's award is the sum of its four visible-window values under **that generation's assignment**. The basic six-cell tank (`.#./###/#.#`) has opening values **0, +1, −1, +2**, so its award is **+2**. Under the opening assignment, rotations, a seven-cell H, and an eight-cell donut are among the other +2 outcomes. Four source choices per quadrant produce 4⁴ = **256 blueprints** but only **35 distinct visible shapes**.

### Fortune wheel

Generations 1 and 2 use the fixed opening assignment above, guaranteeing +2 each. When the player chooses to continue after generation 2 or any later completion, the next generation receives both its one-segment mutation and a **fresh uniform shuffle** of the five distinct values **−2, −1, 0, +1, +2** across the five visible-window pattern types. Each value is used once in the mapping. The full square participates in the wheel and can therefore be beneficial in a later generation. Two windows of the same pattern type receive the same value; uniqueness is by **pattern type**, not by window position.

The wheel is revealed after committing to continue and remains fixed for that generation, including across a reload. It does not change an already completed award. The mutation and wheel are sampled independently. The wheel raises the first mutated generation's chance of a positive completion award from 1/12 to about 41.1%; it also allows larger gains and losses. This is an experiment in variance and cash-out timing, not a claim that a shape has a permanently good or bad trait.

## Generation loop

1. A new run begins at generation 1 with the basic blueprint. Each click fills one occupied cell in the current 3 × 3 shape. Clicking a cell outside the blueprint does nothing. The **Fill next cell** button offers the same one-cell action in row order.
2. A partial tank awards **no trait points**. Only when all its occupied cells are filled does the tank award its four-window score **once**. Add that award to the run's running total.
3. Generation 2 is also guaranteed to use the basic blueprint. Its +2 award brings the opening run total to **+4**, not +12. The earlier child-sum model is superseded. A completed tank is represented by one filled slot at the next scale, but filling a slot does not separately award the previous tank's points.
4. After every completion, choose **Bank score & end run** or **Build next generation**. The choice to continue commits to completing that next tank before banking again.
5. Starting with generation 3, continuing copies the previous generation's four-source blueprint and switches exactly one randomly selected quadrant to one of its other three three-filled choices. Both selections are uniform. Independently, the fortune wheel shuffles the five trait values. The new blueprint and wheel assignment remain fixed for that generation's build. The visible union determines its 5–9 occupied cells and the visible-window patterns; that generation's wheel determines their completion award. Repeat once per subsequent generation.
6. Banking records the current completed generation and running trait total as an immutable high score and ends that run. It cannot be resumed. A new run begins with the two guaranteed basic generations. Restarting an unbanked run discards its unbanked score; it does not erase banked scores.

For example, a generation 3 mutation can yield `.#./###/###`. Its seven cells take seven clicks. Under the **opening** assignment its visible windows would score 0, +1, −2, −2, or **−3**; with the fortune wheel, its actual award depends on the revealed mapping for generation 3. None of its clicks awards points individually.

## Prototype interface and persistence

The module shows the active 3 × 3 build, fortune wheel mapping, four source segments, four scored visible windows, pending completion award, running total, recent generations, and banked high scores. The player can fill cells, continue after completion, cash out, and start a fresh run. The active run and banked scores restore from browser storage on the same origin. High scores banked under the previous fixed rulebook remain visible in a separately labeled list; they are not mixed into wheel rankings. Its previous unfinished run remains stored but is not resumed under the new rules. The earlier Gene Lab's editable 126-gene catalog is superseded; its old storage is left untouched and unused. The legacy `/genetic-warfare/` URL forwards to this module.

## Acceptance checks

- The first two completed tanks each award +2, giving a running total of +4.
- No partial click changes the trait total; completion awards exactly once.
- Every mutation changes exactly one source quadrant to a different three-filled choice, never to a full square.
- Every visible window after overlay is one of the five rulebook states; 5–9 slots are required according to the visible union.
- Continuing after generation 2 produces one changed source and a permutation of all five values; the wheel assignment persists through build and reload.
- A repeated visible pattern uses the same wheel value in each window, including the full square.
- Banking is available after completion, stores the score, ends the run, and cannot reopen it for construction.
- Reloading restores an unfinished or completed run and its banked scores; it does not affect basic TANKS saves.

## Open design work

Playtest whether the larger swings and near-even odds create meaningful bank-or-continue decisions, and whether a mapping that changes each generation leaves enough value in the blueprint itself. Combat, named traits, upgrades, automation, and additional progression are outside this prototype.
