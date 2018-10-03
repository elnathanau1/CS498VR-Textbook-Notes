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


            ![](assets/Chapter-3-Notes-dcaf99cb.png){ width=25% }


            <small>Figure 3.3: Part of double connected edge list shown for face w/ five edges on boundary. Each half-edge structure *e* stores pointers to the next and prev edges along face boundary. Also stores pointer to its twin half-edge, which is part of boundary of adjacent face)</small>


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
      2. How model should appear after lighting sources and surface properties defined in virtual world

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


    ![](assets/Chapter-3-Notes-00dde22f.png){ width=50% }


    <small>Figure 3.4: Every transformation has two possible interpretations</small>
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


      ![](assets/Chapter-3-Notes-f704c3a9.png){ width=50% }
      1. Multiplying by the identity matrix does not transform
      2. Mirrors over $y$ axis, $(x, y) \rightarrow (-x, y)$
      3. Scales to double the size, $(x,y) \rightarrow (2x,2y)$
      4. Stretches as only $y$ is doubled, $(x,y) \rightarrow (x, 2y)$
          - __aspect ratio__ distortion
      5. Rotate 180°, as both $x$ and $y$ are mirrored, $(x,y) \rightarrow (-x,-y)$
      6. Shear along x-axis, amount of displacement dependant on $y$, $(x,y) \rightarrow (x+y,y)$
      7. Shear along y-axis, amount of displacement dependant on $x$, $(x,y) \rightarrow (x,x+y)$
      8. Two-dimensional shape collapses into one dimension, $(x,y) \rightarrow (x+y,x+y)$
          - case of a __singular matrix__:
            - columns are not linearly independant
            - singular iff determinant = 0


- __Only some matrices produce rotations__
    - $M$ must satisfy rules to be a rotation:
      1. No stretching of axes
      2. No shearing
      3. No mirror images
    - Rule 1: columns of M ust have unit length

    $$m_{11}^2 + m_{21}^2 = 1\ \text{and}\ m_{12}^2 + m_{22}^2 = 1$$

    - Rule 2: dot product must equal 0

    $$m_{11}m_{12} + m_{21}m_{22}=0$$

    - Rule 3: determinant of $M$ equals 1

    $$det\begin{bmatrix}m_{11} & m_{12} \\m_{21} & m_{22} \end{bmatrix}=m_{11}m_{22}-m_{12}m_{21}=1$$

    - Using the unit circle, $x=\text{cos}\ \theta\ \text{and}\ y=\text{sin}\ \theta$, M becomes

    $$\begin{bmatrix}\text{cos}\ \theta & -\text{sin}\ \theta \\\text{sin}\ \theta & \text{cos}\ \theta \end{bmatrix}$$

    - Note: reduced *degrees of freedom* from four to one, $\theta$


- __The 3D case__
    - $M$ is extended from 2D to 3D

    $$M =\begin{bmatrix}m_{11} & m_{12} & m_{13} \\m_{21} & m_{22} & m_{23} \\m_{31} & m_{32} & m_{33}
\end{bmatrix}$$

    - Start with nine degrees of freedom
    - First two rules each remove three DOF, last rule doesn't remove any
    - Therefore, left with three degrees of rotational freedom

- __Yaw, pitch, and roll__


    ![](assets/Chapter-3-Notes-951dca77.png){ width=20% }


    <small>Figure 3.7: Any 3D rotation can be described as sequence of yaw, pitch, and roll rotations</small>

    Let *roll* be counterclockwise rotation of $\gamma$ about the $z$-axis.

    $$R_z(\gamma)=\begin{bmatrix}\text{cos}\ \gamma & -\text{sin}\ \gamma & 0 \\\text{sin}\ \gamma & \text{cos}\ \gamma & 0 \\0 & 0 & 1 \end{bmatrix}$$

    Let *pitch* be counterclockwise rotation of $\beta$ about $x$-axis.

    $$R_x(\beta)=\begin{bmatrix}1 & 0 & 0 \\0 & \text{cos}\ \beta & -\text{sin}\ \beta \\0 & \text{sin}\ \beta & \text{cos}\ \beta \end{bmatrix}$$

    Let *yaw* be counterclockwise rotation of $\alpha$ about the $y$-axis.

    $$R_x(\alpha)=\begin{bmatrix}\text{cos}\ \alpha & 0 & \text{sin}\ \alpha \\0 & 1 & 0 \\-\text{sin}\ \alpha & 0 & \text{cos}\ \alpha \end{bmatrix}$$

- __Combining rotations__
    - Yaw, pitch, and roll rotations can be combined to make any possible 3D rotation

    $$R(\alpha,\beta,\gamma)=R_y(\alpha)R_x(\beta)R_z(\gamma)$$

    - Note: ranges of $\alpha$ and $\gamma$ are from 0 to $2\pi$, but $\beta$ only needs to range from $-\pi/2$ to $\pi/2$
    - Operations __ARE NOT COMMUNICATIVE__

- __Matrix multiplications are "backwards"__
    - Suppose we have point $p$ and rotation matrices $R$ and $P$
    - Let $p' = Rp$
    - Let $p''= Qp'$
    - Note: $p''$ __DOES NOT__ equal $RQp$. Instead, $p''=QRp$

- __Translation and rotation in one matrix__
    - If we want to apply rotation $R$ then translate by $(x_t,y_t,z_t)$

    $$ \begin{bmatrix}x' \\y' \\z' \end{bmatrix}=R\begin{bmatrix}x \\y \\z \end{bmatrix} + \begin{bmatrix}x_t \\y_t \\z_t \end{bmatrix}$$

    - This is impossible to fit in 3x3 matrix, but can be done in 4x4 __homogeneous transformation matrix__

    ![](assets/Chapter-3-Notes-65a9c124.png){ width=20% }

    - $T_{rb}$ used for __rigid body transformation__ (does not distort objects)
    - Because of extra dimension, we extend $(x,y,z)$ to $(x,y,z,1)$
    - Note: This is for rotation *followed by* translation. __NOT COMMUNICATIVE__
