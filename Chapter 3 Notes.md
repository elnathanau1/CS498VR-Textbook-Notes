# Chapter 3
## The Geometry of Virtual Worlds

### 3.1 Geometric models
- 3D Euclidean space w/ Cartesion coordinates
  - let R³ denote real world, using (x,y,z)


- __Data Structures__
  - Geometric models usually encoded in clever data structures
    - __Doubly connected edge list__ aka __Half-edge data structure__
      - Three kinds of data elements: _faces_, _edges_, and _vertices_
      - represent 2, 1, and 0-dimensional parts of model
      - ![](assets/Chapter-3-Notes-dcaf99cb.png){ width=50% }
        - <small>Figure 3.3: Part of double connected edge list shown for face w/ five edges on boundary. Each half-edge structure *e* stores pointers to the next and prev edges along face boundary. Also stores pointer to its twin half-edge, which is part of boundary of adjacent face)</small>


- __Inside vs. outside__
  - _Q: is object interior part of model?_
  - __Coherent model__: If model inside were filled w/ gas, could not leak
  - __Polygon soup__: Jumble of triangles that do not fit together nicely, could even have intersecting interiors


- __Why triangles?__
  - Triangles used because simplest for algorithms


- __Stationary vs. movable models__
  - Two kinds of models:
    1. __Stationary models__: keep same coordinates forever
        - <small>ex: streets, floors, buildings</small>
    2. __Movable models__: can be _transformed_ into various positions and orientations
        - <small>ex: vehicles, avatars</small>
  - Motion can be caused either by
    1. tracking system (model match user's motions)
    2. controller
    3. laws of physics in virtual world


- __Choosing coordinate axes__
  - Don't be stupid.


- __Viewing the models__
  - _Q: How is model going to "look" when viewed on display?_
  - Two parts:
    1. Determining where points in virtual world should display
    2. How each part of model should appear after lighting sources and surface properties defined in virtual world

### 3.2 Changing Position and Orientation
- Suppose movable model defined as mesh of triangles. To move, _apply single transformation to every vertex of every triangle_


- __Translations__
  - Consider triangle:
  $((x_1,y_1,z_1), (x_2,y_2,z_2), (x_3,y_3,z_3))$

  - Let $x_t, y_t, z_t$ be amount we want to change triangle's position. __Translation__ given by:


  $$(x_1,y_1,z_1) \rightarrow (x_1 + x_t, y_1 + y_t, z_1 + z_t)$$
  $$(x_2,y_2,z_2) \rightarrow (x_2 + x_t, y_2 + y_t, z_2 + z_t)$$
  $$(x_3,y_3,z_3) \rightarrow (x_3 + x_t, y_3 + y_t, z_3 + z_t)$$


  in which $a \rightarrow b$ denotes $a$ becomes replaced by $b$ after transformation is applied


- __Relativity__
  - ![](assets/Chapter-3-Notes-00dde22f.png){ width=50% }
    - <small>Figure 3.4: Every transformation has two possible interpretations</small>
  - Transforming the coordinate axes results in an _inverse_ of transformation that would correspondingly move the model.
  - _Relativity_: Did the object move, or did the whole world move around it?
    - If we perceive ourselves as having moved, VR sickness can increase


- __Getting ready for rotations__
  - Operation that changes __orientation__ is called __rotation__
  - Simpler problem: 2D linear transformations
    - Consider a 2D virtual world with coordinates $(x,y)$

    $$Let\ M = \begin{bmatrix}m_{11} & m_{12} \\m_{21} & m_{22} \end{bmatrix}$$

    Performing multiplcation of matrix and point $(x,y)$, we get:

    $$\begin{bmatrix}m_{11} & m_{12} \\m_{21} & m_{22} \end{bmatrix} \begin{bmatrix}x \\y \end{bmatrix} = \begin{bmatrix}x' \\y' \end{bmatrix}$$
    $$x' = m_{11}x + m_{12}y$$
    $$y' = m_{21}x + m_{22}y$$

    in which $(x', y')$ is the transformed point. Therefore, $M$ is transformation for $(x,y) \rightarrow (x',y')$


- __Applying the 2D matrix to points__
-
