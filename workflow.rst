.. _workflow:

Workflow
============================

.. warning::

   Pardon our dust, this space is under construction.

Create a launcher file
----------------------------

The launcher file is a script that creates
set the survey parameters,
launcher templates are provided for LUVOIR and HICAT, these scripts are not designed to be run,m but are provided as templates only.

~~~ About launcher file. ~~~

Make a copy of the appropriate launcher template and rename the copy with the following naming convention::

    do_<instrument_name>_<survey_name>_<machine_name>.py


where <instrument_name> is the name of the instrument/ telescope for which you are apodizing; <survey_name> is the name
of the survey that you are running; and <machine_name> is the name of the machine that the survey will be run on. For example,
a launcher file named '``do_luvoir_BW10_small_telserv3.py``' designates the BW10 small design run on telserv3 for a LUVOIR-type telescope.

.. note::

    launcher script templates are already provided for LUVOIR and HiCAT. If planning to create a LUVOIR or HiCAT APLC,
    make a copy of the appropriate launcher template script.

Customize launcher script
--------------------------

Customize the launcher script, depending on the instrument chosen:

LUVOIR Launcher script
'''''''''''''''''''''''

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

# Aperture parameters
pupil mask_size = 19.85e-3 #m: p1 pupil mask size
pupil_diameter = 19.725e-3 #m: p3 apodizer size
ap_spiders = True  # include secondary support mirror structure in the aperture
ap_gaps = True   # include the gaps between individual segments in the aperture
ap_grey = False # grey pupil, else b&w

# Lyot stop parameters
ls_inner = 6.8e-3 #m: P5 lyot stop mask central segment size
ls_outer = 15.9e-3 #m: p5 lyot stop size
ls_spiders = True  # whether to include secondary support mirror structure in the aperture
ls_grey = True  # grey lyot stop, else b&w
The next step is to define the parameters for the generation of the input files.

 - **nArray** *(int)* **-** number of pixels in the input (telescope aperture, Lyot stop) and output (apodizer) arrays. </br>
 - **nArray** *(int)* **-** number of pixels in the input (telescope aperture, Lyot stop) and output (apodizer) arrays.
 - **nArray** *(int)* **-** number of pixels in the input (telescope aperture, Lyot stop) and output (apodizer) arrays.
 - **nArray** *(int)* **-** number of pixels in the input (telescope aperture, Lyot stop) and output (apodizer) arrays.

.. py:function:: input_files_dict[]

   :py:obj:`input_files_dict` is a python dictionary containing the input parameters for the telescope aperture and lyot stop file generation---these parameters are to be defined as follows:

   :param str directory: (*value pre-set and not to be altered*) the name of the folder located in *'aplc-optmization/MASKS/'* within which the input files are stored.
   :param int N: set to the number of pixels in the input and output arrays
   :param int oversamp: set the oversampling level (i.e. the number of grey levels).
   .. py:function:: aperture[]

        :py:obj:`aperture` is a nested dictionary containing the input parameters for the generation of the telescope aperture. These parameters should be defined as follows:

        :param int seg_gap_pad: set the arbitrary padding of gap size to represent gaps on smaller arrays - this effectively makes the gaps larger and the segments smaller to preserve the same segment pitch.
   .. py:function:: lyot_stop[]

    :py:obj:`lyot_stop` is a nested dictionary containing the input parameters for the Lyot stop generation.  These parameters should be defined as follows:

    :param float lyot_ref_diam: define the Lyot reference diameter.
    :param bool ls_spid: opt whether to include secondary mirror support structure in the aperture.
    :param int ls_spid_ov: set to the factor by which to oversize the spiders.
    :param float LS_ID: set to the fractional size of the Lyot stop's circular central obstruction as fraction of the reference diameter (**LS_ref_diam**)
    :param float LS_OD: set to the fractional size of the circular outer edge of the Lyot stop as fraction of the reference diameter (**LS_ref_diam**).

The values set in :py:obj:'input_files_dict' dictionary are passed to the :py:func:`LUVOUR_input_gen()` function to create the input telescope pupil and lyot stop, which are saved as fits files with the
filenames ``pup_filename`` and ``ls_filenames``, located in the ``'MASKS/<directory>'`` folder.

Define the design survey parameters
-------------------------------------
