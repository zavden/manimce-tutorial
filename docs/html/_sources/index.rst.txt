.. Freelance Job documentation master file, created by
   sphinx-quickstart on Sun Jul 19 18:38:11 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. _main_page:

.. role:: underline
    :class: underline

.. role:: underbold
    :class: underbold

ManimCE tutorial by TheoremOfBeethoven
===========================================

.. image:: _static/banner.gif

.. note:: This :underbold:`is not` the official ManimCE tutorial, the official documentation is `here <https://docs.manim.community/en/stable/>`_. I am a person outside the project that has been using Manim since 2018 who wants to share their knowledge.

What is ManimCE?
---------------------------------

**Manim** (just) is a project created by `Grant Sanderson <https://en.wikipedia.org/wiki/3Blue1Brown>`_ (`3Blue1Brown <https://www.youtube.com/channel/UCYO_jab_esuFRV4b17AJtAw>`_) around 2015, he created it with the sole intention of making his own videos on YT.

This project did not have a clear direction, since the purpose of this library was the videos of Grant Sanderson. Starting in 2020, several programmers (with the approval of Grant Sanderson) created a fork of Manim called `ManimCE <https://www.manim.community/>`_, which is not supported by 3b1b, but by the community.

At the beginning of 2020 the Manim version of 3b1b (not ManimCE) changed the graphics engine, from PyCairo to OpenGL. The old version that used PyCairo was called **ManimCairo**, and the modern version was called **ManimGL**, both versions belong to 3b1b.

In summary, there are 3 versions of Manim:

1. `ManimCairo <https://github.com/3b1b/manim/tree/cairo-backend>`_: The original version of Manim that uses PyCairo and is no longer supported by anyone, is currently hosted in the cairo-backend branch of the 3b1b repository.
2. `ManimGL <https://github.com/3b1b/manim/tree/master>`_: It is the new version that 3b1b uses to make its videos, it is the master branch of the 3b1b repository.
3. `ManimCE <https://github.com/ManimCommunity/manim>`_: It is a fork of ManimCairo, supported by the community, it currently uses PyCairo as the main graphics engine, but in the long run it is expected to move to OpenGL in the same way.

What do I need to know to learn Manim?
----------------------------------------

You need to have knowledge of **OOP** and package management in Python, if you only have basic programming knowledge you are going to suffer a lot.

It is also necessary to have knowledge of **LaTeX** to be able to write formulas.

Which version of Manim should I learn?
-----------------------------------------

It depends, if you are a **beginner** it is best to learn **ManimCE**, it has better documentation, it is the most stable of the 3 versions and the community is very good.
If you know how to use ManimCairo and you want higher speed, you can use **ManimGL**, which renders the videos in real time, the only problem is that it is the most unstable of the 3.
I personally use all 3, each version has its good points and bad points.

If you come from ManimCairo or ManimGL and want to learn ManimCE here is a video made by me where I explain the main differences.

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube.com/embed/xrZDKC9Buxk" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>

The most current version is **0.5.0**, and it is constantly updated. I will try to keep this tutorial always up to date.

.. warning:: I am :underbold:`not` part of the development community, please, if you find a bug or error, report it to the official repository.

ManimCE official social networks
---------------------------------

* `Main page. <https://www.manim.community/>`_
* `GitHub repo. <https://github.com/ManimCommunity/manim>`_
* `Documentation. <https://docs.manim.community/en/stable/>`_
* `Discord server. <https://discord.gg/mMRrZQW>`_
* `Reddit. <https://www.reddit.com/r/manim/>`_
* `Twitter. <https://twitter.com/manim_community/>`_

Support this project
=======================

You can support this project on **PayPal** and **Patreon**

* `PayPal <https://paypal.me/zavdn>`_
* `Patreon <https://www.patreon.com/theoremofbeethoven>`_

Or hire me as Freelance, `see here <https://zavden.github.io/freelance-job/docs/html/index.html>`_ all the information.

Contents
=============

.. toctree::
   /basics/installation.rst
   /basics/initial_steps.rst
   /basics/cli_options.rst
   /basics/basic_animations.rst
   /basics/positions.rst
   /basics/basic_properties.rst
   /basics/import_assets.rst
   /basics/groups_and_vgroups.rst
   /basics/tex_and_texts.rst
   /basics/transformations.rst
   /basics/graphs_2d.rst
   /basics/graphs_3d.rst
   /intermediate/basic_updaters.rst
   /intermediate/alpha_updaters.rst
   /intermediate/animate_methods.rst
   /intermediate/dt_updaters.rst
   /intermediate/group_animations.rst
   /advanced/custom_mobjects.rst
   /advanced/custom_animations.rst
   /advanced/moving_camera_scene.rst
   /advanced/zoomed_camera_scene.rst
   :maxdepth: 2





