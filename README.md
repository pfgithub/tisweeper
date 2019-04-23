# tisweeper
A minesweeper game for the TI84 calculator or any calculator with TIBasic support that is 10x26 in screen size.

## Variables

tisweeper uses the variables

### Needed for resuming a game

- <kbd>[G]</kbd> For storing the state of the game
- <kbd>[H]</kbd> For storing the location of bombs
- <kbd>R</kbd> For storing how many tiles are remaining
- <kbd>W</kbd> For storing how many bombs are on the map

### Temporary

- <kbd>Str1</kbd> For storing the set of icons a tile might have
- <kbd>X</kbd>, <kbd>Y</kbd>, <kbd>Z</kbd>, <kbd>Θ</kbd> Temporary variables for loops
- <kbd>I</kbd>, <kbd>J</kbd>, <kbd>K</kbd>, <kbd>L</kbd>, <kbd>P</kbd> Temporary variables for clearing large areas
- <kbd>M</kbd>, <kbd>N</kbd> Temporary variable used as needed
- <kbd>K</kbd> The last key that was pressed
- <kbd>S</kbd>, <kbd>T</kbd> For storing the location of the cursor

## How it works

### New Game [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L6-L87)

During setup, the <kbd>[G]</kbd> variable is used to store the location of the bombs and is 28x11 for convenience [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L37). <kbd>[H]</kbd> is used to store the tile scores of each tile (0-8) [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L41) <kbd>N</kbd> is used to store the difficulty [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L12).

Setup happens in two stages:

- Placing bombs [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L44-L54)
- Calculating tile scores (0-8) [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L56-L80)

#### Placing Bombs [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L44-L54)

<kbd>N</kbd> bombs are placed randomly on <kbd>[G]</kbd>. Since <kbd>[G]</kbd> is actually 28x11 and the game screen is only 26x9, bombs are actually placed from 2..27 on X and 2..10 on Y [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L48-L49). There is no checking if bombs overlap eachother, on large bomb counts it is likely that less than <kbd>N</kbd> bombs will be placed because some overlap eachother.

#### Calculating tile scores [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L56-L80)

This is usually the longest section of making a new game (unless a very high number of bombs were requested to be placed). In this section, the game loops over every tile (1..26 and 1..9), calculates its score, and stores it to <kbd>[H]</kbd> [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L56-L80). Score calculation is easy because the <kbd>[G]</kbd> map of bombs is larger than the game board. For each tile on the game board, a score is created as the result of adding all 8 tiles around it from <kbd>[G]</kbd> [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L62-L77). This section also counts how many bombs actually got placed into <kbd>W</kbd> [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L65).

### Resume Game [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L88-L111)

Resuming a game loops over all the revealed tiles <kbd>[G]</kbd> and shows them on the screen.

### Playing the game [`<>`](https://github.com/pfgithub/tisweeper/blob/4bbd8f9b230cedfd980abc7bd6239688e45f8121/tisweeper#L112-L233)



#### Winning

When the number of tiles remaining equals the number of bombs, you win.

#### Losing

When you reveal a bomb, you lose.
