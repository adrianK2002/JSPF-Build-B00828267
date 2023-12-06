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
### Code 1 - Scoring system

The following code is a scoring system for the game. When player pushes the ball aroudn the map, score increases. This happens when collision is detected.

1. Variable Declaration
+ "score" initializes a variable to store the score, starting with a value of 0. 
+ "scoreText" declares a variable of type TextBlock. T his variable will be used to display and update the score in the user interface.
```typescript
//Create a scoring variable
let score = 0;
let scoreText: TextBlock;
```

2. Function increaseScore
+ "increaseScore" is a function that increments the score by 1, updates the "scoreText" variable to display the new score, logs the score to the console, and allows for additional custom logic based on specific requirements.
```typescript
function increaseScore(): void {
  score += 1;
  scoreText.text = "Score: " + score;
  console.log('Score: ' + score);
  // Additional logic based on your requirements
}
```

3. Function "createScoring"
+ "createScoring"is a function that creates a scoring user interface using the Babylon.js GUI library. It creates a fullscreen UI ("AdvancedDynamicTexture") and initializes a TextBlock (scoreText) to display the score. It sets properties such as text content, color, font size, and alignment to customize the appearance of the score display. The scoreText is added to the UI using advancedTexture.addControl(scoreText).
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

### Code 2 - Function Game Over

When game over condition is checked, game over text is displayed using the GUI (Graphical User Interface) features of Babylon.js.
 
1.Initialization:

 + "gameOverText": This variable is declared to store a Babylon.js TextBlock element, which will be used to display the game over text.

+ "gameOver": This boolean variable is initialized as false. It is used to track whether the game over condition has been triggered.
```typescript
let gameOverText: TextBlock;
let gameOver = false;
```

2. "showGameOverText" Function:

+ This function is responsible for creating and displaying the game over text.
It creates a new "TextBlock" ("gameOverText") with the text "Game Over!", red color, and a font size of 48.
+ The text block's horizontal and vertical alignments are set to center it on the screen. An "AdvancedDynamicTexture" is created and added to the fullscreen UI.
+ The "gameOverText" is added as a control to the advanced texture, making it visible on the screen.
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

+ This callback function is executed before each render cycle of the Babylon.js scene.

+ It checks if the "sphere" (presumably a game object) has fallen below a certain y-coordinate (e.g., -1).

+ If the condition is met and "gameOver" is "false" (indicating the game over condition hasn't been triggered before), it calls the "showGameOverText" function to display the game over text.

+ It then sets "gameOver" to "true" to prevent displaying the game over text multiple times.
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
### Code 3 - Reload Button

This code defines a function, "createReloadButton", that creates a graphical user interface (GUI) button with specific styling and functionality. The button is designed to trigger a page reload when clicked.  

1. "createReloadButton" Function

The function takes several parameters

+ "scene": Represents the 3D scene where the button will be added.\
+ "name": A string representing the name of the button.\
+ "index": A string representing an index for the button.\
+ "x" and "y": Strings representing the X and Y positions of the button.\
+ "advtex": Some variable (possibly a GUI advanced texture) where the button will be added.
```typescript
function createReloadButton(
  scene: Scene,
  name: string,
  index: string,
  x: string,
  y: string,
  advtex
) {
```

2. Creating the Reload Button \
This line creates a GUI button using the Babylon.js library. It is an image button with centered text displaying "Reload," and it uses an image from the path "textures/reload.png."
```typescript
const reloadButton = GUI.Button.CreateImageWithCenterTextButton("reloadButton", "Reload", "textures/reload.png");
```

3. Setting Button Properties \
These lines set various properties for the button, such as width, height, text color, background color, font size, corner radius, and thickness.
```typescript
reloadButton.width = "120px";
reloadButton.height = "40px";
reloadButton.color = "white";
reloadButton.background = "green";
reloadButton.fontSize = 14;
reloadButton.cornerRadius = 8;
reloadButton.thickness = 2;
```
4. Setting Button Position \
These lines set the horizontal and vertical alignment of the button, as well as its top and left positions.
```typescript
reloadButton.horizontalAlignment = GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
reloadButton.verticalAlignment = GUI.Control.VERTICAL_ALIGNMENT_TOP;
reloadButton.top = "20px";
reloadButton.left = "20px";
```
5. Button Click Event

This code sets up an event listener for the button's "onPointerUp" event. When the button is clicked, it logs a message to the console and calls the reloadPage function, which reloads the page.
```typescript
reloadButton.onPointerUpObservable.add(() => {
  console.log("THE BUTTON HAS BEEN CLICKED");
  // Call the reloadPage function when the button is clicked
  reloadPage();
});
```

6. Adding Button to Advanced Texture
This line adds the created button to the specified advanced texture ("advtex").
```typescript
advtex.addControl(reloadButton);
```
7. return reloadButton\
The function returns the created "reloadButton".
```typescript
return reloadButton;
```
8. Creating an Instance of the Reload Button\
This line creates an instance of the reload button by calling the "createReloadButton" function with specific parameters. The button is associated with the 3D scene ("that.scene"), has the name "Reload," and is positioned at coordinates (-500px, -280px) relative to the top-left corner. The button is added to the "advancedTexture".
```typescript
let reloadButton = createReloadButton(that.scene, "Reload", "Reload", "-500px", "-280px", advancedTexture);
```



### Code 4 - Menu Button
1. "createSceneButton" Function\
The function takes several parameters:\
+ "scene": Represents the 3D scene where the button will be added.\
+ "name": A string representing the name of the button.\
+ "index": A string representing an index for the button.\
+ "x" and "y": Strings representing the X and Y positions of the button.\
+"advtex": Some variable (possibly a GUI advanced texture) where the button will be added.
```typescript
function createSceneButton(
  scene: Scene,
  name: string,
  index: string,
  x: string,
  y: string,
  advtex
) {
```
2. Creating the Button\
This line creates a GUI button using the Babylon.js Button.CreateSimpleButton method, providing the specified name and index.
```typescript
let button = GUI.Button.CreateSimpleButton(name, index);
```
3. Setting Button Properties\
These lines set various properties for the button, such as width, height, text color, background color, font size, corner radius, and thickness.
```typescript
button.width = "120px";
button.width = "120px";
button.height = "40px";
button.color = "white";
button.background = "green";
button.fontSize = 14;
button.cornerRadius = 8;
button.thickness = 2;
```
4. Setting Button Position\
These lines set the horizontal and vertical alignment of the button, as well as its top and left positions.
```typescript
button.horizontalAlignment = GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
button.verticalAlignment = GUI.Control.VERTICAL_ALIGNMENT_TOP;
button.top = "20px";
button.left = "150px";
```
5. Adding Sound and Click Event\
This section creates a sound object ("buttonClick") for a menu click sound and associates it with a WAV file. It sets up an event listener for the button's "onPointerUp" event, logging a message to the console, playing the click sound, and calling the "setSceneIndex(0)" function when the button is clicked.
```typescript
const buttonClick = new Sound("MenuClickSFX", "./audio/menu-click.wav", scene, null, {
  loop: false,
  autoplay: false,
});

button.onPointerUpObservable.add(function() {
  console.log("THE BUTTON HAS BEEN CLICKED");
  buttonClick.play();
  setSceneIndex(0);
});
```

6. Adding Button to Advanced Texture\
This line adds the created button to the specified advanced texture ("advtex").
```typescript
advtex.addControl(button);
```
7. Return Statement
The function returns the created button.
```typescript
return button;
```
8. Creating an Instance of the Button\
This line creates an instance of the button by calling the "createSceneButton" function with specific parameters. The button is associated with the 3D scene ("that.scene"), has the name "but1" and index "Menu," and is positioned at coordinates (-500px, -280px) relative to the top-left corner. The button is added to the "advancedTexture".
```typescript
let button1 = createSceneButton(that.scene, "but1", "Menu", "-500px", "-280px", advancedTexture);
```
### Code 5 - Player Functions and action manager
#### importPlayerMesh Function
This code defines functions related to a 3D player character in a Babylon.js scene, including importing a player mesh, handling user input for movement, managing animations, detecting collisions with a collider mesh, and setting up an action manager for keyboard input.
1. Variables\
Defines variables for tracking key presses, current speed, walking speed, and running speed.
```typescript
let keyDownMap: any[] = [];
let currentSpeed: number = 0.1;
let walkingSpeed: number = 0.1;
let runningSpeed: number = 0.4;
```
2. Function Definition\
Defines the importPlayerMesh function that takes parameters like the scene, collider mesh, initial Y and Z positions, and a scale factor.
```typescript
function importPlayerMesh(scene: Scene, collider: Mesh, y: number, z: number, scaleFactor: number) {
```

3. Mesh Import\
Imports a player mesh using Babylon.js SceneLoader.ImportMesh.
```typescript
let item: any = SceneLoader.ImportMesh("", "./models/", "dummy3.babylon", scene, function(newMeshes, particleSystems, skeletons, animationGroups) {
```
4. Mesh Setup\ 

Modifies the scale of the imported mesh and sets up animations.
```typescript
// ... (mesh and skeleton setup code)
mesh.scaling = new Vector3(scaleFactor, scaleFactor, scaleFactor);
```

5. User Input and Animation\ 
Handles user input (W, A, S, D keys) for movement, adjusts the player's position, and manages animations (idle and walking).

6. Collision Handling\
Detects collisions with a collider mesh and takes appropriate actions, such as logging a message and calling increaseScore().

7. Physics Collision Setup\
Sets up physics collision using the Babylon.js physics engine.

8. Return Statement\
Returns the created player mesh.
```typescript
return item;
```

#### "actionManager" Function
1. Function Definition\
Defines the actionManager function that takes a Babylon.js scene as a parameter.
```typescript
function actionManager(scene: Scene) {
```

2. Action Manager Setup\
Initializes a new action manager for the scene.
```typescript
scene.actionManager = new ActionManager(scene);
```

3. Key Down and Key Up Event Handling\
Registers actions for key down and key up events, updating the keyDownMap array accordingly.

4. Return Statement\
Returns the created action manager.
```typescript
return scene.actionManager;
```

### Code 6 - Havok Inizitialization (physics)
This code is using the Babylon.js framework to integrate the Havok Physics engine for handling physics simulations in a 3D scene. 

1. Importing Modules\
The code imports necessary modules from the Babylon.js framework and the Havok Physics engine. This includes the "HavokPhysics" object and specific classes and types related to physics.
```typescript
import HavokPhysics from "@babylonjs/havok";
import { HavokPlugin, PhysicsAggregate, PhysicsShapeType } from "@babylonjs/core";
```
2. Initializing Havok Physics\
This part of the code initializes Havok Physics asynchronously. The "HavokPhysics" function is called, which returns a promise. When the promise resolves, the "then" callback is executed, and the "havok" object is assigned to the "initializedHavok" variable.
```typescript
let initializedHavok;
HavokPhysics().then((havok) => {
  initializedHavok = havok;
});
```
3. Creating Havok Plugin\
Here, another instance of Havok Physics is created using "HavokPhysics()", and a new "HavokPlugin" is instantiated with "true" as the first argument (enabling debugging features) and the obtained "havokInstance".
```typescript
const havokInstance = await HavokPhysics();
const havokPlugin = new HavokPlugin(true, havokInstance);
```
4. Setting up Physics in the Scene\
This section sets up physics in the Babylon.js scene. It assigns the Havok Physics instance to "globalThis.HK" (globally accessible), and then the "enablePhysics" method of the scene is called. It takes a gravity vector ("new Vector3(0, -9.8, 0)") and the "havokPlugin" as parameters to enable physics in the scene.
```typescript
globalThis.HK = await HavokPhysics();
that.scene.enablePhysics(new Vector3(0, -9.8, 0), havokPlugin);
```
### Code 7 - Football with physics(collision, score, game over)
1. Material and Texture:\
A standard material (mat) is created. A texture is loaded and assigned to the diffuseTexture property of the material.
```typescript
// Create a standard material and a texture for the sphere
  const mat = new StandardMaterial("mat");
  const texture = new Texture("https://www.babylonjs-playground.com/textures/fur.jpg");
  ```
2. Creating Sphere:\
A sphere is created using MeshBuilder.CreateSphere. The sphere's scale, position, and material are set.
```typescript
let sphere: Mesh = MeshBuilder.CreateSphere("sphere", {});
  ```
3. Physics Properties:\
A PhysicsAggregate is created for the sphere, specifying it as a sphere shape with a mass of 1.
```typescript
  // Create a PhysicsAggregate for the sphere with physics properties
  const sphereAggregate = new PhysicsAggregate(sphere, PhysicsShapeType.SPHERE, { mass: 1 }, scene);
```
4. Event Listener for Physics:\
An event listener is added to the scene's onBeforeRenderObservable to check if the sphere falls below a certain position (-1 in the y-axis). If the sphere falls below that position and the gameOver flag is not set, it calls a function (showGameOverText) and sets the gameOver flag to true.
```typescript
  // Add an event listener to check if the sphere falls off the ground
  scene.onBeforeRenderObservable.add(() => {
    if (sphere.position.y < -1) {
      if (!gameOver) {
        // Display game over text and set the gameOver flag to true
        showGameOverText();
        gameOver = true;
      }
    }
  });
```
5. Return the Sphere:\
The function returns the created sphere.
6. Creating a Sphere Instance:\
Finally, an instance of the sphere is created in the Babylon.js scene using the createSphere function with specific parameters, and it is assigned to that.box.
```typescript
// Create a sphere in the scene with specific parameters
that.box = createSphere(that.scene, 2, 2, 2, 0.5);
```
### Code 8 - Animated Sphere
1. Material and Texture:\
A standard material (mat) is created. A texture is loaded and assigned to the diffuseTexture property of the material.
2. Creating Sphere:\
A sphere is created using MeshBuilder.CreateSphere with specific parameters such as diameter and segments. The sphere's initial position and material are set.
3. Dynamic Rotation and Position:\
The code sets up a dynamic rotation for the sphere based on the rotation parameter. If rotation is true, the sphere rotates around the x and z axes. The position of the sphere is dynamically updated using a trigonometric function. The sphere moves in a circular path on the x-z plane.
```typescript
 // Set up dynamic rotation and position based on trigonometric functions
  var alpha = 0;
  scene.registerBeforeRender(function () {
    // Rotate the sphere
    if (rotation) {
      sphere1.rotation.x += 0.01;
      sphere1.rotation.z += 0.02;
    }

    // Update the position using a trigonometric function
    sphere1.position = new Vector3(Math.cos(alpha) * 20, 10, Math.sin(alpha) * 20);
    alpha += 0.01;
  });
  ```
5. Event Listener for Dynamic Changes:\
An event listener (registerBeforeRender) is added to the scene to continuously update the rotation and position of the sphere before each render frame.
6. Return the Sphere:\
The function returns the created sphere.
7. Creating a Sphere Instance:\
Finally, an instance of the sphere is created in the Babylon.js scene using the createSphere1 function with specific parameters (that.scene and true for rotation), and it is assigned to that.sphere1.

### Code 9 - Terrain
1. Material and Texture:\
A standard material (largeGroundMat) is created.A diffuse texture is assigned to the material, using an image of lava from the given URL.
2. Creating Ground from Height Map:\
The MeshBuilder.CreateGroundFromHeightMap method is used to create a ground mesh based on a height map. The height map is specified with the URL "https://assets.babylonjs.com/environments/villageheightmap.png". Other parameters such as width, height, subdivisions, minHeight, and maxHeight are configured.
```typescript
  // Create a ground mesh from a height map
  const largeGround = MeshBuilder.CreateGroundFromHeightMap(
    "largeGround",
    "https://assets.babylonjs.com/environments/villageheightmap.png",
    { width: 150, height: 150, subdivisions: 20, minHeight: -0.01, maxHeight: 9.99 }
  );
```
3. Assigning Material:\
The created material (largeGroundMat) is assigned to the ground mesh (largeGround).
```typescript
  // Assign the material to the ground mesh
  largeGround.material = largeGroundMat;
```
4. Return the Ground Mesh:\
The function returns the created ground mesh.
5. Creating a Terrain Instance:\
Finally, an instance of the terrain is created in the Babylon.js scene using the createTerrain function, and it is assigned to that.largeGround. The resulting effect is a textured terrain based on the provided height map, with the appearance of lava due to the applied texture.
### Code 10 - Village Ground
1. Material and Texture:\
A standard material (groundMat) is created. A diffuse texture is assigned to the material, using an image of a village green from the given URL.
2. Alpha Channel for Transparency:\
The hasAlpha property of the material's diffuse texture is set to true, indicating the presence of an alpha channel for transparency.
```typescript
 groundMat.diffuseTexture.hasAlpha = true;
 ```
3. Creating Ground Mesh:\
The MeshBuilder.CreateGround method is used to create a ground mesh with specific parameters such as height, width, and subdivisions.
4. Physics Properties:\
A PhysicsAggregate is created for the ground, specifying it as a box shape with a mass of 0. This implies that the ground is static and won't move due to physics simulation.
```typescript
 const groundAggregate = new PhysicsAggregate(ground, PhysicsShapeType.BOX, { mass: 0 }, scene);
  ```
5. Assigning Material:\
The created material (groundMat) is assigned to the ground mesh (ground).
6. Enabling Shadow Reception:\
The ground mesh is configured to receive shadows by setting the receiveShadows property to true.
```typescript
 ground.receiveShadows = true;
   ```
7. Return the Ground Mesh:\
The function returns the created ground mesh. \
The resulting effect is a textured ground with transparency and the ability to receive shadows in a Babylon.js scene.
### Code 11 - Football Pitch
1. Material and Texture:\
A standard material (groundMat) is created. A diffuse texture is assigned to the material, using an image of a football pitch from the given URL.
2. Alpha Channel for Transparency:\
The hasAlpha property of the material's diffuse texture is set to true, indicating the presence of an alpha channel for transparency.
3. Creating Ground Mesh (Football Pitch):\
The MeshBuilder.CreateGround method is used to create a ground mesh representing the football pitch with specific parameters such as height, width, and subdivisions.
4. Setting Position:\
The position of the ground mesh is set based on the provided position parameter.
```typescript
function createFootballPitch(scene: Scene, size: number = 10, width: number = 10, position: Vector3 = Vector3.Zero()) {
  ```
```typescript
  // Set the position of the ground
  ground1.position = position;
```
5. Physics Properties:\
A PhysicsAggregate is created for the ground, specifying it as a box shape with a mass of 0. This implies that the football pitch is static and won't move due to physics simulation.
6. Return the Ground Mesh:\
The function returns the created ground mesh representing the football pitch.
7. Creating a Football Pitch Instance:\
Finally, an instance of the football pitch is created in the Babylon.js scene using the createFootballPitch function with specific parameters, and it is assigned to that.ground1.
```typescript
// Create a football pitch in the scene and assign it to that.ground1
that.ground1 = createFootballPitch(that.scene, 10, 12, new Vector3(-6, 0.01, -8));
```
### Code 12 - Skybox
1. Creating Skybox Mesh:\
The function uses MeshBuilder.CreateBox to create a box mesh named "skyBox" with a specified size of 150 units. This box will represent the skybox.
2. Creating Skybox Material:\
A StandardMaterial named "skyBox" is created for the skybox.
3. Back-face Culling:\
Back-face culling is disabled (backFaceCulling = false) to render both sides of the skybox.
```typescript
  // Disable back-face culling to render both sides of the skybox
  skyboxMaterial.backFaceCulling = false;
  ```
4. Reflection Texture (CubeTexture):\
A CubeTexture is created and set as the reflection texture for the skybox material. The texture is loaded from the "textures/skybox" directory.
```typescript
 // Set a CubeTexture as the reflection texture for the skybox
  skyboxMaterial.reflectionTexture = new CubeTexture("textures/skybox", scene);
   ```
5. Coordinates Mode for Reflection Texture:\
The coordinates mode for the reflection texture is set to Texture.SKYBOX_MODE.
```typescript
 // Set the coordinates mode for the reflection texture
  skyboxMaterial.reflectionTexture.coordinatesMode = Texture.SKYBOX_MODE;
```
6. Diffuse and Specular Colors:\
Diffuse and specular colors are set to black (Color3(0, 0, 0)) to avoid introducing additional colors to the reflections.
7. Assigning Material to Skybox Mesh:\
The skybox mesh is assigned the created material.
8. Return the Skybox Mesh:\
The function returns the created skybox mesh.
### Code 13 - Goal Posts
This code defines four functions, createGoalPosts1 through createGoalPosts4, each responsible for creating a goal post mesh with specific dimensions and positions in a scene. Additionally, physics properties are applied to each goal post using the PhysicsAggregate class. Finally, the functions are called to create instances of goal posts in the scene and assign them to variables (that.GoalPost1, that.GoalPost2, that.GoalPost3, that.GoalPost4).

#### Goal Post Creation Functions:
1. createGoalPosts1 Function:
+ Creates a goal post mesh (GoalPost1) using MeshBuilder.CreateBox.
+ Sets the position of GoalPost1 to (-11.5, 0, -7).
+ Applies physics properties using PhysicsAggregate with a box shape and mass of 0.
Returns GoalPost1.
2. createGoalPosts2 Function:
+ Similar to createGoalPosts1, creates GoalPost2.
+ Sets the position of GoalPost2 to (-11.5, 0, -9).
+ Applies physics properties using PhysicsAggregate with a box shape and mass of 0.
+ Returns GoalPost2.
3. createGoalPosts3 Function:
+ Similar to createGoalPosts1, creates GoalPost3.
+ Sets the position of GoalPost3 to (-0.5, 0, -9).
+ Applies physics properties using PhysicsAggregate with a box shape and mass of 0.
+ Returns GoalPost3.
4. createGoalPosts4 Function:
+ Similar to createGoalPosts1, creates GoalPost4.
+ Sets the position of GoalPost4 to (-0.5, 0, -7).
+ Applies physics properties using PhysicsAggregate with a box shape and mass of 0.
+ Returns GoalPost4.
#### Goal Post Instance Creation:
Calls each of the four functions to create instances of goal posts and assigns them to variables (that.GoalPost1, that.GoalPost2, that.GoalPost3, that.GoalPost4).\
In summary, these functions provide a modular and organized way to create goal post meshes with specific dimensions and positions in a Babylon.js scene, allowing for easy customization and placement of goal posts within the 3D environment.
### Code 14 - Lighting\
This code defines a TypeScript function createHemiLight that creates a hemispheric light in a Babylon.js scene. The hemispheric light simulates the effect of ambient light by emitting light evenly in all directions from a specified direction.

1. Creating Hemispheric Light:
The function uses the HemisphericLight constructor to create a hemispheric light named "light." The light is oriented with a direction vector of (0, 1, 0), indicating that it emits light from the positive y-axis (upwards), simulating a light source from above.
```typescript
  // Create a hemispheric light named "light" with a direction of (0, 1, 0)
  const light = new HemisphericLight("light", new Vector3(0, 1, 0), scene);
  ```
2. Setting Intensity:
The intensity property of the hemispheric light is set to 0.8. This controls the brightness or strength of the light.
```typescript
  // Set the intensity of the hemispheric light to 0.8
  light.intensity = 0.8;
```
3. Return the Hemispheric Light:
The function returns the created hemispheric light.
4. Creating a Hemispheric Light Instance:
Finally, an instance of the hemispheric light is created in the Babylon.js scene using the createHemiLight function, and it is assigned to that.hemisphericLight.

This hemispheric light can be used to illuminate the scene with ambient light, providing a soft, uniform illumination from above. Adjusting the intensity parameter allows for fine-tuning the overall brightness of the scene.
### Code 15 - Camera\ 
This code defines a function createArcRotateCamera that creates and configures an ArcRotateCamera in a scene. The ArcRotateCamera is a type of camera that revolves around a target point while looking at that point, allowing for interactive navigation.

1. Initial Camera Parameters:\
Initial values for camAlpha, camBeta, camDist, and camTarget are defined. These values determine the initial state of the ArcRotateCamera.
2. Creating ArcRotateCamera:\
The ArcRotateCamera constructor is used to create a camera named "camera1" with the specified parameters:\
+ camAlpha: Horizontal rotation angle in radians (initially set to -π/2).\
+ camBeta: Vertical rotation angle in radians (initially set to π/2.5).\
+ camDist: Distance from the target point (initially set to 10).\
+ camTarget: The target point in 3D space (initially set to (0, 0, 0)).\
+ scene: The scene to which the camera belongs.
3. Attaching Controls:\
The attachControl method is called with true as an argument, enabling user controls for mouse/touch events. This allows users to interactively rotate, zoom, and pan the camera using input devices.
4. Return the ArcRotateCamera:\
+ The function returns the created ArcRotateCamera.
5. Creating a Camera Instance:\
+ An instance of the ArcRotateCamera is created by calling the createArcRotateCamera function in the scene.

This ArcRotateCamera is ready for use in a 3D scene, and users can control its movement and orientation interactively. The initial parameters (camAlpha, camBeta, camDist, camTarget) determine the camera's initial position and orientation. Adjusting these values can customize the camera's starting configuration.
```typescript
function createArcRotateCamera(scene: Scene) {
  // Initial camera parameters
  let camAlpha = -Math.PI / 2;
  let camBeta = Math.PI / 2.5;
  let camDist = 10;
  let camTarget = new Vector3(0, 0, 0);

  // Create an ArcRotateCamera named "camera1" with specified parameters
  let camera = new ArcRotateCamera(
    "camera1",
    camAlpha,
    camBeta,
    camDist,
    camTarget,
    scene,
  );

  // Enable user controls to attach mouse/touch events for camera interaction
  camera.attachControl(true);

  // Return the created ArcRotateCamera
  return camera;
}

// Create an ArcRotateCamera in the scene and assign it to a variable
let cameraInstance = createArcRotateCamera(scene);

```

### Code 18 - Cloned Houses
This code defines a series of functions to create and manipulate 3D house meshes in a scene. Let's break down each part of the code:
```typescript
1. createBox Function:
+ Creates a box mesh with a specified width.
+ Sets different textures for the box material based on the width.
+ Defines face UV coordinates to map textures to different sides of the box.
+ Returns the created box.

const faceUV = [];
    if (width == 2) {
        faceUV[0] = new Vector4(0.6, 0.0, 1.0, 1.0); //rear face
        faceUV[1] = new Vector4(0.0, 0.0, 0.4, 1.0); //front face
        faceUV[2] = new Vector4(0.4, 0, 0.6, 1.0); //right side
        faceUV[3] = new Vector4(0.4, 0, 0.6, 1.0); //left side
    }
    else {
        faceUV[0] = new Vector4(0.5, 0.0, 0.75, 1.0); //rear face
        faceUV[1] = new Vector4(0.0, 0.0, 0.25, 1.0); //front face
        faceUV[2] = new Vector4(0.25, 0, 0.5, 1.0); //right side
        faceUV[3] = new Vector4(0.75, 0, 1.0, 1.0); //left side
    }
```
2. createRoof Function:
+ Creates a cylinder mesh to represent a roof.
+ Assigns a roof texture to the material.
+ Adjusts scaling, rotation, and position properties.
+ Returns the created roof.
```typescript
  function createRoof(scene: Scene, width: number) {
    const roofMat = new StandardMaterial("roofMat");
    roofMat.diffuseTexture = new Texture("https://assets.babylonjs.com/environments/roof.jpg");

    const roof = MeshBuilder.CreateCylinder("roof", {diameter: 1.3, height: 1.2, tessellation: 3});
    roof.material = roofMat;
    roof.scaling.x = 0.75;
    roof.scaling.y = width;
    roof.rotation.z = Math.PI / 2;
    roof.position.y = 1.22;
    
    return roof;
  }
```
3. createHouse Function:
+ Combines a box and a roof into a single mesh using Mesh.MergeMeshes.
+ Sets the position and rotation of the house.
+ Creates a PhysicsAggregate for the house mesh with physics properties.
+ Returns the created house.
```typescript
  function createHouse(scene: Scene, width: number, px: number, py:number, pz:number) {
    const box = createBox(scene, width);
    const roof = createRoof(scene, width);
    const house: any = Mesh.MergeMeshes([box, roof], true, false, undefined, false, true);
    house.position = new Vector3(1, 0, 10);
    const houseAggregate = new PhysicsAggregate(house, PhysicsShapeType.BOX, { mass: 0 }, scene);
    return house;
  }
```
4. cloneHouse Function:
+ Clones instances of two different house types (detached_house and semi_house) with varying positions, rotations, and scales.
```typescript
const detached_house = createHouse(scene, 1, 0,0,0,); //.clone("clonedHouse");
    const detached_houseAggregate = new PhysicsAggregate(detached_house, PhysicsShapeType.BOX, { mass: 0 }, scene);
```
+ Defines an array (places) that specifies the type, rotation, and position for each house instance.
```typescript
//each entry is an array [house type, rotation, x, z]
    const places: number[] [] = []; 
    places.push([1, -Math.PI / 16, -6.8, 2.5 ]);
    places.push([2, -Math.PI / 16, -4.5, 3 ]);
```
+ Creates instances of houses based on the provided specifications.
+ Returns an array of created house instances.


5. Creating Instances:
+ Calls the cloneHouse function and assigns the result to that.house. 
+ Calls the createSphere function (which seems to be missing from the provided code) and assigns the result to that.box.
```typescript
for (let i = 0; i < places.length; i++) {
      if (places[i][0] === 1) {
          houses[i] = detached_house.createInstance("house" + i);
         // const detached_houseAggregate = new PhysicsAggregate(detached_house, PhysicsShapeType.BOX, { mass: 1 }, scene);
          
      }
      else {
          houses[i] = semi_house.createInstance("house" + i);
          //const semi_houseAggregate = new PhysicsAggregate(semi_house, PhysicsShapeType.BOX, { mass: 1 }, scene);
      }
        houses[i].rotation.y = places[i][1];
        houses[i].position.x = places[i][2];
        houses[i].position.z = places[i][3];
        const housesAggregate = new PhysicsAggregate(houses[i], PhysicsShapeType.BOX, { mass: 0 }, scene);
        
    }
  ```
#### Notes:
Physics aggregates are created for each house and box, but they are currently commented out (//). 

The that.house variable represents an array of house instances, and the that.box variable represents a single box instance.

In summary, this code is for creating 3D house  meshes in a scene with various textures, sizes, positions, and rotations. It also demonstrates the use of physics aggregates for potential physics simulations.

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

# Import List (top section)
```typescript
//TOP OF CODE - IMPORTING BABYLONJS
import setSceneIndex from "./index";
import "@babylonjs/core/Debug/debugLayer";
import "@babylonjs/inspector";
import {
    Scene,
    ArcRotateCamera,
    Vector3,
    Vector4,
    HemisphericLight,
    SpotLight,
    MeshBuilder,
    Mesh,
    Light,
    Camera,
    Engine,
    StandardMaterial,
    Texture,
    Color3,
    Space,
    ShadowGenerator,
    PointLight,
    DirectionalLight,
    CubeTexture,
    Sprite,
    SpriteManager,
    SceneLoader,
    ActionManager,
    ExecuteCodeAction,
    AnimationPropertiesOverride,
    Sound,
    SphereBlock
  } from "@babylonjs/core";
  import * as GUI from "@babylonjs/gui";
  import HavokPhysics from "@babylonjs/havok";
  import { HavokPlugin, PhysicsAggregate, PhysicsShapeType } from "@babylonjs/core";
  import { TextBlock } from "@babylonjs/gui";
  //----------------------------------------------------
```
# Function List (middle section)
```typescript
  //----------------------------------------------------
  //Middle Section

  //Initialisation of Physics (Havok)
  let initializedHavok;
  HavokPhysics().then((havok) => {
    initializedHavok = havok;
  });

  const havokInstance = await HavokPhysics();
  const havokPlugin = new HavokPlugin(true, havokInstance);

  globalThis.HK = await HavokPhysics();
  //-----------------------------------------------------

  //Buttons+score system

 // Create a scoring variable
 let score = 0;
 let scoreText: TextBlock;
 let gameOverText: TextBlock;
 let gameOver = false;

 // Function to increase the score
 function increaseScore(): void {
   score += 1;
   scoreText.text = "Score: " + score;
   console.log('Score: ' + score);
   
 }
 //Function to reload page
  function reloadPage(): void {
    // Reload the page
    window.location.reload();
}

function createReloadButton(scene: Scene, name: string, index: string, x: string, y: string, advtex) {
  const reloadButton = GUI.Button.CreateImageWithCenterTextButton("reloadButton", "Reload", "textures/reload.png");
reloadButton.width = "120px";
  reloadButton.width = "120px";
  reloadButton.height = "40px";
  reloadButton.color = "white";
  reloadButton.background = "green";
  reloadButton.fontSize = 14;
  reloadButton.cornerRadius = 8;
  reloadButton.thickness = 2;
  reloadButton.horizontalAlignment = GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
  reloadButton.verticalAlignment = GUI.Control.VERTICAL_ALIGNMENT_TOP;
  reloadButton.top = "20px";
  reloadButton.left = "20px";

  reloadButton.onPointerUpObservable.add(() => {
    console.log("THE BUTTON HAS BEEN CLICKED");
    // Call the reloadPage function when the button is clicked
    reloadPage();
  });

  advtex.addControl(reloadButton);
  return reloadButton;
}
    
function createSceneButton(scene: Scene, name: string, index: string, x: string, y: string, advtex) {
  let button = GUI.Button.CreateSimpleButton(name, index);
  button.width = "120px";
  button.width = "120px";
  button.height = "40px";
  button.color = "white";
  button.background = "green";
  button.fontSize = 14;
  button.cornerRadius = 8;
  button.thickness = 2;
  button.horizontalAlignment = GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
  button.verticalAlignment = GUI.Control.VERTICAL_ALIGNMENT_TOP;
  button.top = "20px";
  button.left = "150px";

      const buttonClick = new Sound("MenuClickSFX", "./audio/menu-click.wav", scene, null, {
        loop: false,
        autoplay: false,
      });

      button.onPointerUpObservable.add(function() {
          console.log("THE BUTTON HAS BEEN CLICKED");
          buttonClick.play();
          setSceneIndex(0);
      });
      advtex.addControl(button);
      return button;
}

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



// Function to display game over text
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

  //player functinos
  let keyDownMap: any[] = [];
  let currentSpeed: number = 0.1;
  let walkingSpeed: number = 0.1;
  let runningSpeed: number = 0.4;

  function importPlayerMesh(scene: Scene, collider: Mesh, y: number, z:number, scaleFactor: number,) {
    let tempItem = { flag: false } 
    let item: any = SceneLoader.ImportMesh("", "./models/", "dummy3.babylon", scene, function(newMeshes, particleSystems, skeletons, animationGroups) {
      let mesh = newMeshes[0];
      let skeleton = skeletons[0];
      skeleton.animationPropertiesOverride = new AnimationPropertiesOverride();
      skeleton.animationPropertiesOverride.enableBlending = true;
      skeleton.animationPropertiesOverride.blendingSpeed = 0.05;
      skeleton.animationPropertiesOverride.loopMode = 1; 
      mesh.scaling = new Vector3(scaleFactor, scaleFactor, scaleFactor);

      let idleRange: any = skeleton.getAnimationRange("YBot_Idle");
      let walkRange: any = skeleton.getAnimationRange("YBot_Walk");

      //Speed and Rotation Variables
      let speed: number = 0.03;
      let speedBackward: number = 0.01;
      let rotationSpeed = 0.05;

      //Animation Variables
      let idleAnim: any;
      let walkAnim: any;
      let animating: boolean = false;

      scene.onBeforeRenderObservable.add(()=> {
        let keydown: boolean = false;
        if (keyDownMap["w"] || keyDownMap["ArrowUp"]) {
          mesh.moveWithCollisions(mesh.forward.scaleInPlace(speed));                
          //Previous code
          //mesh.position.z += 0.01;
          //mesh.rotation.y = 0;
          keydown = true;
        }
        if (keyDownMap["a"] || keyDownMap["ArrowLeft"]) {
          mesh.rotate(Vector3.Up(), -rotationSpeed);
          //Previous code
          //mesh.position.x -= 0.01;
          //mesh.rotation.y = 3 * Math.PI / 2;
          keydown = true;
        }
        if (keyDownMap["s"] || keyDownMap["ArrowDown"]) {
          mesh.moveWithCollisions(mesh.forward.scaleInPlace(-speedBackward));
          //Previous code
          //mesh.position.z -= 0.01;
          //mesh.rotation.y = 2 * Math.PI / 2;
          keydown = true;
        }
        if (keyDownMap["d"] || keyDownMap["ArrowRight"]) {
          mesh.rotate(Vector3.Up(), rotationSpeed);
          //Previous code
          //mesh.position.x += 0.01;
          //mesh.rotation.y = Math.PI / 2;
          keydown = true;
        }

        let isPlaying: boolean = false;
        if (keydown && !isPlaying) {
          if (!animating) {
              idleAnim = scene.stopAnimation(skeleton);
              walkAnim = scene.beginWeightedAnimation(skeleton, walkRange.from, walkRange.to, 1.0, true);
              animating = true;
          }
          if (animating) {
            //walkAnim = scene.beginWeightedAnimation(skeleton, walkRange.from, walkRange.to, 1.0, true);
            isPlaying = true;
          }
        } else {
          if (animating && !keydown) {
            walkAnim = scene.stopAnimation(skeleton);
            idleAnim = scene.beginWeightedAnimation(skeleton, idleRange.from, idleRange.to, 1.0, true);
            animating = false;
            isPlaying = false;
          }
   
        }

        //collision
        if (mesh.intersectsMesh(collider)) {
          console.log("Collision detected!");
          increaseScore();
      }
      });
      
      //physics collision
      item = mesh;
      let playerAggregate = new PhysicsAggregate(item, PhysicsShapeType.CAPSULE, { mass: 0 }, scene);
      playerAggregate.body.disablePreStep = false;
     });
    
  //    item.position.y = y;
  //    item.position.z = z;
  //    if (item.position.y < -1) {
  //     if (!gameOver) {
  //         // Display game over text
  //         showGameOverText();
  //         gameOver = true;
  //     }
  // }

    return item;
  }

  function actionManager(scene: Scene){
    scene.actionManager = new ActionManager(scene);

    scene.actionManager.registerAction(
      new ExecuteCodeAction(
        {
          trigger: ActionManager.OnKeyDownTrigger,
          //parameters: 'w'
        },
        function(evt) {keyDownMap[evt.sourceEvent.key] = true; }
      )
    );
    scene.actionManager.registerAction(
      new ExecuteCodeAction(
        {
          trigger: ActionManager.OnKeyUpTrigger
        },
        function(evt) {keyDownMap[evt.sourceEvent.key] = false; }
      )
    );
    return scene.actionManager;
  } 

  //objects
  function createSphere(scene: Scene, x: number, y: number, z: number, scaleFactor: number) {
    const mat = new StandardMaterial("mat");
  const texture = new Texture("https://www.babylonjs-playground.com/textures/fur.jpg");
    let sphere: Mesh = MeshBuilder.CreateSphere("sphere", { });
    mat.diffuseTexture = texture;
    sphere.scaling = new Vector3(scaleFactor, scaleFactor, scaleFactor);
    sphere.position.x = x;
    sphere.position.y = y;
    sphere.position.z = z;
     const sphereAggregate = new PhysicsAggregate(sphere, PhysicsShapeType.SPHERE, { mass: 1 }, scene);
     sphere.material = mat;
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
    return sphere;
  }

  function createSphere1(scene: Scene, rotation: boolean) {
    const mat = new StandardMaterial("mat");
    const texture = new Texture("https://www.babylonjs-playground.com/textures/lava/lavatile.jpg");
    mat.diffuseTexture = texture;
    let sphere1 = MeshBuilder.CreateSphere(
      "sphere",
      { diameter: 2, segments: 32 },
      scene,
    );
    sphere1.position = new Vector3(10, 20, 10);
    sphere1.material = mat;
    
    var alpha = 0;
    scene.registerBeforeRender(function () {
      sphere1.rotation.x += 0.01;
      sphere1.rotation.z += 0.02;
  
      sphere1.position = new Vector3(Math.cos(alpha) * 20, 10, Math.sin(alpha) * 20);
      alpha += 0.01;
  
    });
    
  
    return sphere1;
  }

  function createBox(scene: Scene, width: number) {
    const boxMat = new StandardMaterial("boxMat");
    if (width == 2) {
       boxMat.diffuseTexture = new Texture("https://assets.babylonjs.com/environments/semihouse.png") 
    }
    else {
        boxMat.diffuseTexture = new Texture("https://assets.babylonjs.com/environments/cubehouse.png");   
    }

    //options parameter to set different images on each side
    const faceUV = [];
    if (width == 2) {
        faceUV[0] = new Vector4(0.6, 0.0, 1.0, 1.0); //rear face
        faceUV[1] = new Vector4(0.0, 0.0, 0.4, 1.0); //front face
        faceUV[2] = new Vector4(0.4, 0, 0.6, 1.0); //right side
        faceUV[3] = new Vector4(0.4, 0, 0.6, 1.0); //left side
    }
    else {
        faceUV[0] = new Vector4(0.5, 0.0, 0.75, 1.0); //rear face
        faceUV[1] = new Vector4(0.0, 0.0, 0.25, 1.0); //front face
        faceUV[2] = new Vector4(0.25, 0, 0.5, 1.0); //right side
        faceUV[3] = new Vector4(0.75, 0, 1.0, 1.0); //left side
    }

    const box = MeshBuilder.CreateBox("box", {width: width, faceUV: faceUV, wrap: true});
    box.material = boxMat;
    box.position.y = 0.5;
  //  const boxAggregate = new PhysicsAggregate(box, PhysicsShapeType.BOX, { mass: 1 }, scene);
    return box;
}

  function createRoof(scene: Scene, width: number) {
    const roofMat = new StandardMaterial("roofMat");
    roofMat.diffuseTexture = new Texture("https://assets.babylonjs.com/environments/roof.jpg");

    const roof = MeshBuilder.CreateCylinder("roof", {diameter: 1.3, height: 1.2, tessellation: 3});
    roof.material = roofMat;
    roof.scaling.x = 0.75;
    roof.scaling.y = width;
    roof.rotation.z = Math.PI / 2;
    roof.position.y = 1.22;
    
    return roof;
  }

  function createHouse(scene: Scene, width: number, px: number, py:number, pz:number) {
    const box = createBox(scene, width);
    const roof = createRoof(scene, width);
    const house: any = Mesh.MergeMeshes([box, roof], true, false, undefined, false, true);
    house.position = new Vector3(1, 0, 10);
    const houseAggregate = new PhysicsAggregate(house, PhysicsShapeType.BOX, { mass: 0 }, scene);
    return house;
  }

  function cloneHouse(scene: Scene, Mesh: Mesh,scaleFactor: number) {
    const detached_house = createHouse(scene, 1, 0,0,0,); //.clone("clonedHouse");
    const detached_houseAggregate = new PhysicsAggregate(detached_house, PhysicsShapeType.BOX, { mass: 0 }, scene);
    detached_house.rotation.y = -Math.PI / 16;
    detached_house.position.x = -6.8;
    detached_house.position.z = 2.5;
    detached_house.scaling = new Vector3(scaleFactor, scaleFactor, scaleFactor);
    const semi_house = createHouse(scene, 2,0,0,0); //.clone("clonedHouse");
    semi_house .rotation.y = -Math.PI / 16;
    semi_house.position.x = -4.5;
    semi_house.position.z = 3;
    semi_house.scaling = new Vector3(scaleFactor, scaleFactor, scaleFactor);
    //each entry is an array [house type, rotation, x, z]
    const places: number[] [] = []; 
    places.push([1, -Math.PI / 16, -6.8, 2.5 ]);
    places.push([2, -Math.PI / 16, -4.5, 3 ]);
    places.push([2, -Math.PI / 16, -1.5, 4 ]);
    places.push([2, -Math.PI / 3, 1.5, 6 ]);
    places.push([2, 15 * Math.PI / 16, -6.4, -1.5 ]);
    places.push([1, 15 * Math.PI / 16, -4.1, -1 ]);
    places.push([2, 15 * Math.PI / 16, -2.1, -0.5 ]);
    places.push([1, 5 * Math.PI / 4, 0, -1 ]);
    places.push([1, Math.PI + Math.PI / 2.5, 0.5, -3 ]);
    places.push([2, Math.PI + Math.PI / 2.1, 0.75, -5 ]);
    places.push([1, Math.PI + Math.PI / 2.25, 0.75, -7 ]);
    places.push([2, Math.PI / 1.9, 4.75, -1 ]);
    places.push([1, Math.PI / 1.95, 4.5, -3 ]);
    places.push([2, Math.PI / 1.9, 4.75, -5 ]);
    places.push([1, Math.PI / 1.9, 4.75, -7 ]);
    places.push([2, -Math.PI / 3, 5.25, 2 ]);
    places.push([1, -Math.PI / 3, 6, 4 ]);
    
    const houses: Mesh[] = [];
    
    for (let i = 0; i < places.length; i++) {
      if (places[i][0] === 1) {
          houses[i] = detached_house.createInstance("house" + i);
         // const detached_houseAggregate = new PhysicsAggregate(detached_house, PhysicsShapeType.BOX, { mass: 1 }, scene);
          
      }
      else {
          houses[i] = semi_house.createInstance("house" + i);
          //const semi_houseAggregate = new PhysicsAggregate(semi_house, PhysicsShapeType.BOX, { mass: 1 }, scene);
      }
        houses[i].rotation.y = places[i][1];
        houses[i].position.x = places[i][2];
        houses[i].position.z = places[i][3];
        const housesAggregate = new PhysicsAggregate(houses[i], PhysicsShapeType.BOX, { mass: 0 }, scene);
        
    }
    
    return houses;
  }


//terrain+skybox+ground

  function createTerrain(scene: Scene) {
    const largeGroundMat = new StandardMaterial("largeGroundMat");
    largeGroundMat.diffuseTexture = new Texture("https://www.babylonjs-playground.com/textures/lava/lavatile.jpg");
    const largeGround = MeshBuilder.CreateGroundFromHeightMap(
      "largeGround",
      "https://assets.babylonjs.com/environments/villageheightmap.png",
      { width: 150, height: 150, subdivisions: 20, minHeight: -0.01, maxHeight: 9.99 }
    );
    largeGround.material = largeGroundMat;
    return largeGround;
  }
  

  function createGround(scene: Scene) {
    const groundMat = new StandardMaterial("groundMat");
    groundMat.diffuseTexture = new Texture("https://assets.babylonjs.com/environments/villagegreen.png");
    groundMat.diffuseTexture.hasAlpha = true;
    const ground: Mesh = MeshBuilder.CreateGround("ground", {height: 28, width: 24, subdivisions: 4});
    const groundAggregate = new PhysicsAggregate(ground, PhysicsShapeType.BOX, { mass: 0 }, scene);
    ground.material = groundMat;
     ground.receiveShadows = true;
    return ground;
  }

  function createFootballPitch(scene: Scene, size: number = 10, width: number = 10,  position: Vector3 = Vector3.Zero()) {
    const groundMat = new StandardMaterial("groundMat");
    groundMat.diffuseTexture = new Texture("https://t4.ftcdn.net/jpg/04/40/51/03/360_F_440510369_R1T9gwH1ZkpSBCjYDg47X2AhfL0AOOWf.jpg");
    groundMat.diffuseTexture.hasAlpha = true;

    const ground1: Mesh = MeshBuilder.CreateGround("ground1", { height: size, width: width, subdivisions: 4 }, scene);
    ground1.material = groundMat;

    // Set the position of the ground
    ground1.position = position;

    const ground1Aggregate = new PhysicsAggregate(ground1, PhysicsShapeType.BOX, { mass: 0 }, scene);
    return ground1;
}

  function createSkybox(scene: Scene) {
    //Skybox
    const skybox = MeshBuilder.CreateBox("skyBox", {size:150}, scene);
	  const skyboxMaterial = new StandardMaterial("skyBox", scene);
	  skyboxMaterial.backFaceCulling = false;
	  skyboxMaterial.reflectionTexture = new CubeTexture("textures/skybox", scene);
	  skyboxMaterial.reflectionTexture.coordinatesMode = Texture.SKYBOX_MODE;
	  skyboxMaterial.diffuseColor = new Color3(0, 0, 0);
	  skyboxMaterial.specularColor = new Color3(0, 0, 0);
	  skybox.material = skyboxMaterial;
    return skybox;
  }

// goal posts 
function createGoalPosts1(scene: Scene) {
  const goalPostHeight = 3;
  const goalPostWidth = 0.2;
  const goalPostDepth = 0.2;
  const GoalPost1 = MeshBuilder.CreateBox("GoalPost1", { height: goalPostHeight, width: goalPostWidth, depth: goalPostDepth }, scene);
  GoalPost1.position = new Vector3(-11.5,0,-7); // Adjusted position
  const GoalPost1Physics = new PhysicsAggregate(GoalPost1, PhysicsShapeType.BOX, { mass: 0 }, scene);
  
  return GoalPost1;
}

function createGoalPosts2(scene: Scene) {
  const goalPostHeight = 3;
  const goalPostWidth = 0.2;
  const goalPostDepth = 0.2;
  const GoalPost2 = MeshBuilder.CreateBox("GoalPost2", { height: goalPostHeight, width: goalPostWidth, depth: goalPostDepth }, scene);
  GoalPost2.position = new Vector3(-11.5,0,-9);
  const GoalPost2Physics = new PhysicsAggregate(GoalPost2, PhysicsShapeType.BOX, { mass: 0 }, scene);

  return GoalPost2;
}
  
function createGoalPosts3(scene: Scene) {
  const goalPostHeight = 3;
  const goalPostWidth = 0.2;
  const goalPostDepth = 0.2;
  const GoalPost3 = MeshBuilder.CreateBox("GoalPost3", { height: goalPostHeight, width: goalPostWidth, depth: goalPostDepth }, scene);
  GoalPost3.position = new Vector3(-0.5,0,-9); // Adjusted position
  const GoalPost3Physics = new PhysicsAggregate(GoalPost3, PhysicsShapeType.BOX, { mass: 0 }, scene);
  
  return GoalPost3;
}

function createGoalPosts4(scene: Scene) {
  const goalPostHeight = 3;
  const goalPostWidth = 0.2;
  const goalPostDepth = 0.2;
  const GoalPost4 = MeshBuilder.CreateBox("GoalPost4", { height: goalPostHeight, width: goalPostWidth, depth: goalPostDepth }, scene);
  GoalPost4.position = new Vector3(-0.5,0,-7);
  const GoalPost4Physics = new PhysicsAggregate(GoalPost4, PhysicsShapeType.BOX, { mass: 0 }, scene);

  return GoalPost4;
}


  //lights and camera
  function createHemiLight(scene: Scene) {
    const light = new HemisphericLight("light", new Vector3(0, 1, 0), scene);
    light.intensity = 0.8;
    return light;
  }

  function createArcRotateCamera(scene: Scene) {
    let camAlpha = -Math.PI / 2,
      camBeta = Math.PI / 2.5,
      camDist = 10,
      camTarget = new Vector3(0, 0, 0);
    let camera = new ArcRotateCamera(
      "camera1",
      camAlpha,
      camBeta,
      camDist,
      camTarget,
      scene,
    );
    camera.attachControl(true);
    return camera;
  }
  //----------------------------------------------------------
```
# Render List (bottom section)
```typescript
  //----------------------------------------------------------
  //BOTTOM OF CODE - MAIN RENDERING AREA FOR YOUR SCENE
  export default function GameScene(engine: Engine) {
    interface SceneData {
      scene: Scene;
      box?: Mesh;
      sphere?: Mesh;
      ground?: Mesh;
      ground1?: Mesh;
      largeGround?: Mesh;
      importMesh?: any;
      tree?: Sprite;
      GoalPost1?: Mesh;
      GoalPost2?: Mesh;
      GoalPost3?: Mesh;
      GoalPost4?: Mesh;
      GoalPost5?: Mesh;
      GoalPost6?: Mesh;
      actionManager?: any;
      skybox?: Mesh;
      light?: Light;
      hemisphericLight?: HemisphericLight;
      camera?: Camera;
      sphere1?: Mesh;
      
      
    }
  
    let that: SceneData = { scene: new Scene(engine) };
    that.scene.debugLayer.show();
    //initialise physics
    that.scene.enablePhysics(new Vector3(0, -9.8, 0), havokPlugin);

    //buttons
    const advancedTexture = GUI.AdvancedDynamicTexture.CreateFullscreenUI("UI");
    let reloadButton = createReloadButton(that.scene, "Reload", "Reload", "-500px", "-280px", advancedTexture);
    let button1 = createSceneButton(that.scene, "but1", "Menu", "-500px", "-280px", advancedTexture);
    let scoring = createScoring(that.scene,);
    //let gameOverText = showGameOverText(that.scene);
    //objects
    that.house = cloneHouse(that.scene, 0,1.1);
    that.box = createSphere(that.scene, 2, 2, 2,0.5);
    that.sphere1 = createSphere1(that.scene, true);

    //goal posts
    that.GoalPost1 = createGoalPosts1(that.scene);
    that.GoalPost2 = createGoalPosts2(that.scene);
    that.GoalPost3 = createGoalPosts3(that.scene);
    that.GoalPost4 = createGoalPosts4(that.scene);

    //grounds + skybox + terrain
    that.ground = createGround(that.scene);
    that.ground1 = createFootballPitch(that.scene, 10, 12, new Vector3(-6, 0.01, -8));
    that.largeGround = createTerrain(that.scene);
    that.skybox = createSkybox(that.scene);

    //player
    that.importMesh = importPlayerMesh(that.scene, that.box, 0, 0, 0.8,0,0,5);
    that.actionManager = actionManager(that.scene);
    
    
    //Scene Lighting & Camera
    that.hemisphericLight = createHemiLight(that.scene);
    that.camera = createArcRotateCamera(that.scene);

    return that;
  }
  //----------------------------------------------------
```