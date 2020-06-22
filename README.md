## README

*Game name: Huoxialai*

Development members: Jiang Li, Xia Gong, Qinhang Li

#### Introduction

This is a survival action game. Enemies, weapons and props are distributed in the game scene. The player need to pick up weapons or props to attack or protect itself. The game is designed with a safe zone, and characters will continuously get hurt when outside this zone. The player wins after defeating all enemies. If the player's health is damaged to 0, the game is lost.

#### Demonstration

* The player is idling in the scene, with a wrench holding in his hand.

  ![idle](/Users/jiangli/Desktop/huoxialai github/DemoRecordings/idle.gif)

* This is how the game starts.

  ![start_scene](/Users/jiangli/Desktop/huoxialai github/DemoRecordings/start_scene.gif)

* Player and NPCs can pick up weapons to attack others or take drug to cure themselves.

  ![fight](/Users/jiangli/Desktop/huoxialai github/DemoRecordings/fight.gif)

* Magic attack is available!

  ![magic_attack](/Users/jiangli/Desktop/huoxialai github/DemoRecordings/magic_attack.gif)

* Your blood will decrease when standing outside the safezone.

  ![outside_safezone](/Users/jiangli/Desktop/huoxialai github/DemoRecordings/outside_safezone.gif)

* The game ends when you die

  ![lose_scene](/Users/jiangli/Desktop/huoxialai github/DemoRecordings/lose_scene.gif)

  

#### Scripts

* GameManager.cs  // Compute global static variables and control swiching scenes
* Sound/SoundManager.cs  // Control playing audios

* Environment/Environment.cs  // Generate environments and safe zone

* NPC/NPCMovement.cs  // Control NPC movements, states, health bar, death, AI, etc.

* NPC/predictPlayerMovement.cs  // For NPC to predict player's movement
* Player/PlayerMovement.cs  // Control player movements, states, health bar, death
* UI/GameDisplay.cs  // UI of game scene
* UI/LoseDisplay.cs  // UI of lose scene
* UI/StartDisplay.cs  // UI of start scene
* UI/WinDisplay.cs  // UI of win scene
* Weapons/Drug.cs  // Function drug
* Weapons/Wrench.cs  // Control the weapon functions, pick up or attack, animation, etc.

#### Responsibilities

* **Jiang Li**

  I mainly worked on the design of game rules and mechanics, as well as implementing the basic logics of the game, participating in making game object functions, animations, UI and audios.

  Here're the scripts I wrote:

  * Environment/Environment.cs
    * GenerateWeaponsOnGround(int amount)  // Generate weapons on the ground
    * GenerateNPCsOnGround(int amount)  // Generate NPCs on the ground
    * PoisonCircle()  // Shrink the safe zone circle randomly
  * NPC/NPCMovement2.cs
    * RandomDirectionChanged()  // Change direction randomly
    * DeathEffect()  // Generate bone after death, destroy itself
    * updateHealthBar()  // Update health bar
    * getSafeZoneCoord()  // Decrease health when outside safe zone
    * Jump()  // Implement the NPC's jumping physics with Euler ODE
    
  * Player/PlayerMovement.cs
      * Update()  // Keyboard control
      * Jump()  // Implement the player's jumping physics with Euler ODE
      * DeathEffect()  // Generate bone after death, destroy itself
      * updateHealthBar()  // Update health bar
      * CheckInSafeZone()  // Check if player is outside safe zone, lose health and set alert
  * Weapons/Wrench.cs
    * OnTriggerEnter(Collider other)  // Attack event
    * OnCollisionEnter(Collision other)  // Pick up or attack events
    * PlayAnimation()  // play animation of specified weapon
  * Weapons/Drug.cs
  * Sound/SoundManager.cs
  * UI/GameDisplay.cs
  * UI/LoseDisplay.cs
  * UI/StartDisplay.cs
  * UI/WinDisplay.cs
  
* **Xia Gong**

  I'm responsible for weapons and animations of the players and NPCs. I searched for the materials and animations that can be use to perform an attacking action for the player and NPCs. Also I'm responsible for the in-game animation system.

  Here're the scripts I wrote:

  * NPC/NPCMovement.cs  and Player/PlayerMovement.cs
    * Throw() // perform throwing action
    * Cast() // perform magic casting action
    * getHurt() // get hurt and lose health
    * hurt() // an coroutine that display the hurt animation
  * Weapons/Wrench.cs  // Control the weapon functions, pick up or attack, animation, etc.
    * GetAttackMode() // Returns if the weapon is being  used to attack
    * RangeAttack() // Perform magic Attack
    * selectTarget() // Find nearest target around the weapon holder to attack
    * ThrowMe() // Start a throwing status of a throwing star
  
* **Qinhang Li**

    I'm responsible for the movement of NPCs and AI for NPC to predict player's movement.  Also, I am responsible for finding the asset of the game scene and generate them and participating in making the audio part. 

    And I am also responsible for recoding the video, and the narrative of the video.

    * Environment/Environment.cs
      
      *  Generate() //Generate the ground(i.e. the mountains)
      *  GenerateNatureObjects(int amount) //Generate trees, grass, etc.
      
    * NPC/NPCMovement.cs

      * increaseWeaponNum() //increase number of weapons that NPC is holding
      * decreaseWeaponNum() //decrease number of weapons that NPC is holding
      * findNearByWeaponIndex() //return -1 if no weapon nearby, or the index of the weapon
      * getNearByWeaponByIndex() //get the weapom object that the NPC find.
      * NPCMovementWhenOutsideofSafeZone(Vector3 safeZonePos) //control the movement of NPC when is get outside of the safe zone
      * NPCMovementNoWeapon(float distanceToPlayer) //control the movement of NPC when it doesn't hold any weapon
      * NPCMoveMentWithWeapon(flaot distanceToPlayer) //control the movement of NPC when it holds a weapon
      * getSafeZoneCoord() //get the center coordniate of the safe zone
      * ManagerNPCPosQueue(Vector3 NPCPos) //store the movement of NPC
      * ManagePlayerPosQueue(int index, int method) //store the movement of player when the NPC sees the player
      * NPCIsStuck() //check if NPC got stucked
      * predict(List<float> playerCoordnate, int num) //Call functions in the predictPlayerMovement.cs to predict player's movement.

    * NPC/predictPlayerMovement.cs

      This cs file implements a polynomical regression, to predict the movement of the player.

      To predict, call the function:

      ```
      predictMovement(List<float> arrY, int length, int dimension, int num);
      arrY: player's coordinate
      length: length of the input data
      dimension: the dimension of the poly
      num: the predicted coordinate at time t.
      ```


\* Some functions are written by one more group members. So it's hard to distinguish them all.

