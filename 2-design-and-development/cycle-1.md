# Cycle 1 - Drawing the initial level

## Design

### Objectives

In this cycle I aim to create a simple level, paste in a character and make it move. I will be doing this in repl.it, and will be using JavaScript with the Kaboom library.&#x20;

* [x] Design the game assets and load them in
* [x] Design a simple level using these assets
* [x] Paste in a character on top of the level

### Usability Features

Visibility - I want to make each object in the game clearly visible and will be doing this by picking colours that contrast to each other. This will help the player to see each object in the game more easily.

### Key Variables/Functions

| Variable name               | Use                                                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| levelconfig                 | Sets the grid size and maps each character to a sprite, giving it specific properties and tags.                    |
| levels                      | An array containing the levels. These levels are built using characters, which are later mapped to sprites/images. |
| background colour           | Sets the colour of the background                                                                                  |
| levelNumber                 | Stores a number that will be used to pick a level from the levels array.                                           |
| game                        | A scene that will run the main game.                                                                               |
| window width, window height | sets the width and height of the game window                                                                       |
| width,height                | Sets the width and height of the game grid                                                                         |

### Pseudocode

The pseudocode for this cycle is shown below

```
import kaboom

background colour = "blue"
set window width to (1000)
set window height to (700)

load in Character.pedit as "Character"
load in Floor.pedit as "Floor"
load in Spike V.pedit as "Spike V"
load in Spike H.pedit as "Spike H"


levels = [
[
  "                                                                       ",
  "                                                         <=============",
  "            +                       +          <==========            ",
  "=========================  ===  =====  =========                       "
  ],
]

levelconfig = {
    set width to 32
    set height to 32

    "=" set to sprite("Floor"){
        area(),
        origin("bottom")
    }
    
    "+" set to sprite("Spike V"){
        area(),
        origin("bottom")
    }

    "o" set to sprite("Character"){
        area(),
        body(),
        origin("bottom")
    }

    "<" set to sprite("Spike H"){
        area(),
        origin("bottom")
    }
}

create game scene(levelnumber = 0){
    level = addlevel(levels[levelnumber], levelconfig)
    player = spawn in "o" at (1,3)
}
```

## Development

Firstly, I imported the kaboom library. This will allow me to use all of the assets available in my game.

```javascript
import kaboom from "kaboom"
```

Then I initialised the context, making the dimensions (700, 1000) and changing the background colour to blue. I feel that these dimensions will suit my game well, and the colour I chose will make the game look brighter and clearer.

```javascript
//initialize context
kaboom({
//Making the bacground blue
  background: [0, 34, 255],
//Setting the screen dimensions
  width: 1000,
  height: 700,
})a
```

I then started drawing some simple shapes and loading them in so that I could use them later on. I created four simple shapes that I thought would be necessary for my level design: the floor, a vertical spike, a horizontal spike and the player character. I ensured that the colours of these sprites contrasted to each other and the background nicely, but didn't look too obscure and unnatural.&#x20;

<figure><img src="../.gitbook/assets/image (5) (2).png" alt=""><figcaption><p>Player Character</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2) (1) (4).png" alt=""><figcaption><p>Floor</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>Vertical Spike</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption><p>Horizontal Spike</p></figcaption></figure>

I then added the load code for each individual sprite, giving each one a unique name.

```javascript
//loading assets
loadPedit("Floor", "sprites/Floor.pedit");
loadPedit("Spike V", "sprites/Spike V.pedit");
loadPedit("Spike H", "sprites/Spike H.pedit");
loadPedit("Character", "sprites/Character.pedit");
```

I then began to design the levels. Kaboom allows you to create a level using characters on the keyboard, and then later assigning each character a sprite or image. I kept this design mostly simple for now, but later on I intend on expanding it and turning it into something more exciting for the user. I also saved the level in a list as this would allow me to add other levels later on or test specific sections of the level I am working on.

```javascript
// Array containing levels
const levels = [
//Initial level
[
  "                                                                       ",
  "                                                         <=============",
  "            +                       +          <==========            ",
  "=========================  ===  =====  =========                       "
  ],
 
]
```

After this I created the level configuration, which is used to map each icon you have used in your level design to a sprite that you have loaded in. In this case I mapped each "=" to my floor tile, each "+" to my vertical spike and each "<" to my horizontal spike. I also mapped the character "o" to my character sprite, however I didn't put this character anywhere in my level design. This is because I intend on pasting in the character later on, as this will make it easier to reference it later on.

<pre class="language-javascript"><code class="lang-javascript"><strong>//Level configuration
</strong><strong>const levelconfig = {
</strong><strong>//Grid dimensions
</strong>  width: 32,
  height: 32,
  pos: vec2(0,400),
  //Player Character configuration
  "o": () => [
    sprite("Character"),
    area(),
    body(),
    origin("bot"),
    scale(2,2)
  ],
  //Floor configuration
  "=": () => [
    sprite("Floor"),
    area(),
    solid(),
    origin("bot")
  ],
  //Vertical spike configuratrion
  "+": () => [
    sprite("Spike V"),
    area(),
    origin("bot") 
  ],
  // Horizontal spike configuration
  "&#x3C;": () => [
    sprite("Spike H"),
    area(),
    origin("bot"),
  ],
 
}

</code></pre>

I also added in tags under each object that gives them specific properties. Anything that is effected by gravity needs to have a body() tag and anything that will be involved in collisions needs an area() tag. The origin() tag determines where the origin of the sprite will be. I set this to "bot" which means the co-ordinate origin of each sprite will be the bottom. I also scaled up the character sprite as when I ran the level it appeared too small initially.

After this I created a game scene. By using scenes it will allow me to create a death screen and a main menu more easily.  I defined a variable called levelNumber when creating the scene. This will allow me to test and add levels more easily later on as I can change what level is being run in the game. Then I added in the level and pasted the character on top.

```javascript
// Creating the main game scene
scene("game", (levelNumber = 0) => {
  // Adding the level in
  const level = addLevel(levels[levelNumber], levelconfig);
  // Adiing in the player character
  const player = level.spawn("o", 1, 3)
  }
```

### Challenges

The main challenge I faced here was trying to re-learn how the kaboom library actually works, and understanding what each section of code does. I used both the kaboom website and a tutorial I found online to help me with this which really helped me in understanding the basics of kaboom.

## Testing

### Tests

| Test | Instructions | What I expect                          | What actually happens | Pass/Fail |
| ---- | ------------ | -------------------------------------- | --------------------- | --------- |
| 1    | Run code     | The level and the character to appear. | As expected           | Pass      |

### Evidence

<figure><img src="../.gitbook/assets/image (1) (4) (1).png" alt=""><figcaption></figcaption></figure>

After running the code this appeared on the screen. Here you can see the character stationary in the level
