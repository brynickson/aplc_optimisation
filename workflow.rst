.. _workflow:

Design Survey Workflow
========================

.. warning::

   Pardon our dust, this space is under construction.

Using the `aplc-optimization` toolkit, the workflow for a design survey proceeds as follows:

Creating a launcher script
---------------------------

The `aplc-optimization` tooklkit uses *Launcher scripts* to define and execute design surveys.

*Template* launcher scripts are provided for HiCAT, LUVOIR and GPI.

Make a copy of the appropriate launcher template and rename the copy with the following naming convention::

    do_<instrument_name>_<survey_name>_<machine_name>.py


where <instrument_name> is the name of the instrument/ telescope for which you are apodizing; <survey_name> is the name
of the survey that you are running; and <machine_name> is the name of the machine that the survey will be run on. For example,
a launcher file named '``do_luvoir_BW10_small_telserv3.py``' designates the BW10 small design run on telserv3 for a LUVOIR-type telescope.


Survey information
```````````````````
Set the `instrument`, `survey` and `machine` name parameters to match file name.


Provide survey information parameters including the name of the instument (`instrument`), the
chosen name of the survey (`survey`), and the machine that the survey will be run on (`machine`).


Define input file parameters
``````````````````````````````

 - **nArray** *(int)* - number of pixels in the input (telescope aperture, Lyot stop) and output (apodizer) arrays.
 - **oversamp** *(int)* - oversampling factor used in `evaluate_supersampled() <https://docs.hcipy.org/0.3.1/api/hcipy.field.evaluate_supersampled.html#hcipy.field.evaluate_supersampled>`_, defining the number of gray levels. If set to 1 returns a black and white pupil/ lyot stop. For gray set to > 1, nominally set to 4 (4 grey levels).
 - **gap_padding** *(float)* - arbitratry padding of gap size to represent gaps on smaller arrays. Effectively makes the gaps larger and the segments smaller to preserve the same segment pitch.
 - **lyot_ref_diameter** *(float)* - diameter used to reference the LS inner and outer diameter against.
 - **ls_spid** *(boolean)* - whether to include the secondary support mirror structure in the aperture.
 - **spid_ov** *(int)* - factor by which to oversize the spiders compared to the LUVOUR-A aperture spiders.
 - **ls_id** *(float)* - Lyot stop inner diameter(s) as a fraction of ``lyot_ref_diameter``, re-normalized against circumscribed pupil diameter during the Lyot stop generation
 - **ls_od** *(float)* - Lyot stop outer diameter as a fraction of ``lyot_ref_diameter``, re-normalized against circumscribed pupil diameter during Lyot stop generation


HiCAT
'''''
*General parameters*
 - **nArray** *(int)* - number of pixels in the input (telescope aperture, Lyot stop) and final (apodizer) arrays.
    *Telescope Aperture parameters*
 - **pupil_mask_size** *(float)* - p1 pupil mask size (meters).
 - **pupil_diameter** *(float)* - p3 aperture size (meters).

nArray = 486    # number of pixels in input (TelAP, LS) and final (apodizer) arrays

Define the design survey parameters
-------------------------------------
