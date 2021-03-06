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
- <kbd>L1</kbd>, <kbd>L2</kbd> Used for storing the X and Y positions of tiles that need revealing
- <kbd>⌊θ</kbd> Used by dispmenu to create menus

## How it works

### New Game

During setup, the <kbd>[G]</kbd> variable is used to store the location of the bombs and is 28x11 for convenience. <kbd>[H]</kbd> is used to store the tile scores of each tile (0-8) <kbd>N</kbd> is used to store the difficulty.

Setup happens in two stages:

- Placing bombs
- Calculating tile scores (0-8)

#### Placing Bombs

<kbd>N</kbd> bombs are placed randomly on <kbd>[G]</kbd>. Since <kbd>[G]</kbd> is actually 28x11 and the game screen is only 26x9, bombs are actually placed from 2..27 on X and 2..10 on Y. There is no checking if bombs overlap eachother, on large bomb counts it is likely that less than <kbd>N</kbd> bombs will be placed because some overlap eachother.

#### Calculating tile scores

This is usually the longest section of making a new game (unless a very high number of bombs were requested to be placed). In this section, the game loops over every tile (1..26 and 1..9), calculates its score, and stores it to <kbd>[H]</kbd>. Score calculation is easy because the <kbd>[G]</kbd> map of bombs is larger than the game board. For each tile on the game board, a score is created as the result of adding all 8 tiles around it from <kbd>[G]</kbd>. This section also counts how many bombs actually got placed into <kbd>W</kbd>.

### Resume Game

Resuming a game loops over all the revealed tiles <kbd>[G]</kbd> and shows them on the screen.

### Playing the game

Each loop step, the game waits for a key to be pressed. Based on the key, it does a different thing:

#### Reveal a tile

A tile is revealed by moving its real value at <kbd>S</kbd>, <kbd>T</kbd> from <kbd>[H]</kbd> to <kbd>[G]</kbd>. If this tile is a blank space, space clearing mode is activated.

#### Move the cursor

Before moving the cursor, the current tile at <kbd>S</kbd>, <kbd>T</kbd> is drawn from <kbd>[G]</kbd> to the screen. Then, based on what key was pressed, the cursor is moved. The new cursor is drawn at the new <kbd>S</kbd>, <kbd>T</kbd> position.

#### Add a flag

A flag is added at the cursor, or removed if it was already added.





#### Space clearing mode

Space clearing mode loops over every tile in (L1, L2) and reveals a 3x3 around it.

#### Winning

When the number of tiles remaining equals the number of bombs, you win.

#### Losing

When you reveal a bomb, you lose.


### Tile IDs

Tile IDs are used to store tiles in their matrices:
- `-3`: `*`: A bomb.
- `-2`: `+`: A flag.
- `-1`: `·`: A tile that is not yet uncovered.
- `0`: `•`: A tile which is in the process of being uncovered in space clearing mode.
- `1`: `1`: A tile with 1 bomb around it.
- `2`: `2`: A tile with 2 bombs around it.
- `3`: `3`: A tile with 3 bombs around it.
- `4`: `4`: A tile with 4 bombs around it.
- `5`: `5`: A tile with 5 bombs around it.
- `6`: `6`: A tile with 6 bombs around it.
- `7`: `7`: A tile with 7 bombs around it.
- `8`: `8`: A tile with 8 bombs around it.
- `9`: `9`: Unused. If I were thinking while making this program, this could've been used for the bomb.
- `10`: ` `: A blank tile.

Tiles are drawn to the screen from <kbd>Str1</kbd>, where `-3` is the first character of the string. Sometimes, tiles are drawn directly from a "string" value, making changing Str1 not a reliable way to re-skin tisweeper.
