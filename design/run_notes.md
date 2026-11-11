# Task 9 run notes

Each run was started from the project folder with `cargo run`, feeding the answers on
stdin: menu option `6`, the pattern number, the number of generations, one empty line
per "Press Enter", then `0` to quit the main menu. For example, the blinker run:

```
{ printf "6\n1\n10\n"; for i in $(seq 10); do echo; done; echo 0; } | cargo run -q
```

Every run printed generations 0 through N (11 grids for 10 generations, 31 for 30) and
"Press Enter for the next generation." exactly N times, never after the last grid.

## Blinker, 10 generations

Alternates every generation between a horizontal line (4,9) (4,10) (4,11) on even
generations and a vertical line (3,10) (4,10) (5,10) on odd generations. Population
stays 3. Generation 10 matches generation 0.

## Block, 10 generations

Never changes: (4,10) (4,11) (5,10) (5,11) in all 11 grids, population 4.

## Glider, 10 generations

Travels down and to the right, population 5 throughout. Every four generations the
same shape is back, moved one row down and one column right: generation 4 is
(2,3) (3,4) (4,2) (4,3) (4,4), generation 8 is (3,4) (4,5) (5,3) (5,4) (5,5).

## Glider, 30 generations: what happens at the bottom edge

The glider keeps its 5 cells through generation 24, when it is sitting on the
bottom row (row 9):

Generation 24, population 5
```
....................
....................
....................
....................
....................
....................
....................
........#...........
.........#..........
.......###..........
```

The grid does not wrap, so the cells it would need below row 9 are never born. It
falls apart:

- Generation 25: population 4, (8,7) (8,9) (9,8) (9,9)
- Generation 26: population 3, (8,9) (9,8) (9,9)
- Generation 27: population 4, a 2×2 block at (8,8) (8,9) (9,8) (9,9)

From generation 27 on it is a still block in the bottom rows, and it stays the same
through generation 30:

Generation 30, population 4
```
....................
....................
....................
....................
....................
....................
....................
....................
........##..........
........##..........
```

That is the expected result of a grid that does not wrap, not a bug.
