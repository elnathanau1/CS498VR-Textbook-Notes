# Chapter 3
## The Geometry of Virtual Worlds

### 3.1 Geometric models
- 3D Euclidean space w/ Cartesion coordinates
  - let R³ denote real world, using (x,y,z)
<br><br>
- __Data Structures__
  - Geometric models usually encoded in clever data structures
    - __Doubly connected edge list__ aka __Half-edge data structure__
      - Three kinds of data elements: _faces_, _edges_, and _vertices_
      - represent 2, 1, and 0-dimensional parts of model
      - ![](assets/Chapter-3-Notes-dcaf99cb.png)
        - <small>Figure 3.3: Part of double connected edge list shown for face w/ five edges on boundary. Each half-edge structure _e_ stores pointers to the next and prev edges along face boundary. Also stores pointer to its twin half-edge, which is part of boundary of adjacent face)<small>
<br><br>
- __Inside vs. outside__
  - _Q: is object interior part of model?_
  - __Coherent model__: If model inside were filled w/ gas, could not leak
  - __Polygon soup__: Jumble of triangles that do not fit together nicely, could even have intersecting interiors
<br><br>
- __Why triangles?__
  - Triangles used because simplest for algorithms
<br><br>
- __Stationary vs. movable models__
- 
