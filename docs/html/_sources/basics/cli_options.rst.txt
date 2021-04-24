.. role:: underbold
    :class: underbold

Basic CLI options
------------------

.. note:: :underbold:`Source code of this section`: `_01_render_settings.py <https://github.com/Elteoremadebeethoven/ManimCE-tutorial/blob/main/_01_render_settings.py>`_

Basic structure of an Animation
""""""""""""""""""""""""""""""""

For a script to be renderable it must have the following structure:

.. code-block:: python

    # Import the manim library
    from manim import *

    # This is the way to define an Scene
    class SCENE_NAME(Scene):
        def construct(self):
            # Here is all the code for your animation.
            pass

Cli options
"""""""""""""

.. code::

                                    DEFAULTS
    =================================================================================
    -p          PREVIEW                       Open the scene with your media player

    -a          RENDER ALL SCENES
                IN THE FILE
                (DON'T USE IT WITH -p FLAG)

    -ql         LOW QUALITY         480p    15 fps
    -qm         MEDIUM QUALITY      720p    30 fps
    -qh         HIGHT QUALITY       1080p   60 fps
    -qp         PRODUCTION QUALITY  1440p   60 fps
    -qk         4K                  2160p   60 fps
    -s          RENDER PNG OF THE
                LAST FRAME

    Shorts:
        -pql    PREVIEW IN LOW QUALITY
        -pqm    PREVIEW IN MEDIUM QUALITY
        -pqh    PREVIEW IN HIGHT QUALITY
        -pqp    PREVIEW IN PRODUCTION QUALITY
        -pqk    PREVIEW IN 4K QUALITY
        -ps     RENDER LAST FRAME AS PNG

                                    CUSTOM
    =================================================================================
    -r H,W      RENDER WITH CUSTOM
                DIMENSIONS

                Example: -r 500,500

    -o FILE_NAME

    CLICK (Not all properties works fine yet)
    -----------------------------------
    [CLI]
    # my config file
    #save_as_gif = True
    #background_color = WHITE
    -----------------------------------


Use default settings
""""""""""""""""""""""

In the first file ``_01_render_settings.py`` you will find this code.

.. code:: python

    from manim import *

    class Scene1(Scene):
        def construct(self):
            t = Text("SCENE 1")
            self.play(Write(t))
            self.wait()

    class Scene2(Scene):
        def construct(self):
            t = Text("SCENE 2")
            self.play(FadeIn(t))
            self.wait()

    class Scene3(Scene):
        def construct(self):
            t = Text("SCENE 3")
            self.play(GrowFromCenter(t))
            self.wait()

Each class that inherits from Scene is a separate animation. You can render the first one at 480p using:

.. code:: sh

    manim tutorial/_01_render_settings.py Scene1 -p -ql

You will see something like this in the terminal:

.. code-block:: sh
    :emphasize-lines: 19-22

    Manim Community v0.5.0
    [04/23/21 23:44:37] INFO     Animation 0 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/480p15/partial_                         
                                movie_files/Scene1/3163782                         
                                288_3424579518_1323973724.                         
                                mp4'}                                              
                        INFO     Animation 1 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/480p15/partial_                         
                                movie_files/Scene1/1495979                         
                                052_1438405273_696553468.m                         
                                p4'}                                               
                        INFO                                scene_file_writer.py:579
                                File ready at /Users/zavde                         
                                n/Downloads/ManimCE/media/                         
                                videos/_01_render_settings                         
                                /480p15/Scene1.mp4                                 
                                                                                    
                        INFO     Rendered Scene1                        scene.py:190
                                Played 2 animations                                
                        INFO     Previewed File at: /Users/zavden/Dow file_ops.py:99
                                nloads/ManimCE/media/videos/_01_rend               
                                er_settings/480p15/Scene1.mp4

If you have installed Manim correctly, the animation will have automatically opened with your default player.
In the highlighted lines you will see the full location of the file in mp4.

In general, to render any scene the command structure is

.. code:: sh

    manim <scrip.py> <SCENE-NAME> <FLAGS>

In our case, we can join the ``-p`` and ``-ql`` flags to have the same result,

.. code:: sh

    manim tutorial/_01_render_settings.py Scene1 -pql

Render all scenes
"""""""""""""""""""

To render all scenes in a script use ``-a``.

In our case, if we want all the scenes to be rendered at low resolution we would use ``-aql``:

.. code:: 

    manim tutorial/_01_render_settings.py -aql

.. warning:: Don't use ``-paql`` because if you have a lot of scenes they will open automatically when they finish rendering.

If we wanted them to be rendered at medium resolution we would use ``-aqm``.

You can see all the predefined settings above.

Custom resolution
"""""""""""""""""""""""""""""""

.. code::

    manim tutorial/_01_render_settings.py Scene1 -pql -r 900,600

Where 900 is the pixel height and 600 is the pixel width.

It doesn't matter if you use ``-ql``, ``-qm``, ``-qh``, or another resolution flag, the ``-r`` will overwrite the dimensions, if you change the resolution flags you would only change the **fps**.


Save as gif
"""""""""""""""""""""""""""""""

Render animation as GIF using low resolution.

.. code::

    manim tutorial/_01_render_settings.py Scene1 -ql -i

Render animation as GIF using 900x600 resolution at 30 fps with preview:

.. code::

    manim tutorial/_01_render_settings.py Scene1 -pqm -r 900,600 -i


Render last frame
"""""""""""""""""""""""""""""""""

Render last frame at 1080p with preview:

.. code::

    manim tutorial/_01_render_settings.py Scene1 -ps

Start animation from
""""""""""""""""""""""""""""""""""

Copy this animation in your file:

.. code-block:: python

    class Scene4(Scene):
        def construct(self):
            t = Text("Hello world")
            square = Square()
            circle = Circle()
            triangle = Triangle()

            print("Start animations -------------")

            print("Add text")
            self.add(t)

            print("Wait 1 second")
            self.wait()

            print("Create square")
            self.play(Create(square))

            print("Wait 2 seconds")
            self.wait(2)

            print("Create circle")
            self.play(Create(circle))

            print("Wait 1.5 seconds")
            self.wait(1.5)

            print("Create triangle")
            self.play(Create(triangle))

            print("Last wait")
            self.wait()

If we render this video with:

.. code:: sh

    manim tutorial/_01_render_settings.py Scene4 -pqm

You will see this output:

.. code-block:: sh

    Manim Community v0.5.0
    Start animations -------------
    Add text
    Wait 1 second
    [04/24/21 00:40:26] INFO     Animation 0 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/720p30/partial_                         
                                movie_files/Scene4/6552404                         
                                68_1438405273_192487528.mp                         
                                4'}                                                
    Create square
                        INFO     Animation 1 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/720p30/partial_                         
                                movie_files/Scene4/1201832                         
                                484_1768192346_2074958280.                         
                                mp4'}                                              
    Wait 2 seconds
    [04/24/21 00:40:27] INFO     Animation 2 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/720p30/partial_                         
                                movie_files/Scene4/1201832                         
                                484_2616472470_324434285.m                         
                                p4'}                                               
    Create circle
                        INFO     Animation 3 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/720p30/partial_                         
                                movie_files/Scene4/1201832                         
                                484_355446327_3071649543.m                         
                                p4'}                                               
    Wait 1.5 seconds
                        INFO     Animation 4 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/720p30/partial_                         
                                movie_files/Scene4/1201832                         
                                484_2941483014_474227006.m                         
                                p4'}                                               
    Create triangle
    [04/24/21 00:40:28] INFO     Animation 5 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/720p30/partial_                         
                                movie_files/Scene4/1201832                         
                                484_3040797843_2557678564.                         
                                mp4'}                                              
    Last wait
                        INFO     Animation 6 : Partial      scene_file_writer.py:395
                                movie file written in {'/U                         
                                sers/zavden/Downloads/Mani                         
                                mCE/media/videos/_01_rende                         
                                r_settings/720p30/partial_                         
                                movie_files/Scene4/1201832                         
                                484_1438405273_4180111533.                         
                                mp4'}                                              
                        INFO                                scene_file_writer.py:579
                                File ready at /Users/zavde                         
                                n/Downloads/ManimCE/media/                         
                                videos/_01_render_settings                         
                                /720p30/Scene4.mp4                                 
                                                                                    
                        INFO     Rendered Scene4                        scene.py:190
                                Played 7 animations                                
                        INFO     Previewed File at: /Users/zavden/Dow file_ops.py:99
                                nloads/ManimCE/media/videos/_01_rend               
                                er_settings/720p30/Scene4.mp4

If we render this animation this time the output will be different:

.. code-block:: sh
    :emphasize-lines: 5,9,13,17,21,25,29

    Manim Community v0.5.0
    Start animations -------------
    Add text
    Wait 1 second
    [04/24/21 00:41:42] INFO     Animation 0 : Using cached     cairo_renderer.py:99
                                data (hash : 655240468_1438405                     
                                273_192487528)                                     
    Create square
                        INFO     Animation 1 : Using cached     cairo_renderer.py:99
                                data (hash : 1201832484_176819                     
                                2346_2074958280)                                   
    Wait 2 seconds                                                                  
                        INFO     Animation 2 : Using cached     cairo_renderer.py:99
                                data (hash : 1201832484_261647                     
                                2470_324434285)                                    
    Create circle
                        INFO     Animation 3 : Using cached     cairo_renderer.py:99
                                data (hash : 1201832484_355446                     
                                327_3071649543)                                    
    Wait 1.5 seconds                                                                
                        INFO     Animation 4 : Using cached     cairo_renderer.py:99
                                data (hash : 1201832484_294148                     
                                3014_474227006)                                    
    Create triangle
                        INFO     Animation 5 : Using cached     cairo_renderer.py:99
                                data (hash : 1201832484_304079                     
                                7843_2557678564)                                   
    Last wait                                                                       
                        INFO     Animation 6 : Using cached     cairo_renderer.py:99
                                data (hash : 1201832484_143840                     
                                5273_4180111533)                                   
                        INFO                                scene_file_writer.py:579
                                File ready at /Users/zavde                         
                                n/Downloads/ManimCE/media/                         
                                videos/_01_render_settings                         
                                /720p30/Scene4.mp4                                 
                                                                                    
                        INFO     Rendered Scene4                        scene.py:190
                                Played 7 animations                                
                        INFO     Previewed File at: /Users/zavden/Dow file_ops.py:99
                                nloads/ManimCE/media/videos/_01_rend               
                                er_settings/720p30/Scene4.mp4 

Explanation: Manim renders each animation (each self.play) separately, and in the end it concatenates all the videos into one.

If the animations are simple, the compiler saves a hash that identifies each animation of a script, and if it does not detect changes, then it will not render it, it will simply copy it, so the rendering will be faster.

.. note:: If the animations are relatively complex, this won't work (at least, for now).

In the highlighted lines you will see the number of each animation, in this example there are 7 animations (counting from 0).

This is because pauses are also considered animations, that is, ``Scene.wait`` and ``Scene.play`` are interpreted as animations. If you don't understand why ``Scene.wait`` is considered an animation we will explain it in the **updaters** section with *dt*.

If we wanted to start the animation from the creation of the circle we would use:

.. code::

    manim tutorial/_01_render_settings.py Scene4 -pqm -n 3

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/Sf3.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

If we wanted to start the animation from the creation of the square and ending in the creation of the circle we would use:

.. code::

    manim tutorial/_01_render_settings.py Scene4 -pqm -n 1,3

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
    <video allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" controls>
        <source src="../_static/S1t3.mp4" type="video/mp4">
    </video>
    </div>
    <hr/>

Change name
""""""""""""""

The animations will be rendered with the name of the class you defined, that is, if we render ``Scene1`` the mp4 file will be called the same, if we want it to be called in another way we simply use ``-o Other_name``.

.. code::

    manim tutorial/_01_render_settings.py Scene1 -pqm -o First_scene
