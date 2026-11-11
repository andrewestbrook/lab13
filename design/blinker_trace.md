# Blinker hand trace (Task 1)

Traced by hand before writing `next_generation`. Coordinates are `grid[row][col]`,
counting from 0. The grid is 10 rows × 20 columns and does not wrap, but this blinker
sits in the middle, so the edge never matters here. Only the 5×5 patch (rows 3–7,
columns 8–12) is shown; every cell outside it is dead and has 0 live neighbors, so it
stays dead.

Rules: a live cell with 2 or 3 live neighbors stays alive. A dead cell with exactly 3
live neighbors becomes alive. Every other cell is dead in the next generation.

Key: `#` = live, `.` = dead. In the "apply the rules" grids: `S` = live and survives,
`D` = live and dies, `B` = dead and is born, `.` = dead and stays dead.

## Generation 0 — vertical line

Live cells: (4,10), (5,10), (6,10).

```
          col  8  9 10 11 12
row 3          .  .  .  .  .
row 4          .  .  #  .  .
row 5          .  .  #  .  .
row 6          .  .  #  .  .
row 7          .  .  .  .  .
```

### Neighbor counts for generation 0

```
          col  8  9 10 11 12
row 3          0  1  1  1  0
row 4          0  2  1  2  0
row 5          0  3  2  3  0
row 6          0  2  1  2  0
row 7          0  1  1  1  0
```

### Apply the rules

```
          col  8  9 10 11 12
row 3          .  .  .  .  .
row 4          .  .  D  .  .
row 5          .  B  S  B  .
row 6          .  .  D  .  .
row 7          .  .  .  .  .
```

- (4,10) and (6,10), the ends of the line: 1 live neighbor each, so they **die**.
- (5,10), the middle: 2 live neighbors ((4,10) and (6,10)), so it **survives**.
- (5,9) and (5,11), beside the middle: 3 live neighbors each, so they are **born**.
- Every other dead cell has 0, 1, or 2 neighbors, so it stays dead.

## Generation 1 — horizontal line

Live cells: (5,9), (5,10), (5,11).

```
          col  8  9 10 11 12
row 3          .  .  .  .  .
row 4          .  .  .  .  .
row 5          .  #  #  #  .
row 6          .  .  .  .  .
row 7          .  .  .  .  .
```

### Neighbor counts for generation 1

```
          col  8  9 10 11 12
row 3          0  0  0  0  0
row 4          1  2  3  2  1
row 5          1  1  2  1  1
row 6          1  2  3  2  1
row 7          0  0  0  0  0
```

### Apply the rules

```
          col  8  9 10 11 12
row 3          .  .  .  .  .
row 4          .  .  B  .  .
row 5          .  D  S  D  .
row 6          .  .  B  .  .
row 7          .  .  .  .  .
```

- (5,9) and (5,11), the ends of the line: 1 live neighbor each, so they **die**.
- (5,10), the middle: 2 live neighbors ((5,9) and (5,11)), so it **survives**.
- (4,10) and (6,10), above and below the middle: 3 live neighbors each, so they are **born**.
- Every other dead cell has 0, 1, or 2 neighbors, so it stays dead.

## Generation 2 — vertical line again

Live cells: (4,10), (5,10), (6,10).

```
          col  8  9 10 11 12
row 3          .  .  .  .  .
row 4          .  .  #  .  .
row 5          .  .  #  .  .
row 6          .  .  #  .  .
row 7          .  .  .  .  .
```

Generation 2 is the same as generation 0, so the blinker has period 2. This is what
the instructor's `blinker_returns_after_two` test checks, and `next_generation` has to
agree with every grid on this page.
