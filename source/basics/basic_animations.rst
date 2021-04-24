.. role:: underbold
    :class: underbold

Basic animations
----------------------

.. note:: :underbold:`Source code of this section`: `_02_basic_animations.py <https://github.com/Elteoremadebeethoven/ManimCE-tutorial/blob/main/_02_basic_animations.py>`_


.. raw:: html

    <hr/>

Mobjects
""""""""""""

All objects that can be displayed on the screen inherit from the ``Mobject`` class, there are several types:

* ``ImageMobject``: Raster images.
* ``VMobjects``: Bezier curves, all predefined geometric shapes inherit from ``VMobject``.
* ``SVGMobject``: SVG file, inherits from ``VMobject``.
* ``Group``: Mobjects grouping.
* ``VGroup``: VMobjects grouping.

There are two ways to add Mobjects to the screen and two ways to remove something from the screen.

To add something to the screen we can use ``Scene.add`` or ``Scene.play`` with some creation or modification animation.

``Scene.add``
""""""""""""""

When we use ``Scene.add`` it is done instantly, that is, if we do this:

.. code-block:: python

    self.add(Square())
    self.add(Circle())
    self.add(Text("Hello world"))

the objects are going to be added without animation, we could even do this to write less code.

.. code-block:: python

    self.add(Square(),Circle(),Text("Hello world"))

If your script doesn't have any ``Scene.wait`` or ``Scene.play`` then **you can't** use ``-ql``, ``-qm`` etc, you must use ``-s`` or ``-ps``, because your script doesn't have animations. See the second file of the tutorial repo.

.. code-block:: python

    class NoAnimations(Scene):
        """
        In this scene there are no animations,
        neither Scene.wait(...) nor Scene.play(...)
        so it should not be rendered as video,
        but can be rendered as image using -s or -ps
        """
        def construct(self):
            text = Text("Hello world")
            self.add(text)
            # self.wait() # <---- use a wait to render this as animation.

.. raw:: html

    <p style="text-align:center;font-size: 2em; font-weight: bold; text-decoration: underline overline; text-underline-offset: 0.2em;">Quiz</p>
    <p style="text-align:center;">Imagine the result of the following code.</p>

.. code-block:: python

    def construct(self):
        self.add(Square())
        self.wait()

        self.add(Circle())
        self.wait()

        self.add(Triangle())
        self.wait()


Types of animations
""""""""""""""""""""

There are **two ways** to make animations, one is with **updaters** and the other is using the ``Scene.play`` method. The updaters are more advanced and we will see them later.

``Scene.play``
"""""""""""""""""""

The ``Scene.play`` method accepts **two types** of arguments, either **methods of Mobjects as animations** and **class animations**, we will see the methods of Mobjects later after seeing Mobjects properties, the most basic animations are the class animations.

In summary, the ways to make animations are:

* Updaters:

    * Simple updaters
    * :math:`\alpha` updaters
    * :math:`\tt dt` updaters

* ``Scene.play``:

    * Methods of Mobjects
    * Class animations

In this section we will analyze the last one, which is the simplest.

Class animations
******************

.. raw:: html

    <hr/>

Types
+++++++

There are already several predefined class animations, and they are divided into 4 groups.

1. :underbold:`Creation animations`: They add an object to the screen.

2. :underbold:`Transformation animations`: They modify the shape or position of an object.

3. :underbold:`Indication animations`: They help to identify an object on the screen, they are actually a fusion of the other 3 animations.

4. :underbold:`Animations to remove`: They remove an object from the screen.

Attributes
+++++++++++++++

Every class animation has the following main properties:

* ``run_time`` *(float)*: It is the duration of the animation.

* ``rate_func`` *(function)*: It is the behavior of the animation, most of them are ``smooth``, but they can also be:

.. code-block:: python

    def linear(t: typing.Union[np.ndarray, float]) -> typing.Union[np.ndarray, float]:
        return t

    def smooth(t: float, inflection: float = 10.0) -> np.ndarray:
        error = sigmoid(-inflection / 2)
        return np.clip(
            (sigmoid(inflection * (t - 0.5)) - error) / (1 - 2 * error),
            0,
            1,
        )

    def rush_into(t: float, inflection: float = 10.0) -> np.ndarray:
        return 2 * smooth(t / 2.0, inflection)

    def rush_from(t: float, inflection: float = 10.0) -> np.ndarray:
        return 2 * smooth(t / 2.0 + 0.5, inflection) - 1

    def slow_into(t: np.ndarray) -> np.ndarray:
        return np.sqrt(1 - (1 - t) * (1 - t))

    def double_smooth(t: float) -> np.ndarray:
        if t < 0.5:
            return 0.5 * smooth(2 * t)
        else:
            return 0.5 * (1 + smooth(2 * t - 1))

    def there_and_back(t: float, inflection: float = 10.0) -> np.ndarray:
        new_t = 2 * t if t < 0.5 else 2 * (1 - t)
        return smooth(new_t, inflection)

    def there_and_back_with_pause(t: float, pause_ratio: float = 1.0 / 3) -> np.ndarray:
        a = 1.0 / pause_ratio
        if t < 0.5 - pause_ratio / 2:
            return smooth(a * t)
        elif t < 0.5 + pause_ratio / 2:
            return 1
        else:
            return smooth(a - a * t)

    def running_start(t: float, pull_factor: float = -0.5) -> typing.Iterable:
        return bezier([0, 0, pull_factor, pull_factor, 1, 1, 1])(t)

    def not_quite_there(
        func: typing.Callable[[float, typing.Optional[float]], np.ndarray] = smooth,
        proportion: float = 0.7,
    ) -> typing.Callable[[float], np.ndarray]:
        def result(t):
            return proportion * func(t)
        return result

    def wiggle(t: float, wiggles: float = 2) -> np.ndarray:
        return there_and_back(t) * np.sin(wiggles * np.pi * t)

    def squish_rate_func(
        func: typing.Callable[[float], typing.Any],
        a: float = 0.4,
        b: float = 0.6,
    ) -> typing.Callable[[float], typing.Any]:  # what is func return type?
        def result(t):
            if a == b:
                return a

            if t < a:
                return func(0)
            elif t > b:
                return func(1)
            else:
                return func((t - a) / (b - a))
        return result

    # See all in manim/utils/rate_functions.py

* ``remover`` *(bool)*: It is ``True`` when the intention of the animation is to remove the Mobject from the screen, some class animations that have this attr as ``True`` are ``FadeOut`` and ``Uncreate``.

* ``Mobject`` *(Mobject)*: Some animations only accept VMobjects (like ``Write``) or some specific Mobject for that animation, while others accept any Mobject (like ``FadeIn``).

There are some rules for using ``Scene.play``, one of the most important is that you cannot animate a Mobject twice in the same ``Scene.play`` method.

In the example below, you couldn't have more than one uncommented animation.

.. code-block:: python

    class BasicAnimations(Scene):
        def construct(self):
            text = Text("Hello word")
            self.play(
                Write(text),
                # FadeIn(text),
                # GrowFromCenter(text),
                # FadeInFromLarge(text, scale_factor=2), # <- Some animations require more arguments to work.
            )
            self.wait() # <- It is advisable to always have a wait at the end

And in general, it is always advisable to have a ``Scene.wait`` at the end so that the above animation does not have strange behaviors.

Multiple animations at the same using Scene.play
++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: python

    class MultipleAnimationSameTime(Scene):
        def construct(self):
            square = Square()
            circle = Circle()
            self.play(
                Create(square),
                FadeIn(circle)
            )
            self.wait()

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/MultipleAnimationSameTime.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

Animations with arguments
++++++++++++++++++++++++++++++

Of all animations:

.. code-block:: python

    class ChangeDuration(Scene):
        def construct(self):
            self.play(
                Create(Circle()),
                FadeIn(Square()),
                run_time=3,
                rate_func=linear
            )
            self.wait()

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/ChangeDuration.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

Of each animation:

.. code-block:: python

    class ChangeDurationMultipleAnimations(Scene):
        def construct(self):
            self.play(
                Create(
                    Circle(),
                    run_time=3,
                    rate_func=smooth
                ),
                FadeIn(
                    Square(),
                    run_time=2,
                    rate_func=there_and_back
                ),
                GrowFromCenter(
                    Triangle()
                )
            )
            self.wait()

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/ChangeDurationMultipleAnimations.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

More animations
++++++++++++++++++++

.. code-block:: python

    class MoreAnimations(Scene):
        def construct(self):
            text = Text("Hello world")
            self.play(Write(text))
            self.wait()
            self.play(Rotate(text,PI/2))
            self.wait()
            self.play(Indicate(text))
            self.wait()
            self.play(FocusOn(text))
            self.wait()
            self.play(ShowCreationThenDestructionAround(text))
            self.wait()
            self.play(FadeOut(text))
            self.wait()

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/MoreAnimations.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

Where to see all the predefined animations
+++++++++++++++++++++++++++++++++++++++++++++

Some time ago I made `this small documentation <https://elteoremadebeethoven.github.io/manim_3feb_docs.github.io/html/tree/animation.html#animations>`_ of all ManimCairo animations, the use of animations is not the same in ManimCE but you can get an idea of how they work.

The source code of all class animations are in ``manim/animations``.

``Scene.remove``
""""""""""""""""""

It is the equivalent of ``Scene.add``, but instead of adding to the screen, they remove it from the screen, there is no more mystery.

Example:

.. code-block:: python

    class AddAndRemove(Scene):
        def construct(self):
            text = Text("Hello world")
            self.add(text)
            self.wait()
            self.remove(text)
            self.wait()