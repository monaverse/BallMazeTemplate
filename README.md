# BallMazeTemplate

The example blender files in this project serve as a guide to making playable Maze 3d glb objects.

These objects can then be minted and played on the webgl based Maze Game hosted at: [https://monaverse.com/play/ball-maze](https://monaverse.com/play/ball-maze)

This guide will teach you the specifications of a maze glb that make it compatible with the game.

## Table of Contents

* Object Hierarchy
* Scaling
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
