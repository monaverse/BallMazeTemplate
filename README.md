# BallMazeTemplate

The example blender files in this project serve as a guide to making playable Maze 3d glb objects.

These objects can then be minted and played on the webgl based Maze Game hosted at: [https://monaverse.com/play/ball-maze](https://monaverse.com/play/ball-maze)

This guide will teach you the specifications of a maze glb that make it compatible with the game.

## Installation

To get started, make sure you have Blender 4.1 or later installed!

## Table of Contents

* [Object Hierarchy](#object-hierarchy)
* [Exporting a Maze](#exporting-a-maze)
* [Testing a Maze](#testing-a-maze)
* [Minting a Maze](#minting-a-maze)

### Object Hierarchy

When the Ball Maze game loads a maze glb, it looks for a specific object hierarchy to attach scripts, add physics colliders, and size the ball appropriately. This automation makes a plain 3d maze object playable!

```
├── BallMaze
│   ├── Ball
│   ├── BoardX
│   │   ├── BoardY
│   │   │   ├── BoardFloor
│   │   │   ├── Goal.Empty
│   │   │   ├── SpawnPoint.Empty
│   │   │   ├── Hole.Empty
│   │   │   ├── Wall
│   │   │   ├── Ramp
│   │   │   └── OuterWall
│   │   ├── AxisY
│   │   └── AxisX
```
---

#### BallMaze

This object can have a mesh and should represent the outer shell of the maze. It will NOT receive a collider.

- Max Size: `x=8m,y=8m,z=2m`
- Scale: `x=1,y=1,z=1`
- Location: `x=0,y=0,z=0`
- Rotation: `x=0,y=0,z=0`

<img src="https://github.com/user-attachments/assets/e8f0f923-f45e-4d37-9fc5-a6e9c3c81fe8" alt="BallMaze" width="200" />

#### Ball

This object should be a sphere with a diameter of 1m, the scale of this object determines the size of the ball in the game.

- Size: `x=1m,y=1m,z=1m`
- Scale: `x=1,y=1,z=1`

<img src="https://github.com/user-attachments/assets/ed1f7052-23c5-41f4-9d01-8cf0ff8f697e" alt="Ball" width="200" />

#### BoardX

This object can have a mesh and should represent the outer ring of the maze floor. It will NOT receive a collider.

- Scale: `x=1,y=1,z=1`
- Rotation: `x=0,y=0,z=0`
  - The game will rotate the board around the local y axis at a range of -5 to 5 degrees when the user moves horizontally.
- Origin: the game will pivot the board at this point.

<img src="https://github.com/user-attachments/assets/2199bca0-03cd-4f12-8be7-f90a4b091d02" alt="BoardX" width="200" />

#### BoardY

This object does not require a mesh, instead all the floors, walls, ramps, holes, spawnpoint, and goal rotate with it.

It will NOT receive a collider, but its children will. 

Make sure that there are walls that surround the maze floor to prevent the ball from rolling off the board.

- Scale: `x=1,y=1,z=1`
- Rotation: `x=0,y=0,z=0`
  - The game will rotate the board around the local x axis at a range of -5 to 5 degrees when the user moves vertically.
- Origin: `x=0,y=0,z=0` (!important)

<img src="https://github.com/user-attachments/assets/0d45a4f8-99b9-47df-9595-ac52e892210c" alt="BoardY" width="200" />

#### BoardFloor

This object must contain the word `BoardFloor` in its name.

It will receive a Box Collider

This object will have holes punched in it. Note that since it receives a Box Collider, the ball would roll right over the holes were it not for the `Hole.Empty` objects, which are described in the next section.

- Scale: `x=1,y=1,z=1`
- Rotation: `x=0,y=0,z=0`

<img src="https://github.com/user-attachments/assets/4b55bac4-0714-4def-beca-d431b881e162" alt="BoardFloor" width="200" />

#### Hole.Empty

There should be one `Hole.Empty` object for each hole on the board. 

Each `Hole.Empty` object must contain `Hole` in the name.

It will receive a small sphere Trigger that detects when the ball enters it.

- Scale: the scale should be relative to 1.0 == 1meter
  - for example, a hole with a .3m diameter should have a cooresponding `Hole.Empty` with a scale of `x=.3,y=.3,z=.3`
- Rotation: `x=0,y=0,z=0`
- Origin: the origin of each `Hole.Empty` should be at the center of the geometry of each hole on the `BoardFloor`

<img src="https://github.com/user-attachments/assets/9c05cdbf-067e-4178-b4e1-a5e7c00a9263" alt="Hole.Empty" width="200" />

#### Goal.Empty

There should be one `Goal.Empty` object at the end of the maze. 

The `Goal.Empty` object must contain `Goal` in the name.

It will receive a small box Trigger that detects when the ball enters it.

- Scale: the scale should be relative to 1.0 == 1meter

<img src="https://github.com/user-attachments/assets/fed28f2d-5901-422d-8e93-64401f3572b6" alt="Goal.Empty" width="200" />

#### SpawnPoint.Empty

There should be one `SpawnPoint.Empty` object at the start of the maze. 

The `SpawnPoint.Empty` object must contain `SpawnPoint` in the name.

This object should contain a mesh that marks the start of the maze.

- Scale: `x=1,y=1,z=1`
- Origin: the ball with be spawned at the origin of this object.

<img src="https://github.com/user-attachments/assets/24ad1905-7186-47d6-98ee-d13051bd6265" alt="SpawnPoint.Empty" width="200" />

#### Ramp

Ramps receive a convex mesh collider. This allows them to serve as wedge shaped ramps or walls in the maze.

The collider will follow the contours of the mesh, keep them simple and make sure there are not concave surfaces. (eg. a cheese wedge is convex, a crescent moon shape is concave)

A `Ramp` object must contain `Ramp` in the name.
- Scale: `x=1,y=1,z=1`

<img src="https://github.com/user-attachments/assets/b5db4028-af13-4436-9a7d-63adce49da2d" alt="Ramp" width="200" />

#### Wall

Walls receive a box collider. This allows them to serve as simple platforms and walls in the maze.

A `Wall` object must contain `Wall` in the name.

- Scale: `x=1,y=1,z=1`
<img src="https://github.com/user-attachments/assets/9324b8f7-3490-4a41-9f3e-b98dc8da414e" alt="Wall" width="200" />

#### OuterWall

OuterWalls receive a box collider. This allows them to serve as an outer wall for the `BoardFloor`

An `OuterWalls` object must contain `Wall` in the name.

- Scale: `x=1,y=1,z=1`
  
<img src="https://github.com/user-attachments/assets/ff9726b3-d609-4946-bc89-e8e101edf479" alt="OuterWall" width="200" />

#### Axis

`Axis` meshes are for decoration, they should rotate around the axes of `BoardX` and `BoardY`

<img src="https://github.com/user-attachments/assets/8b99cc30-2ec9-411f-9ee3-9dace0b8b5d8" alt="Axis" width="200" />

---

### Exporting A Maze

We'll be exporting this maze as a GLB file.

To begin, right click on the `BallMaze` object in your scene hierarchy and select `Select Hierarchy`

<img src="https://github.com/user-attachments/assets/f59dbae8-71d7-4850-b64b-e2c582d4a877" alt="Select Hierarchy" width="300" />

All of your objects should now be selected.

<img src="https://github.com/user-attachments/assets/8c3f30f3-6645-4cdb-a8c6-0a1905e2e770" alt="Selected Objects" width="300" />

From your `File` menu, select `Export/glTF (2.0) (.glb/.gltf)`

<img src="https://github.com/user-attachments/assets/9395117c-652e-4555-a57b-b2ee579b16fd" alt="Selected Objects" width="300" />

In the export panel, make sure `Format` is `gltfBinary (.glb)` is selected. This will export one `.glb` file with materials and textures packed inside.

Make sure to also select `Include\Selected Objects` and `Mesh\Apply Modifiers` (if you used modifiers to punch out holes)

<img src="https://github.com/user-attachments/assets/ababb45d-8c28-4147-8b82-df259b51e10b" alt="Export Panel" width="300" />

Fill out your file name and complete the export.

---

### Testing A Maze

To test a maze, upload it to a web server.  I typically use a pinning service like `Pinata` to host my files.

I right click on the uploaded file and select `copy the link address`.

<img src="https://github.com/user-attachments/assets/b29194b0-0dd2-42ae-85f9-ddc3150e9990" alt="Export Panel" width="300" />

Load the game up in your desktop browser, hold the `p` key and while holding the `p` key, press the `o` key. This allows you to load a glb manually.

Paste the url to your glb file into the prompt and wait for it to load.

<img src="https://github.com/user-attachments/assets/3b35f22b-3d33-4146-b459-fa7e1c4fba90" alt="Manually Load Maze" width="300" />

If all goes well you should be able to play your maze! If not, then review the specs above or reach out to me on the MONA Discord to troubleshoot.

---

### Minting A Maze

I'll compile a tutorial for setting up a contract on `manifold.xyz` later, but for now if you have a preferred contract provider, make sure that when you mint the object, you mint the glb file and add the following trait to the token:

Trait: "3D Object Type"
Value: "Ball Maze"

Then register your contract with us on the MONA marketplace by reaching out on the MONA discord.

Once your contract is listed, the Ball Maze game will allow other players who own the token to load it into their games!
