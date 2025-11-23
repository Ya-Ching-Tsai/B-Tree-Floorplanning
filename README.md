# B\*-Tree Floorplanning in C++

A C++ implementation of **B\*-tree–based floorplanning**, supporting coordinate packing, contour computation, and module perturbations.  
Given a `.nodes` file and an optional `.perturbation` file, the program constructs a B\*-tree, performs preorder traversal, computes module placement using horizontal contour analysis, and outputs the final `.m` and `.txt` result files.

This project is based on the coursework for **Data Structure HW2** at NCKU, referencing the official homework slides and B\*-tree lecture materials.

---

## Features

### B\*-Tree Construction  
- Reads module information from `.nodes` (name, width, height, parent/child relations).  
- Builds the tree structure where:  
  - **Left child** → module placed to the *right*  
  - **Right child** → module placed *above* (same x-coordinate)  

### Preorder Traversal for Packing  
- Visits nodes in **preorder (VLR)** 
- x-coordinate is determined directly by B\*-tree relations:
   - **Left child**: x = parent_x + parent_width
   - **Right child**: x = parent_x
- y-coordinate is determined by the horizontal contour,taking the maximum contour height over [x, x + width] 

### Horizontal Contour Structure  
- Maintains a list of `(left_x, right_x, height)` intervals  
- Ensures modules are packed compactly without overlap  
- Updates contour dynamically during traversal

### Perturbation Support (Part 2)
Based on `.perturbation` instructions 

- `rotate <module>` — rotate a macro  
- `swap <A> <B>` — swap two nodes  
- (delete/insert exists in B\*-tree theory but not required in HW2)

### 📝 Output Files  
Two formats based on homework specifications

- `.m` — module coordinates in required format  
- `.txt` — module name + bottom-left corner (x, y) in `.nodes` order

---

## Input Format

### 1. **nodes file (`*.nodes`)**
Contains:
- Module name  
- Width & height  
- Parent, left child, right child  
- `X` means NULL  

### 2. **perturbation file (`*.perturbation`)** (Part 2 only)
Examples:
