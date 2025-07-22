# Maze Solver Using DSA

This project solves mazes using **DFS, BFS, A\***, and **Dijkstra's Algorithm**.  
It demonstrates pathfinding techniques and compares their performance on different maze sizes and configurations.

---

## Contents
- **MazeSolver.java**: Main program implementing four pathfinding algorithms.
- **requirements.txt**: Environment and setup requirements.
- **screenshots/**: Maze images and visualized paths.
- **Documentation/**: Project report and presentation slides.
- **video_demo/**: Demo video showcasing the project.

---

## Features
- Implements **DFS, BFS, A\***, and **Dijkstra** for maze solving.
- Prints the maze with the **shortest path highlighted**.
- Simple console-based interaction for algorithm selection.
- Easily extendable to add new algorithms or maze types.

---

## Algorithms Implemented
- **Depth First Search (DFS)** – explores paths by going as deep as possible.
- **Breadth First Search (BFS)** – explores paths layer by layer.
- **A\*** – uses heuristics for faster pathfinding.
- **Dijkstra's Algorithm** – finds the shortest path based on cost.

---

## Usage
1. Compile and run the program:
    ```
    javac MazeSolver.java
    java MazeSolver
    ```
2. Choose your preferred algorithm from the menu.
3. View the computed path in the console output.

---

## Screenshots

| **Maze Input** | **Path Found (DFS)** |
|----------------|----------------------|
| ![Maze Input](screenshots/maze_input.png) | ![DFS Path](screenshots/maze_dfs.png) |

| **Path Found (BFS)** | **Path Found (Dijkstra)** |
|----------------------|---------------------------|
| ![BFS Path](screenshots/maze_bfs.png) | ![Dijkstra Path](screenshots/maze_dijkstra.png) |

---

## Documentation & Demo Video
- **[Project Report](Documentation/maze.docx)**
- **[Project Presentation](Documentation/MAZE%20SOLVER.pptx)**
- **[Demo Video](video_demo/mazesolverdemovideo.mp4)**

---

## Requirements
- Java JDK 11 or later
- Any IDE or terminal that supports compiling and running Java code
