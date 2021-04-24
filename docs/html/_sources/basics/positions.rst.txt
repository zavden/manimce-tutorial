Positions
------------

.. note:: :underbold:`Source code of this section`: `_03_basic_positions.py <https://github.com/Elteoremadebeethoven/ManimCE-tutorial/blob/main/_03_basic_positions.py>`_

For this section we will be using the object called ScreenGrid, a Mobject that I created to help us visualize the coordinates of the screen.

.. code-block:: python

    class CoordScreen(Scene):
        def construct(self):
            screen_grid = ScreenGrid()
            dot = Dot([1, 1, 0])
            self.add(screen_grid)
            self.play(FadeIn(dot))
            self.wait()

.. image:: ../_static/CoordScreen.png

There are several constants that help to locate objects on the screen, and we can specify any coordinate through them using linear combinations.

From ``manim/constants.py``

.. code-block:: python

    # Geometry: directions
    ORIGIN: np.ndarray = np.array((0.0, 0.0, 0.0))
    """The center of the coordinate system."""

    UP: np.ndarray = np.array((0.0, 1.0, 0.0))
    """One unit step in the positive Y direction."""

    DOWN: np.ndarray = np.array((0.0, -1.0, 0.0))
    """One unit step in the negative Y direction."""

    RIGHT: np.ndarray = np.array((1.0, 0.0, 0.0))
    """One unit step in the positive X direction."""

    LEFT: np.ndarray = np.array((-1.0, 0.0, 0.0))
    """One unit step in the negative X direction."""

    IN: np.ndarray = np.array((0.0, 0.0, -1.0))
    """One unit step in the negative Z direction."""

    OUT: np.ndarray = np.array((0.0, 0.0, 1.0))
    """One unit step in the positive Z direction."""

    # Geometry: axes
    X_AXIS: np.ndarray = np.array((1.0, 0.0, 0.0))
    Y_AXIS: np.ndarray = np.array((0.0, 1.0, 0.0))
    Z_AXIS: np.ndarray = np.array((0.0, 0.0, 1.0))

    # Geometry: useful abbreviations for diagonals
    UL: np.ndarray = UP + LEFT
    """One step up plus one step left."""

    UR: np.ndarray = UP + RIGHT
    """One step up plus one step right."""

    DL: np.ndarray = DOWN + LEFT
    """One step down plus one step left."""

    DR: np.ndarray = DOWN + RIGHT
    """One step down plus one step right."""

Example:

.. code-block:: python

    class BasicPositions(Scene):
        def construct(self):
            dot_center = Dot(color=WHITE)      # ORIGIN: [0,0,0] by default
            dot_left  = Dot(LEFT,color=RED)    # [-1,0,0]
            dot_right = Dot(RIGHT,color=BLUE)  # [1,0,0]
            dot_up    = Dot(UP,color=GREEN)    # [0,1,0]
            dot_down  = Dot(DOWN,color=ORANGE) # [0,-1,0]
            dot_2_3   = Dot([2,3,0],color=TEAL)# [2,3,0]

            logger.info(f"frame_width: {config.frame_width}")
            logger.info(f"frame_height: {config.frame_height}")

            self.add(
                # ScreenGrid(), # <- uncomment this
                dot_center,
                dot_left,
                dot_right,
                dot_up,
                dot_down,
                dot_2_3,
            )
            self.wait()

.. image:: ../_static/BasicPositions.png

``Mobject.to_edge & Mobject.to_corner``
""""""""""""""""""""""""""""""""""""""""""

.. code-block:: python

    class EdgesAndCorners(Scene):
        def construct(self):
            square = Square()
            square.to_corner(UR)               # UP + RIGHT

            triangle = Triangle()
            triangle.to_edge(DOWN,buff=0.1)    # DOWN + LEFT

            dot_up   = Dot(color=RED)
            dot_up.to_edge(UP)

            dot_down = Dot(color=BLUE)
            dot_down.to_edge(DOWN,buff=2)

            self.add(
                square,
                triangle,
                dot_up,
                dot_down
            )
            self.wait()

.. image:: ../_static/EdgesAndCorners.png

``Mobject.shift``
""""""""""""""""""

.. code-block:: python

    class ShiftMethod(Scene):
        """
        The shift method moves the object 
        based on the current position of 
        the object.
        """
        def construct(self):
            circle = Circle()
            self.add(circle)
            self.wait()
            circle.shift(RIGHT)
            self.wait()
            circle.shift(RIGHT)
            self.wait()
            circle.shift(DOWN)
            self.wait()
            circle.shift(LEFT)
            self.wait()

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/ShiftMethod.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

``Mobject.move_to``
"""""""""""""""""""""

.. code-block:: python

    class MoveToMethod1(Scene):
        """
        The move_to method moves the object
        taking as reference the origin or
        some particular point
        """
        def construct(self):
            circle = Circle()
            self.add(circle)
            self.wait()
            # In this way, it takes the center of the screen as a reference
            circle.move_to(RIGHT)
            self.wait()
            circle.move_to(RIGHT)
            self.wait()
            circle.move_to(DOWN)
            self.wait()
            circle.move_to([2,3,0])
            self.wait()

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/MoveToMethod1.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

.. code-block:: python

    class MoveToMethod2(Scene):
        def construct(self):
            circle = Circle()
            dot_1 = Dot([1,3,0],color=ORANGE)
            dot_2 = Dot([-2,-3,0],color=BLUE)
            self.add(circle,dot_1,dot_2)
            self.wait()
            circle.move_to(dot_1)
            self.wait()
            circle.move_to(dot_2)
            self.wait()
            In this way, it takes a Mobject (dot_2) as a reference
            circle.move_to(dot_2.get_center()+RIGHT)
            self.wait()

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/MoveToMethod2.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

``Mobject.next_to``
"""""""""""""""""""""

.. code-block:: python

    class NextTo(Scene):
        """
        next_to references the edges of an 
        object to locate another object.
        """
        def construct(self):
            text = Text("Hello world")
            text.shift(LEFT+2*UP)

            left_dot = Dot().next_to(text,LEFT)
            right_dot = Dot().next_to(text,RIGHT,buff=0)
            down_dot = Dot().next_to(text,DOWN,buff=1)

            self.add(text, left_dot, right_dot,down_dot)
            self.wait()

.. image:: ../_static/NextTo.png


``Mobject.get_``
"""""""""""""""""

.. code-block:: python

    class BordersAndCorners(Scene):
        def construct(self):
            text = Text("Hello world").scale(2)
            d1 = Dot(text.get_corner(UL))
            d2 = Dot(text.get_bottom())
            d3 = Dot(text.get_top())
            d4 = Dot(text.get_left())
            d5 = Dot(text.get_right())

            self.add(text,d1,d2,d3,d4,d5)
            self.wait()

.. image:: ../_static/BordersAndCorners.png


In addition to these methods there are also these others:

* ``Mobject.get_x()`` :math:`\Leftrightarrow` ``Mobject.get_center()[0]``
* ``Mobject.get_y()`` :math:`\Leftrightarrow` ``Mobject.get_center()[1]``
* ``Mobject.get_z()`` :math:`\Leftrightarrow` ``Mobject.get_center()[2]``

``Mobject.align_to``
"""""""""""""""""""""""

.. code-block:: python

    class Align(Scene):
        def construct(self):
            rect = Rectangle(width=6,height=4,color=RED)
            a = Text("A")
            b = Text("B")
            c = Text("C")

            a.align_to(rect,LEFT)
            b.align_to(rect,UP)
            c.align_to(rect,UR)

            self.add(rect,a,b,c)
            self.wait()

.. image:: ../_static/Align.png


``Mobject.rotate``
"""""""""""""""""""

.. code-block:: python

    class Rotations(Scene):
        def construct(self):
            a = Text("A")
            a.shift(LEFT*3)
            a.rotate(30*DEGREES) #or .rotate(PI/6)

            dot = Dot(RIGHT)
            b = Text("B")
            b.rotate(PI/2,about_point=dot.get_center())

            self.add(a,b,dot)
            self.wait()

.. image:: ../_static/Rotations.png
