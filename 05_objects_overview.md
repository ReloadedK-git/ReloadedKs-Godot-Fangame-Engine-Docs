# Objects overview

This section will give a short overview of each object inside the engine (what they are and do).

It's a text-heavy section and using any search function (usually Ctrl + F) to quickly locate the object you want to know about is recommended. Objects will appear in the same order as in the engine.

---

### objBackgroundMenus:

Specific type of background used only for the main menus. It has a constant scroll offset with a speed of -80.

### objBackgroundColor:

Simple type of background which is basically a colored rectangle that can be stretched. It has a default hex value of **d6cabe**.

### objBackgroundScrolling

A generic parallax background. You can set the background's properties directly from the editor.

1. Parallax_amount: defines the amount of "parallax motion". To give a sense of distance, lower values are usually better.
2. Background_size: extends the background so it can repeat itself, either vertically or horizontally. You need to set the background's exact size.
3. Background_index: the texture/background you want to use.

### objBackgroundTexture

Background which uses a repeating texture. This texture can be changed from the node's properties, and can be stretched if needed.

---

### objCollectableItem

A generic collectable item. It detects if it was collected previously, in which case it destroys itself. If not, it will store its "item_name key" inside of GLOBAL_SAVELOAD's dictionary when colliding with the player object.

---

### dialogTesting01

Object used to demonstrate how the dialog system works.

### objDialogBox

The core of the dialog system. A very complex object which does many things:

* Freezes the player.
* Shows a portrait of the character which is currently talking.
* Includes a "typewritter" effect.
* Allows text and dialog skipping (by pressing the jump_button and shoot_button, respectively).
* Unfreezes the player and destroys itself when finished.

This dialog system was made from scratch with ease of use in mind. By using exported properties, you can edit the text and portrait images inside of the node editor's properties. Once edited, you can make a copy of your custom dialog and spawn it when you need. An example of this is found in the next object, objSign.

### objSign

A sign which spawns a dialog box when the player collides with it and presses a certain key (button_up, respectively). It indicates what key needs to be pressed when the player is colliding, which also updates according to the input device you're using (keyboard and controller).

---

### objCoin

The classic "Pick all coins to proceed" gimmick. Simple, but surprisingly versatile.

Coins can get picked by the player and, if there's no more coins, will queue_free() a selected scene. This scene will likely be a tilemap (walls or rows of spikes).

### objInvisibleBlock

The classic invisible block. Turns visible as soon as the player touches it.

Due to how Godot handles collisions, using Area2D nodes is not possible. What is used instead is a trick known as "duck typing", which is checking what the player is currently colliding with, getting the collision information, and calling a method if it exists. It's not optimal, but it's a lot cleaner and there are ways to mitigate the amount of processing it requires, like only checking for collisions while invisible and inside of the screen.

### objJumpRefresher

Re-enables double jumping for the player if it detects a collision with it and is currently active. Will also emit some particles when this happens, disabling itself until a timer runs out and re-enables it.

### objMovingBlock

This moving block has a speed vector (x,y) and 3 collision interactions. You set both of them from the inspector properties.

The collision interactions are:

1. ***None:*** Once moved, it never stops
2. ***Stop:*** Stops and snaps after colliding with a platformBlock
3. ***Bounce:*** Reverses its speed after colliding with a platformBlock

It is not strictly necessary, but multiples of 2 work better for collisions when setting the initial move_speed.

### objMovingPlatform

A classic moving platform.

* The player can only stand on it from the top, and will go through it from any other side
* Will give the player infinite djumps as long as it is colliding
* Bounces against invisible platformBlocks. Check the "Tilemaps" folder

### objPhysicsBox

An experimental object which is moved by using Godot's 2D physics engine. It's left unused, as it has some bugs that need fixing, but the core functionality of it does work, so you might want to edit it yourself to suit your needs.

### objWater

Simple water object. It's pretty much just a sprite and a collision shape, since the player handles water by itself. It will also draw itself on top of most gameplay objects.

The way to use this water object is rather simple:

1. Place it where you want to in your level
2. Go to the "Transform" tab in the editor properties and modify the scene's scale
3. Copy it as many times as you see fit.

### tilConveyorBlock

A tilemap which adds horizontal linear velocity to the player. To change this horizontal speed, go to the TileSet properties, Select, Physics, Physics Layer 0 and check the "Linear Velocity" property.

***WARNING:*** If the player is carried by the conveyor but suddently stops when colliding with a regular solid wall, it will return an error. This error is non-intrusive and will not stop your game, but it's annoying and I could not find a proper fix for it, at least not without making the object unnesessarily complex.

### tilPlatformBlock

Tilemap which works as a central part of objMovingBlock, objMovingBlock and objBouncingCherry. Does nothing by itself, other than turning invisible.

### tilVines

Tilemap which gets detected by the player, activating the walljumping gimmick.

---

### objEnemyDummy

A generic enemy, used as a base for more complex enemies. It detects collisions with an attack (player's bullets), losing a pre-defined amount of HP while displaying a visual effect and a sound. If HP is 0 or less, it destroys itself.

### objBouncingCherry

Simple floating cherry with an exported property called "Move Speed". You can edit this and the cherry will move. If it detects a collision with a platformBlock, it will bounce vertically or horizontally depending on how it collided.

### objJumpSwitchSpikeDown / objJumpSwitchSpikeUp

A spike which changes its position smoothly each time the "button_jump" input is detected, and only if the player exists. It can be set to start in a hidden state from the editor's properties.

### tilSpikes

Tilemap of spikes. Made this way instead of using nodes because in fangames they are used a lot.

---

### objBloodEmitter

Visual effect object which indicates when the player dies.

It emits "blood" particles and also has a blinking player sprite. If the autoreload_on setting from GLOBAL_SETTINGS is set to "true", this object can reset automatically (same as pressing R). If autoreload_on is set to "false", this object will show a classic GAMEOVER screen when destroyed.

### objBullet

Classic projectile attack for the player. A lot more complex in design when compared to most fangame engines:

1. It gets created from the player, giving it its horizontal speed and direction
2. Gets its ***attack_type*** and ***attack_damage*** values from ***GlobalClass*** and ***GLOBAL_GAME***, respectively. This allows more complex attack systems and could allow for some basic rpg mechanics.
3. Doesn't get destroyed the frame it touches a block. Instead, it stops its movement for a single frame and then destroys itself, giving a nice visual effect.
4. Can get destroyed either by colliding with something or if its timer runs out (0.4 seconds).
5. Due to how Godot handles collisions, it uses duck typing to collide and call functions from the objects it collided with, if they exist.

### objGameOver

A simple texture which gets displayed on top of the screen, without any special function.

### objJumpParticle

Visual indicator for the player's double jump. Destroys itself as soon as it stops emitting particles.

### objPlayer

This object gets a section dedicated to it, due to its importance. Check that one instead.

---

### objCameraDynamic

Camera which follows another previously defined object. You can set its zoom amount and its limits. Limits define where the camera should stop moving at. Godot doesn't know what "rooms" are, so we have to define them ourselves, unlike Game Maker where you can use built-in functions like room_width and room_height.

### objCameraFixed

Camera which "follows" another previously defined object, in steps of *camera_width* and *camera_height*. You can set its zoom amount and its scrolling speed. Limits are not really needed as long as you design your levels properly (and if you don't, not knowing where your player is because it went outside the limits of your level would look terrible, anyway).

### objMusicPlayer

Used set and play music in your game's rooms. Set its *Song ID* from the editor's properties and the song will play and loop itself. Additionally, you can set where the loop should start and end, in seconds. Songs will only change when their *Song IDs* are different from the previous one.

### objSaveBlocker

Blocks bullets, destroying them but also showing a small visual effect. The bullet's destruction happens on objBullet, this just has the proper collision layer for it to be detected.

### objSavePoint

A classic save point. It has 2 types of interactions:

1. ***With objBullet:*** Saves on collision, as long as the save point is not colliding with objPlayer.
2. ***With objPlayer:*** Checks if objPlayer is touching the save point. If it is, then bullets can no longer save by themselves, but pressing button_shoot will save as long as objPlayer is inside the sprite.

There's no "medium, hard, very hard, impossible". I prefer having a single difficulty setting throughout the game. You can implement them yourself, if you like.

### objWarp

Object used to change levels. It works by colliding with the player, storing its xscale and indicating that the current level is being changed. It can have a warp transition effect and warp the player to a specific point in the room.

---


### objHud

Works as the game's "overlay". If you were to code certain mechanics, like an HP or magic bar, they would go here. In this engine, the HUD is used only as a way to show some extra information when god mode is active.

### objSaveFilePreview

Loads and displays screenshots from your save files. If they don't exist, they show a default "no data" sprite. Only used in the main menu scene.

### objSoundManager

Taken from heartbeast's "Godot pixel platformer tutorial" series.

This autoloaded scene manages everything related to sound effects. It can play up to 8 sound effects at the same time and they don't get cut or interrupted, making it a nice and clean solution. Sounds get preloaded, so there's no need to reload them each time you want to play them. You would instead reference the sound manager and its preloaded sounds.

### objWarpTransition

A simple fade-to-black transition.

Taken from Heartbeast's "Godot 4 Heart Platformer", with some edits. It's an autoloaded object you can reference and call its functions for a fading transition effect.

---

### til16x16

A tilemap made up of tiles 16 pixels in width and height. There's no easy way to change tile dimensions like in Game Maker, so we make different tilemaps instead.

### til32x32

Same as the above, but tiles are 32 pixels in width and height. It includes some basic graphics with collisions already built in and also includes a tilemap made for slopes specifically.

---

### objTrigger

Generic collision trigger. It allows setting the trigger ID directly from the editor's properties. It will hide itself when the game is running, but will allow you to see its ID when placing it on a level.

When a collision with the player is detected, it will:

* Search its value on the global trigger array.
* Add its value to the global trigger array, if it wasn't added before.
* Destroy itself.

***-Full credit to GFX32 for this idea and implementation (besides some small personal edits)***

### objTriggerBlock

A moving block activated by using triggers.

1. Needs a trigger to activate.
2. When triggered, it moves to "target_position", lerping its speed.
3. It also disables its collision shape until it reaches the desired position, to avoid pushing or crushing the player.

This object is meant to be used by ***editing its children nodes***, particularly the "$Target" sprite node. As the name implies, this node's position is used as the target position, which the object will move to.

After placing this object on a room, from the scene tree, right click the object and select the "editable children" option. From there, search for the "$Target" node and move it to the desided position. Thanks to @tool, you'll have some visual feedback which should make setting it easier.

### objTriggerCherry

A simple triggered cherry. You have to define its velocity and trigger ID for it to work, which you can do directly from the editor's node properties.

### objTriggerCherryOrbit

Cherry activated by using the trigger system. This object will orbit around a direction (in this case the player's direction). You need to define a speed (other than 0) and a trigger ID for it to work, which you can do directly from the editor's node properties.

### objTriggerCherryTowards

Cherry activated by using the trigger system. This object will move towards a direction (in this case the player's direction). You need to define a speed (other than 0) and a trigger ID for it to work, which you can do directly from the editor's node properties.

---

### objControlsMenuButton

A type of button used only in the controls menu. If activated, it will wait for an input from the user and assign it to the corresponding *button_action*. It will also display the name of its *button_action* in string form, and will show some visual and sound feedback.

### objGenericMenuButton

A generic button meant to be used in multiple types of menus. It changes colors when focused or unfocused, and plays a button sound when focused.

### objPauseMenu

Stops most of the game's processes (unless defined otherwise), "pausing" everything. Very similar in its functionality to the settings menu, as it also loads and saves data from GLOBAL_SETTINGS, allowing you to change the game's music and sound volume directly. Also allows you to return to the main menu or resume playing.

---

**Previous page: [04. Rooms](04_rooms.md)**

**Next page: [06. The Player](06_the_player.md)**
