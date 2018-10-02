# Chapter 3
## The Geometry of Virtual Worlds

### 3.1 Geometric models
- 3D Euclidean space w/ Cartesion coordinates
  - let R³ denote real world, using (x,y,z)
<br>
- __Data Structures__
  - Geometric models usually encoded in clever data structures
    - __Doubly connected edge list__ aka __Half-edge data structure__
      - Three kinds of data elements: _faces_, _edges_, and _vertices_
      - represent 2, 1, and 0-dimensional parts of model
      - ![](assets/Chapter-3-Notes-dcaf99cb.png)
        - <small>Figure 3.3: Part of double connected edge list shown for face w/ five edges on boundary. Each half-edge structure _e_ stores pointers to the next and prev edges along face boundary. Also stores pointer to its twin half-edge, which is part of boundary of adjacent face)<small>
<br>
- __Inside vs. outside__
  - _Q: is object interior part of model?_
  - __Coherent model__: If model inside were filled w/ gas, could not leak
  - __Polygon soup__: Jumble of triangles that do not fit together nicely, could even have intersecting interiors
<br>
- __Why triangles?__
  - Triangles used because simplest for algorithms
<br>
- __Stationary vs. movable models__
  - Two kinds of models:
    1. __Stationary models__: keep same coordinates forever
      - <small>ex: streets, floors, buildings<small>
    2. __Movable models__: can be _transformed_ into various positions and orientations
      - <small>ex: vehicles, avatars<small>
  - Motion can be caused either by
    1. tracking system (model match user's motions)
    2. controller
    3. laws of physics in virtual world
<br>
- __Choosing coordinate axes__
  - Don't be stupid.
<br>
- __Viewing the models__
  - _Q: How is model going to "look" when viewed on display?_
  - Two parts:
    1. Determining where points in virtual world should display
    2. How each part of model should appear after lighting sources and surface properties defined in virtual world

### 3.2 Changing Position and Orientation
