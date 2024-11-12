## Tech Stack
Using PixiJs (https://pixijs.com/8.x/guides) is a good choice for making the game. It is easy and fast to render 2d image assets realtime and it simplifies a lot of the heavy-coding for javascript. It seems to be deployable to multiple platforms as an actual app so it'll be a great tool to publish your game on something like the app store.

## Game Architecture
### Player
- `PlayerController` class
  - Represents the player circle
  - Handles player movement based on WASD input
  - Calculates player speed and acceleration based on inertia
  - Manages player energy/health
  - Detects collisions with enemies and the lava border
- `PlayerPhysics` class
  - Calculates player movement and momentum
  - Applies friction to slow down player when no keys are pressed
  - `handleCollisionAnimation()` handles the animation when players collide

### Arena
- `ArenaView` class
  - Renders the circular arena
  - Draws the lava border around the edge
  - Sets the size and proportions of the playable area

### Enemies
- `EnemyManager` class
  - Spawns new enemies at random positions on the arena edge
  - Moves enemies towards the player using simple AI
  - Detects collisions between enemies and the player
- `Enemy` class
  - Represents an individual enemy circle
  - Handles enemy appearance and fiery particle effects
  - Manages enemy movement and collision logic

### Energy System
- `EnergyManager` class
  - Tracks the player's current energy level
  - Calculates energy gain based on player speed and movement
  - Handles energy depletion when colliding with enemies
  - Triggers 'overcharge' state when energy reaches maximum
- `EnergyVisual` class
  - `renderEnergy()` updates the energy bar display based on the `EnergyManager`

### Game Flow
1. `GameManager` class
   - Orchestrates the overall game flow
   - Handles game start, countdown, and game over transitions
   - `StartGame()` starts the countdown in the game; enable player and enemy movement; disable game over UI; reset the energy level
   - `GameOver()` displays the "Game Over" message; Provides "Play Again" and "Exit" buttons; Renders the high score leaderboard
2. `LeaderboardManager` class
   - `appendScore()` stores player scores and updates the leaderboard and high scores in a database
   - `renderLeaderboard()` renders the leaderboard UI element 

### Audio
- `AudioManager` class
  - Plays background music and sound effects
  - Handles audio for player movement, enemy interactions, and game events
