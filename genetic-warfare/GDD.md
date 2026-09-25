# Genetic Warfare — design document, draft 0.1

This is a separate experiment beside **TANKS**. Its initial purpose is to test whether tiny spatial patterns can form an interesting system of inherited advantages and disadvantages. It does not change the existing tank clicker.

## Core rule established so far

A **gene** is a 3 × 3 grid with exactly four filled cells. The four cells have no placement order. Each position-specific gene has a value of either **+1 trait point** or **−1 trait point**.

There are **C(9, 4) = 126** possible genes. In this draft, a rotated or mirrored pattern is a separate gene because its occupied grid positions differ. If orientations should be equivalent, the catalog would contain 34 rotation classes or 23 rotation-and-mirror classes instead. Only 36 of the 126 raw patterns are connected through shared edges; disconnected patterns remain valid for now.

The word *trait* is deliberately generic. We have not decided whether points contribute to one score or to named attributes such as armor, mobility, firepower, or stability. A +1/−1 assignment is data attached to a gene, not a claim that a shape is inherently good or bad.

## Prototype 0.1: Gene Lab

This is a design sandbox, not yet a combat game.

1. The player clicks cells in a 3 × 3 grid. A fifth cell cannot be filled.
2. At four filled cells, the lab identifies that exact pattern in a catalog of 126.
3. Every catalog entry has a +1 or −1 assignment. The initial catalog alternates signs by its stable pattern index, yielding 63 of each. This is a neutral placeholder, **not** a final balance rule.
4. The player can change an entry's sign to explore the mapping. Overrides persist in the same browser on this origin.
5. The catalog can reopen any gene for inspection. It shows the number of positive and negative assignments.

A pattern's stable ID is its nine-bit occupancy mask, read row by row. The displayed catalog number is its position among the 126 masks in ascending order. The mask is the identity; the catalog number is a convenient label.

### Prototype acceptance criteria

- Exactly 126 distinct four-cell patterns appear, once each.
- Selecting four cells resolves the same gene regardless of click order.
- A fifth filled cell is refused without changing the current gene.
- Every entry has exactly one sign; changing one entry does not change any other.
- Overrides survive a reload in the same browser.
- TANKS remains available at the repository root; the lab lives at `/genetic-warfare/`.

## Possible game loop, not designed yet

A later game might combine genes into a unit genome, create variation through mutation or inheritance, and then test units in a conflict. Those actions need rules before they become features. In particular, we need to decide what a genome is, how many genes it contains, how multiple points combine, what resources or choices the player controls, and what constitutes victory.

## Open design decisions

| Question | Current prototype choice | Alternatives to test |
| --- | --- | --- |
| Do orientation and reflection matter? | All 126 position-specific patterns are distinct. | Merge rotations, or merge rotations and mirrors. |
| Must the four cells be connected? | No. | Require edge connectivity, leaving 36 raw patterns. |
| How is a gene's sign assigned? | Editable catalog seeded with 63 positive and 63 negative entries. | Curated signs, geometry-based rules, or seeded generation. |
| Which trait receives the point? | One abstract trait point. | Named traits; a gene could also choose both a trait and sign. |
| How are genes combined? | Not yet specified. | Fixed genome slots, layered grids, or inheritance from parent units. |
| What does warfare mean? | No conflict system yet. | Simulated encounters, tactical decisions, or population-level competition. |
| What is the player's objective? | Explore and evaluate the gene catalog. | Breed for a target, win encounters, or sustain a lineage. |

## Next design pass

Choose the trait vocabulary and the composition rule first. Then define how players acquire or mutate genes and what a +1 or −1 actually changes. Once these rules exist, a small encounter can test whether the spatial genetics influence meaningful decisions.
