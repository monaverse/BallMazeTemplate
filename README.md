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

This object can have a mesh and should represent the outer shell of the maze.

- Max Size: x 8m, y 8m, z 2m
- Scale: x=1, y=1, z=1
- Location: x=0, y=0, z=0
- Rotation: x=0, y=0, z=0

<img src="https://github.com/user-attachments/assets/e8f0f923-f45e-4d37-9fc5-a6e9c3c81fe8" alt="BallMaze" width="200" />

