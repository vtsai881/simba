Batch Video Processing
=======================================

It is often helpful, and sometimes necessary, to pre-process
experimental videos prior to analysis. This is generally accomplished
through the use of open-source approaches like **FFmpeg** or commercial
software, but can be a time consuming and cumbersome when applying to
numerous similar videos. To streamline this process, SimBA incorporates
**FFmpeg** into a a batch-process GUI.

This video pre-processing tool allows you to change multiple video
parameters (clip/trim/crop, etc.) for multiple videos in a batch-process
that is rapidly configured and then executed when ready. Once the
required parameters has been set for all the videos, the user press
``Execute`` and the new videos will be generated according to the user
input. Videos are processed using **FFmpeg**. Click
`here <https://m.wikihow.com/Install-FFmpeg-on-Windows>`__ to learn how
to install FFmpeg on your computer.

.. note::
  Processing numerous high-resolution or long-duration videos
  takes time. We strongly suggest that you not execute a batch until you
  are ready to commit computational time to the process.**

We suggest pre-processing videos in the following scenarios:

1) Red-light: If you have recorded in red-light conditions, we suggest
   converting to gray-scale and using CLAHE.
2) Reflections: If your recordings include reflections on the walls of
   your testing apparatus, we suggest cropping to remove the
   reflections.
3) Artifacts: If your recordings include frames where your hands (or
   other unintended features) are included in the video, at either the
   start or the end, we suggest trimming the videos to remove these
   frames.
4) Resolution: If your recordings are significantly higher resolution
   than needed, we suggest down-sampling to decrease processing time.

Pipeline
--------

The video parameters that you specify will be processed in the following
sequence. If the user leaves certain parameters unchanged, then they are
ignored in the pipeline.

.. image:: img/video_process/flow_diagram.png
  :width: 800
  :align: center

Step 1: Folder Selection
------------------------

.. image:: img/video_process/menu_1.png
  :width: 1000
  :align: center

1. To begin batch pre-processing, in the main SimBA window click on
   ``Process Videos`` –> ``Batch pre-process videos``. The window shown
   below will display.

.. image:: img/video_process/menu_2.png
  :width: 1000
  :align: center

2. Under **Folder Selection** heading and next to ``Video directory``,
   click on ``Browse Folder`` and navigate to a folder that contains the
   videos that should be batch processed and click on ’Select Folder\`.
   All vidoes that you would like to process must be present in this
   directory.

.. image:: img/video_process/menu_3.png
  :width: 1000
  :align: center

3. Next to ``Output Directory``, click on ``Browse Folder`` and navigate
   to a folder *(usually a new, empty, folder)* that should store the
   processed videos and click on ’Select Folder\`.

4. Click to ``Confirm`` the two selected directories.

.. note::
   Please make sure there is no spaces in your folder names or
   video names. Instead use underscores if needed.

.. image:: img/video_process/menu_4.png
  :width: 1000
  :align: center

Step 2: The batch processing interface.
---------------------------------------

1. Once you select ``Confirm``, an interface will be displayed which
   will allow us to manipulate the attributes of each video, or batch
   change attributes of all videos in the directory. Below is a
   screengrab of this interface, which I have labelled into three
   different parts: **(1) QUICK SETTINGS, (2) VIDEOS, and (3) EXECUTE**.
   We will go through the functions of each one in turn.

.. image:: img/video_process/menu_5.png
  :width: 1000
  :align: center


Quick settings
~~~~~~~~~~~~~~

The quick setting menu allows us to batch specify new resolutions, new
frames rates, or clipping times for all videos. In my toy example I have
10 videos, each which is 10s long (Note: you can see that they are 10s
long in the middle **VIDEOS** table, by looking in the *End Time*
column, shich SimBa has populated with the video meta-information data).

Let’s say I want to remove the first 5s from each of the videos, and to
do this I can use the ``Clip Videos Settings`` sub-menu in QUICK
SETTINGS. To do this, I set the ``Start Time`` to 00:00:05, and the
``End Time`` to 00:00:10 and click ``Apply``, as in the gif below. Note
that the ``Start Time`` of all videos listed in the VIDEOS table are
updated:

.. image:: img/video_process/quick_clip.gif
  :width: 1000
  :align: center


Similarly, let say I want to downsample all my videos to a 1200x800
resolution. I then update the ``Width`` and ``Height`` values in the
``Downsample Videos`` sub-menu, and click ``Apply``:

.. image:: img/video_process/quick_downsample.gif
  :width: 1000
  :align: center

The video table
~~~~~~~~~~~~

The middle VIDEOS table list all the video files found inside your input
directory defined in Step 1, with one video per row. Each video has a
``Crop`` button, and several entry boxes and radio buttons that allows
us to specify which pre-processing functions we should apply to each
video. In the header of the VIDEOS table, there are also radio buttons
that allows us to tick all of the videos in the table. For example, if I
want to apply the 00:00:05 to 00:00:10 clip trimming to all videos, I go
ahead and click the ``Clip all videos`` radio button. If I want
downsample all videos, I go ahead and click the
``Downsample All Videos`` radiobutton. If I want to ``Clip all videos``
*except* few videos. I go ahead and de-select the videos I want to omit
from downsampling. The same applies for the FPS, greyscale, CLAHE and
Frame count radio buttons:

.. image:: img/video_process/header_radiobtn.gif
  :width: 1000
  :align: center

Next, it might be that you want to crop some of the videos listes in the
VIDEOS table. To do this, click on the ``Crop`` button associated with
the video. In this scenario I want to crop Video 1, and click the
``Crop`` button. Once clicked, the first frame of ``Video 1`` pops open.
To draw the region of the video to keep, click and hold the left mouse
button at the top left corner of your rectangular region and drag the
mouse to the bottom right corner of the rectanglar region. If you’re
unhappy with your rectangle, start to draw the rectangle again by
holding the left mouse button at the top left corner of your, new,
revised, rectangle. The previous rectangle will be automatically
discarded. When you are happy with your region, press the keyboard SPACE
or ESC button to save your rectangle. Notice that the ``Crop`` button
associated with Video 1 turns red after I’ve defined the cropped region.

.. image:: img/video_process/crop.gif
  :width: 1000
  :align: center

Chose with types of manipulation you which to perform on each video.
Once done, head to the **EXECUTE** section. To learn more about each
individual manipulation, check out their descriptions in the `SimBA
TOOLS
Guide <https://github.com/sgoldenlab/simba/blob/master/docs/Tutorial_tools.md>`__.

Execute
~~~~~~~

The ``Execute`` section contains three buttons: (i) RESET ALL, (ii) RESET
CROP, and (iii) EXECUTE.

**RESET ALL**: The RESET ALL button puts all the choices back to how
they were when opening the batch processing interface:

.. image:: img/video_process/reset.gif
  :width: 1000
  :align: center

**RESET CROP**: The RESET CROP button removes all crop settings only
(once clicking the ``RESET CROP`` button, you should see any red
``Crop`` button associated the videos go bck to their original color).

**EXECUTE**: The ``EXECUTE`` button initates your chosen manipulations
on each video according the settings in the VIDEO TABLE. The results are
stored in the ``Output Directory`` defined during Step 1 above. Together
with the output files, there is a ``.json`` file that is also saved in
the output directory. This ``.json`` file contains the information on
the manipulations performed on the videos in the VIDEO TABLE. For an
exampple of this .json file, click
`HERE <https://github.com/sgoldenlab/simba/blob/master/misc/batch_process_log.json>`__.

   .. important::
      If you have a lot of videos (>100s), and are performing a lot
      of manipulations, then batch pre-processing videos may take some
      time, and it might be best to make it an over-nighter.

If you have any questions, bug reports or feature requests, please let
us know by opening a new github issue or contact us through gitter and,
we will fix it together!

Author `Simon N <https://github.com/sronilsson>`__
