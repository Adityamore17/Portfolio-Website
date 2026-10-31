# Barricade Coach

A small web page that suggests your best move in 2-player Barricade (Quoridor rules: move your pawn one
square or place a two-square wall; first pawn to reach the far row wins). Open `index.html` in a browser
next to your game (split screen, pop-up view or Slide Over on a phone or tablet) and keep it in sync:

1. On your turn the coach shows the best move: a dashed yellow ring for a pawn step, or a yellow
   striped wall. Make that move in your game, then tap **I played it**.
2. On their turn, tap the square their pawn moved to. If they placed a wall, switch to **Wall**, tap
   the groove where it went, and tap again (or **Place wall**) to confirm.
3. If the coach and your game get out of step, use **Undo** or **Edit position** to fix the board.

**New game** sets the board size (5×5 to 11×11), walls per player, who moves first and how long the
coach thinks (0.5 to 8 seconds). The game is saved in the browser, so reloading keeps your place.

## How it picks moves

- Alpha-beta search with iterative deepening, running in a Web Worker so the page stays responsive.
- Positions are scored by the difference in shortest-path length to each goal row, plus the walls
  each player still has. The wall value (14 points, against 12 for one step) was tuned by self-play.
- At the first move every legal wall is considered. Deeper in the search, only walls that lengthen
  the opponent's shortest path are tried, which keeps it fast enough to look 6 to 8 turns ahead.

Everything is in the one `index.html` file with no build step or dependencies.
