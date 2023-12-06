# Element 5
In Element 5 I have included the following: 
* Multiple Objects
* Merged Meshes
* Arc Rotate Camera
* Player Movement with Animation
* Havok Physics
* Sound and Music
* Menu Buttons
* Scoring System Based on Collision
* Game over Function Based on Location of the Ball (sphere)
* Example of Motion and Animation
* Terrain and Skybox
* Use of Textures and Assets 
* Use of Lighting

# Code snippets
Code 1 - Scoring system
<br>
The following code is a scoring system for the game. When player pushes the ball aroudn the map, score increases. This happens when collision is detected.

1. Variable Declaration
"score" initializes a variable to store the score, starting with a value of 0. "scoreText" declares a variable of type TextBlock. T his variable will be used to display and update the score in the user interface.
```typescript
//Create a scoring variable
let score = 0;
let scoreText: TextBlock;
```

2. Function increaseScore
"increaseScore" is afunction that increments the score by 1, updates the "scoreText" variable to display the new score, logs the score to the console, and allows for additional custom logic based on specific requirements.
```typescript
function increaseScore(): void {
  score += 1;
  scoreText.text = "Score: " + score;
  console.log('Score: ' + score);
  // Additional logic based on your requirements
}
```

3. Function "createScoring"
"createScoring"is a function that creates a scoring user interface using the Babylon.js GUI library. It creates a fullscreen UI ("AdvancedDynamicTexture") and initializes a TextBlock (scoreText) to display the score. It sets properties such as text content, color, font size, and alignment to customize the appearance of the score display. The scoreText is added to the UI using advancedTexture.addControl(scoreText).
```typescript
function createScoring(scene: Scene) {
  const advancedTexture = GUI.AdvancedDynamicTexture.CreateFullscreenUI("UI");
  scoreText = new TextBlock();
  scoreText.text = "Score: " + score;
  scoreText.color = "white";
  scoreText.fontSize = 36; // Increase font size for better visibility
  scoreText.textHorizontalAlignment = GUI.Control.HORIZONTAL_ALIGNMENT_RIGHT; // Align text to the right
  scoreText.textVerticalAlignment = GUI.Control.VERTICAL_ALIGNMENT_TOP; // Align text to the top
  scoreText.paddingTop = "20px";
  scoreText.paddingRight = "20px";
  advancedTexture.addControl(scoreText);
}
```

4. Initialization
Initialization calls the "createScoring" function to set up the scoring UI. The resulting UI component is assigned to the "scoring" variable.
```typescript
let scoring = createScoring(that.scene);
```

Code 2 - Function Game Over

When game over condition is checked, game over text is displayed using the GUI (Graphical User Interface) features of Babylon.js.
 
1.Initialization:

 "gameOverText": This variable is declared to store a Babylon.js TextBlock element, which will be used to display the game over text.

"gameOver": This boolean variable is initialized as false. It is used to track whether the game over condition has been triggered.
```typescript
let gameOverText: TextBlock;
let gameOver = false;
```

2. "showGameOverText" Function:

This function is responsible for creating and displaying the game over text.
It creates a new "TextBlock" ("gameOverText") with the text "Game Over!", red color, and a font size of 48.
The text block's horizontal and vertical alignments are set to center it on the screen. An "AdvancedDynamicTexture" is created and added to the fullscreen UI.
The "gameOverText" is added as a control to the advanced texture, making it visible on the screen.
```typescript
function showGameOverText() {
    // Create and display game over text using GUI
    gameOverText = new TextBlock();
    gameOverText.text = "Game Over!";
    gameOverText.color = "red";
    gameOverText.fontSize = 48;
    gameOverText.textHorizontalAlignment = GUI.Control.HORIZONTAL_ALIGNMENT_CENTER;
    gameOverText.textVerticalAlignment = GUI.Control.VERTICAL_ALIGNMENT_CENTER;

    const advancedTexture = GUI.AdvancedDynamicTexture.CreateFullscreenUI("UI");
    advancedTexture.addControl(gameOverText);
}

```

3. "onBeforeRenderObservable" Callback:

This callback function is executed before each render cycle of the Babylon.js scene.

It checks if the "sphere" (presumably a game object) has fallen below a certain y-coordinate (e.g., -1).

If the condition is met and "gameOver" is "false" (indicating the game over condition hasn't been triggered before), it calls the "showGameOverText" function to display the game over text.

It then sets "gameOver" to "true" to prevent displaying the game over text multiple times.
```typescript
scene.onBeforeRenderObservable.add(() => {
    // Check if the sphere falls off the ground
    if (sphere.position.y < -1) {
        if (!gameOver) {
            // Display game over text
            showGameOverText();
            gameOver = true;
        }
    }
});
```
Code 3 - Reload Button
Code 4 - Menu Button
Code 5 - Player Functions and action manager
Code 6 - Football with physics(collision, score, game over)
Code 7 - Animated Sphere
Code 8 - Cloned Houses
Code 9 - Terrain
Code 10 - Village Ground
Code 11 - Football Pitch
Code 12 - Skybox
Code 13 - Goal Posts
Code 14 - Lighting
Code 15 - Camera
Code 16 - Enabling Physics

# Assets and texture sources
Player model has been sourced from babylon documentation website and can be found here:
* https://playground.babylonjs.com/#C38BUD#1

Football pitch texture has been sourced from google and can be found here: 
* https://t4.ftcdn.net/jpg/04/40/51/03/360_F_440510369_R1T9gwH1ZkpSBCjYDg47X2AhfL0AOOWf.jpg

Village ground has been sourced from babylon documentation website and can be found here:
* https://assets.babylonjs.com/environments/villagegreen.png

Lava texture has been sourced from babylon documentation and can be found here: 
* https://www.babylonjs-playground.com/textures/lava/lavatile.jpg

Terrain that surrounds village has been sourced from babylon documentation and can be found here: 
* https://assets.babylonjs.com/environments/villageheightmap.png

Textures for the houses have been sourced from babylon documentation and can be found here: 
* https://assets.babylonjs.com/environments/roof.jpg
* https://assets.babylonjs.com/environments/semihouse.png
* https://assets.babylonjs.com/environments/cubehouse.png

Texture for ball has been sourced from babylon documentation and can be found here: 
* https://www.babylonjs-playground.com/textures/fur.jpg

Texture for animated sphere has been sourced from babylon documentation and can be found here: 
* https://www.babylonjs-playground.com/textures/lava/lavatile.jpg