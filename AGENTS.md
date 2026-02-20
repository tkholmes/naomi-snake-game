# Naomi's Neon Snake - Design Decisions

## Architecture
- Single file: `snake.html` containing all HTML, CSS, and JS
- HTML5 Canvas for game rendering
- Web Audio API for sound effects (no external audio files)
- No external dependencies or frameworks
- All game logic wrapped in an IIFE to avoid global scope pollution

## Game Rules
- Snake starts at center, moving right, length 3
- Food is 3x3 grid cells; spawns at random position (never overlapping the snake)
- Snake grows by 2 segments per food eaten (1 from not popping tail + 1 duplicated tail)
- Win condition: eat 30 pieces of food
- Lose conditions: hit wall boundary OR hit own body
- Direction input is buffered (nextDir) to prevent reversing into self

## Board Size
- 30x30 grid (600x600px canvas)
- Grid cell size: 20px
- Subtle white grid lines (4% opacity) drawn on the board

## Difficulty Modes
- Easy: ~180ms tick interval
- Medium: ~120ms tick interval (default)
- Hard: ~72ms tick interval
- Difficulty can be changed mid-game; the tick interval restarts immediately at the new speed

## Controls
- Arrow keys AND WASD for snake movement
- Enter or Space to start game
- P or Escape to pause/unpause
- R to restart after game over
- 1 / 2 / 3 to switch difficulty (Easy / Medium / Hard) mid-game
- All actions also accessible via clickable buttons

## Sound Effects
- Chime on food eaten: two-oscillator ascending sine tone (~350ms, 523Hz→784Hz and 659Hz→1047Hz)
- Thud on game over: triangle wave dropping from 120Hz→40Hz (~300ms, dampened)
- AudioContext resumed on first user interaction

## UI/UX
- Clean, modern look with dark background (#1a1a2e), dark blue canvas (#0f3460)
- Teal (#4ecca3) accent color used for title, score, canvas border, and active buttons
- Title has teal glow text-shadow
- Snake: 9-color neon rainbow (pink, red-orange, orange, yellow, green, cyan, blue, purple, magenta) smoothly interpolated along the body, animated to flow through the snake each tick (offset advances by 2 per tick, spread of 3 per segment)
- All snake segments have a neon glow matching their current rainbow color (head glow: 12px blur, body glow: 6px blur)
- Snake segments drawn with 1px inset and dark blue (#0f3460) borders
- Sparkles: 4-pointed star particles in cyan/green/yellow/purple/pink, 2-3 spawned at the tail each tick, fade out with gentle upward drift
- Food: large cupcake emoji (🧁) rendered at 50px font size, centered across 3x3 grid cells
- Motivational message on food eat: pool of 11 messages including "Dad Loves You!", displayed with fade-in + upward float animation (~1.4s)
- Game Over overlay: semi-transparent dark background (88% opacity), red title for loss, teal for win, clickable to restart
- Score display tracking food eaten (0/30)

## Visual Layout
- Centered game board (600x600px) with 3px teal border
- Title, score, and difficulty selector above the board
- Controls hint bar below the board (small gray text)
- Toast messages appear at 30% from top, centered horizontally
- Game Over overlay rendered on top of the canvas with restart hint
