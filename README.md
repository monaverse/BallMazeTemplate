# BallMazeTemplate

The example blender files in this project serve as a guide to making playable Maze 3d glb objects.

These objects can then be minted and played on the webgl based Maze Game hosted at: [https://monaverse.com/play/ball-maze](https://monaverse.com/play/ball-maze)

This guide will teach you the specifications of a maze glb that make it compatible with the game.

## Table of Contents

* [Object Hierarchy](#object-hierarchy)
* Exporting a Maze
* Testing a Maze
* Minting a Maze

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

#### BallMaze

This object can have a mesh and should represent the outer shell of the maze. It will NOT receive a collider.

- Max Size: x 8m, y 8m, z 2m
- Scale: x=1, y=1, z=1
- Location: x=0, y=0, z=0
- Rotation: x=0, y=0, z=0

<img src="https://github.com/user-attachments/assets/e8f0f923-f45e-4d37-9fc5-a6e9c3c81fe8" alt="BallMaze" width="200" />

#### Ball

This object should be a sphere with a diameter of 1m, the scale of this object determines the size of the ball in the game.

- Max Size: x=1m, y=1m, z=1m
- Scale: x=1, y=1, z=1

<img src="https://github.com/user-attachments/assets/ed1f7052-23c5-41f4-9d01-8cf0ff8f697e" alt="Ball" width="200" />

#### BoardX

This object can have a mesh and should represent the outer ring of the maze floor. It will NOT receive a collider.

- Scale: x=1, y=1, z=1
- Rotation: x=0, y=0, z=0
  - The game will rotate the board around the local y axis at a range of -5 to 5 degrees when the user moves horizontally.
- Origin: the game will pivot the board at this point.

<img src="https://github.com/user-attachments/assets/2199bca0-03cd-4f12-8be7-f90a4b091d02" alt="BoardX" width="200" />


