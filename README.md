# Terminal Bomberman

A classic Bomberman game that runs in your terminal. Pure Python, no dependencies.

## Play

```
python3 bomberman.py
```

Requires Python 3 and a terminal at least 30×16 characters (macOS/Linux; on Windows install `windows-curses` first).

## Controls

| Key | Action |
| --- | --- |
| Arrows / WASD | Move |
| Space | Drop bomb |
| P | Pause |
| R | Restart after game over |
| Q | Quit |

## Rules

- Blow up every enemy (`&&`), then find the exit door hidden under a brick (`[]`) to advance a level.
- Bombs explode after 2.5s; blasts stop at pillars (`##`), destroy the first brick they hit, and set off other bombs.
- Power-ups hide under bricks: `+B` extra bomb, `+F` longer blast, `+S` speed. Flames destroy exposed power-ups.
- You have 3 lives. Touching an enemy or a flame costs one.
