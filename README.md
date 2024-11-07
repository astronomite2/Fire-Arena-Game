### **Tech Specification: 2D Birds-Eye View Arena Game**

**Overview:** The game features a top-down view of a circular arena, where the player controls a solid-colored circle. The player has inertia, controlled by the WASD keys, and is tasked with avoiding and colliding with fiery enemies that emerge periodically. Energy is built up by moving faster, which is used to collide with enemies. The arena is surrounded by lava, represented by a red background. If the player runs out of energy or collides with an enemy without enough energy, it results in a game over.

---

### **1\. Gameplay Mechanics:**

* **Player Controls:**  
  * The player is a solid-colored circle that moves inside a circular arena.  
  * The player’s movement is governed by inertia, which is controlled using the WASD keys:  
    * **W** \- Move Up  
    * **A** \- Move Left  
    * **S** \- Move Down  
    * **D** \- Move Right  
    * **F** \- Explode Screen (If player is in overcharged state)  
  * The player’s movement has momentum, meaning the more the player moves in a certain direction, the faster they go. Speed decreases over time if no key is pressed.  
* **Arena:**  
  * **Shape**: A circular arena, visually represented with a thick border surrounding the playable area. The border signifies the "lava" outside, which the player must avoid. Contact with the lava results in game over.  
  * **Size**: The arena consists of 3 concentric rings, with the player starting in the innermost ring. The size of these rings should allow for a dynamic feel as the player accelerates.   
* **Player Energy:**  
  * **Energy (Lifepoints)**: Energy is built by moving faster in a circular pattern. The faster the player moves, the more energy they accumulate. This energy is used when the player collides with enemies.  
  * **Rings:** Each ring has a multiplier for energy buildup, moving in the outermost ring yields the greatest multiplier (outer 2x, 2nd 1.5x, middle disk 1x)  
  * **Energy Depletion**: Each collision with an enemy costs a certain amount of energy, which is deducted based on the player's current speed.  
  * **Game Over**: The player loses the game if their energy reaches 0 or if they collide with an enemy and have insufficient energy to defeat them.  
  * **Energy Overflow**: If an energy cap is reached, player enters overcharge mode, emitting electric particles and turning light blue. Collision will cause an explosion that cuts energy in half while killing all enemies in the ring.  
  * **Mass:** For collision purposes, a constant value set by developer.  
* **Enemy Behavior:**  
  * **Appearance**: Enemies are orange circles with fiery particles around them.  
  * **Spawn**: Enemies spawn randomly at the edge of the arena every few seconds.  
  * **Movement**: Enemies move towards the player in a direct path, accelerating towards the player once they are within range.  
  * **Collision**: When an enemy touches the player, a collision occurs. If the player has enough energy, the enemy is destroyed and the player bounces off the enemy based on momentum. If not, the player loses energy and may eventually die if they run out.  
  * **Mass:** For collision purposes, a constant value set by developer.  
* **Objective**: The goal is to survive as long as possible by accumulating energy and defeating enemies without running out of energy or touching the lava surrounding the arena.

---

### **2\. User Interface (UI):**

* **Opening Page**  
  * Display Controls and Guide:  
    * The opening screen will show an informative guide for new players, explaining how to play:  
      * Movement: "Use WASD to move the player circle."  
      * Objective: "Avoid lava and defeat enemies by building energy through speed\!"  
      * Energy: "Move fast to build energy. Energy is used to collide with enemies."  
      * Enemies: "Fiery enemies spawn periodically. Collide with them using energy to destroy them."  
      * Game Over: "If your energy reaches zero, or you collide with lava, it's Game Over\!"  
  * Start Button:  
    * A Start button will be clearly visible to begin the game.  
    * When pressed, it will start the countdown and transition the player to the main game screen.  
  * Main Menu Button:  
    * An option to return to the main menu, allowing players to navigate back to the homepage or other mini-games.  
    * This button is always available in the UI, in case the player wants to exit the game before starting.  
* **Game Screen:**  
  * **Arena View**: The central part of the screen shows the circular arena with the player and enemies.  
  * **Energy Bar**: A visual energy bar at the top or side of the screen shows the player’s current energy level.  
  * **Lava Border**: The outer border is colored red, representing lava. The player must avoid touching it.  
  * **Enemy Indicators**: Fiery enemies appear as orange circles with particles around them.  
* **Game Over Screen:**  
  * Upon game over, the screen fades to a **game over screen**.  
  * The screen contains:  
    * **"Game Over" Text**.  
    * **Play Again** button.  
    * **Exit** button (to return to the main page).  
    * **Leaderboard**: Displays the top 10 player scores with names/IDs. The player’s name is derived from the unique ID passed from the main page.  
* **Leaderboard:**  
  * The leaderboard should show the top 10 players, ordered by their score (most energy accumulated before death).  
  * Each player’s ID (unique to the game session) will be displayed next to their score.  
* **Countdown Timer At Start**:  
  * When the player presses the **Start** button, a **3-second countdown** will appear on the screen.  
  * The countdown will be displayed in large, bold numbers, centered in the middle of the screen: "3... 2... 1..."  
  * Once the countdown reaches **0**, the game will automatically transition to the main arena, and the player will begin controlling their character.  
  * The countdown will briefly dim the game UI to signal that the game is starting, ensuring a smooth transition from the menu to gameplay.

---

### **3\. Technical Specifications:**

* **Game Engine**: The game should be built using **HTML5, CSS, and JavaScript**, leveraging the **Canvas API** for rendering the game.  
* **Canvas**:  
  * The game arena and all elements (player, enemies, lava) will be drawn on an HTML5 `<canvas>` element.  
  * The canvas size should be responsive to different screen sizes but maintain the circular nature of the arena.  
* **Physics:**  
  * **Inertia**: The movement of the player will be governed by simple 2D physics. The velocity will decay when the player isn't pressing any movement keys, mimicking inertia.  
  * **Collisions**: The game will check for collision between the player’s circle and enemies, as well as with the lava border. If the player’s energy reaches 0, the game ends.  
* **Energy Calculation**:  
  * The player’s speed is calculated based on how much they are moving in the arena. As the player moves faster, their energy accumulates.  
  * The energy is used when colliding with enemies, with higher speed requiring more energy to destroy an enemy.  
* **Enemy AI**: Enemies will have simple AI, where they move towards the player in a straight line until they collide. They will spawn randomly at the edge of the arena.  
* **Sound**:  
  * Background music and sound effects for:  
    * Player movement.  
    * Enemy spawn and collision.  
    * Game over.  
    * Energy accumulation.  
* **Leaderboard Data Storage**:  
  * The leaderboard will be populated by server-side logic, storing player scores (unique ID with score) and displaying the top 10\.  
  * Scores will be updated in real-time when the player finishes a game session, and it will update upon the next game load.

---

### **4\. Technical Stack:**

* **Frontend:**  
  * HTML5: For structuring the game page.  
  * CSS3: To style the game, responsive design, and UI components.  
  * JavaScript: For game logic (player movement, physics, collisions) and interaction with the backend.  
  * **Canvas API**: For rendering the game world, player, enemies, and animations.  
* **Backend (Optional)**:  
  * **Node.js \+ Express**: For handling game sessions, player IDs, and leaderboard data storage.  
  * **Database (e.g., MongoDB)**: To store player scores and leaderboard data.  
  * **REST API**: To manage player data, leaderboard updates, and interactions with the frontend.

---

### **5\. Game Flow:**

1. **Start Screen**:  
   * Player is assigned a unique ID when they access the game from the main page.  
   * The game screen loads with the arena and UI elements (energy bar, lava border).  
2. **In-Game**:  
   * Player controls the character using WASD keys to move.  
   * Enemies spawn periodically and move towards the player.  
   * Player accumulates energy by moving fast in circles.  
   * On collision with an enemy, energy is depleted if sufficient, or player loses on insufficient energy.  
   * If the player touches the lava, it results in a game over.  
3. **Game Over**:  
   * The game transitions to the game over screen with options to play again or exit.  
   * The player's score is recorded, and the leaderboard is updated if necessary.  
4. **Leaderboard**:  
   * Players can view the top 10 leaderboard, displaying the scores and their unique IDs.

---

### **6\. Performance Considerations:**

* **Frame Rate**: Ensure the game runs smoothly at 60 FPS.  
* **Responsive Design**: The game should adapt to various screen sizes while maintaining the circular arena appearance.  
* **Optimizations**: Use efficient collision detection algorithms to handle multiple enemies and fast player movements.

---

This specification covers the essential elements of the game, providing clear guidelines for both the gameplay mechanics and technical implementation.

