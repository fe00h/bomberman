# Roadmap: known issues & ideas

Found during a code review. None of these crash the game on a normal terminal,
but they're good next steps if you want to contribute. Pick one and open a PR!

## Gameplay bugs

- [ ] **Dying regenerates the whole level.** `Game.tick()` calls `new_level()` on
  respawn, which builds a fresh map: killed enemies return, bricks come back, and
  new hidden power-ups are placed, while score and collected power-ups carry over.
  A player can die on purpose to farm points and upgrades.
  *Idea:* on death, reset only the player position, bombs and fire; keep the map.

- [ ] **Chained blasts pierce too many bricks.** In `Game.explode()`, bombs in a
  chain are processed one after another, so a later bomb's ray passes through a
  brick an earlier bomb just cleared and destroys the brick behind it.
  *Idea:* collect bricks to destroy during the chain and clear them at the end.

- [ ] **Game keeps running when the terminal is too small.** `draw()` shows a
  "resize" message but `main()` still calls `g.tick()`, so you can lose lives
  without seeing the board. *Idea:* auto-pause while the board can't be drawn.

## Display / input

- [ ] **HUD is wider than the advertised minimum.** The top line
  (`LV 1  LIVES 3  BOMBS 1  FIRE 1  SCORE 0`) needs ~40 columns but the size
  check only requires 30, so the score wraps and is hidden. Shorten the HUD or
  raise the minimum width (and update the README).

- [ ] **Possible startup crash on unusual terminals.** `curses.curs_set(0)` raises
  `curses.error` on terminals that can't hide the cursor. Wrap it in `try/except`.

- [ ] **Key order within a frame is lost.** `main()` always handles the bomb
  before the move, and keeps only the last direction pressed. Pressing Right then
  Space very quickly can drop the bomb on the old tile.

- [ ] **Speed power-up at max level.** Picking up `+S` at the speed cap still says
  "Speed up!" and awards points, and current speed isn't shown in the HUD.

## Code cleanup

- [ ] `Enemy.__init__` picks a direction with the global `random` that
  `new_level()` immediately overwrites, and `Enemy.alive` is never used.
- [ ] `draw()` calls `g.bomb_at()` twice per bomb cell, each a linear scan;
  build a `{(x, y): bomb}` dict once per frame instead.
- [ ] `dead_until` is used both as the respawn timer and the level-clear timer;
  split it into separate fields for clarity.

## Feature ideas

- [ ] Two-player local mode (WASD vs. arrows)
- [ ] Smarter enemies that chase the player on later levels
- [ ] High-score file saved between runs
