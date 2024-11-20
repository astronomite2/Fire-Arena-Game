## Tech Stack
Using PixiJs (https://pixijs.com/8.x/guides) is a good choice for making the game. It is easy and fast to render 2d image assets realtime and it simplifies a lot of the heavy-coding for javascript. It seems to be deployable to multiple platforms as an actual app so it'll be a great tool to publish your game on something like the app store.

## Game Architecture
### Player
- `PlayerController` class -> P0
  - Represents the player circle
  - `handlesMovement()` handles player movement based on WASD input
  - `handlePhysics` calculates player speed and acceleration based on inertia; applies friction to slow down player when no keys are pressed; calculates player movement and momentum (this may me doable by default using PixiJs) 
  - `updateEnergy()` manages player energy/health; triggers 'overcharge' state when energy reaches maximum
  - `checkDeath()` detects collisions with enemies and the lava border
  - `handleCollision()` Handles energy depletion when colliding with enemies
  - `handleCollisionAnimation()` handles the animation when players collide
- `PlayerStats` class
  - `energy` tracks the player's current energy level and energy gain based on player speed and movement
  - `speed` double for the speed of player's movement
  - `health` double for health of player
  - `set()` methods for respective variables
  - `get()` methods for respective variables

### Arena
- `ArenaView` class -> P0
  - Renders the circular arena
  - Draws the lava border around the edge
  - Sets the size and proportions of the playable area

### Enemies
- `EnemyManager` class
  - `enemyList` list of Enemy instances
  - `spawnEnemy()`spawns new enemies at random positions on the arena edge
enemy
- `Enemy` class
  - Represents an individual enemy circle
  - `speed` double for the speed of enemy's movement
  - `health` double for health of enemy
  - `handleEnemyParticle()` handles enemy appearance and fiery particle effects
  - `die()` manages collision logic on player hit
  - `updateEnemyMovement()` handle enemy movement; moves enemies towards the player using simple AI 

### Energy Stats
- `EnergyManager` class -> P3
  - `renderEnergy()` updates the energy bar display based on the current energy
  - `updateEnergy()` calls the energy set methods in the playerstats to update energy accordingly.

### Game Flow
1. `GameManager` class -> P2
   - Orchestrates the overall game flow
   - Handles game start, countdown, and game over transitions
   - `startGame()` starts the countdown in the game; enable player and enemy movement; disable game over UI; reset the energy level
   - `gameOver()` displays the "Game Over" message; Provides "Play Again" and "Exit" buttons; Renders the high score leaderboard
2. `LeaderboardManager` class
   - `appendScore()` stores player scores and updates the leaderboard and high scores in a database
   - `renderLeaderboard()` renders the leaderboard UI element 

### Audio
- `AudioManager` class -> P4
  - `handleBGAudio()` plays background music and sound effects
  - `handlePlayerAudio()` handles audio for player movement, enemy interactions, and game events

 ## Figma Class Diagram
 https://www.figma.com/design/fw8RicLVMyG3xYliQEBvgm/John-Xu's-team-library?node-id=2313-2&t=Zsnpj4CWWac9jdXX-1
