.. _workflow:

Design Survey Workflow
========================

.. warning::

   Pardon our dust, this space is under construction.

Using the `aplc-optimization` toolkit, the workflow for a design survey proceeds as follows:

Create a launcher script
---------------------------

The `aplc-optimization` tooklkit uses *Launcher scripts* to define and execute design surveys.

*Template* launcher scripts are provided for HiCAT, LUVOIR and GPI.

Make a copy of the appropriate launcher template and rename the copy with the following naming convention::

    do_<instrument>_<survey>_<machine>.py


where <instrument> is the name of the instrument/ telescope for which you are apodizing; <survey> is the name
of the survey that you are running; and <machine> is the name of the machine that the survey will be run on. For example,
a launcher file named '``do_luvoir_BW10_small_telserv3.py``' designates the BW10 small design run on telserv3 for a LUVOIR-type telescope.

Inside the launcher script define the design parameters to survey according to the template you have selected
- these include a list of telescope aperture specifications, tolerance constraints, focal plane mask size, Lyot stop dimensions,
and contrast and bandwidth goals. Any unspecified parameters are set to reasonable default values.

Run the launcher script
------------------------

Run the launcher script using the following command in terminal::

    (aplc-optimization) $ python do_<instrument>_<survey>_<machine>.py

If all goes well, this should provide you with the following output::

    This survey has # design parameter combinations.
    # parameter are varied:

    File organization:
    {'analysis_dir': '../aplc-optimization/surveys/<instrument>_<survey>_<machine>/analysis',
     'drivers_dir': '../aplc-optimization/surveys/<instrument>_<survey>_<machine>/drivers',
     'input_files_dir': '../aplc-optimization/masks',
     'log_dir': '../aplc-optimization/surveys/<instrument>_<survey>_<machine>/logs',
     'solution_dir': '../aplc-optimization/surveys/<instrument>_<survey>_<machine>',
     'survey_dir': '../aplc-optimization/surveys/<instrument>_<survey>_<machine>'}


    All input files exist? False
    All drivers exist? False
    All solutions exist? False

where "File organization" indicates the location within which the survey results and intermediate products are stored; and the boolean provided after
"All Input Files exist?", "All drivers exist?" and "All solutions exist" indicate whether the input mask files, drivers and solutions already exist, respectively.

Inspect the products
------------------------------
Input mask files
'''''''''''''''''
Once launched, the script first runs a "check" routine to verify whether the necessary static input files defining the
telescope aperture and lyot stop masks, according to the input file parameters set, are in place. If they do not, the program will call the
corresponding input file generation script.

Output products
''''''''''''''''
Once the survey is executed, the following output products are written to disk: a re-usable python driver script storing
the parameters and file organization defined in the launcher script and in turn calls the optimizer (stored in `drivers_dir`); an automatically produced file that contains a record of events
while the optimizer runs (stored in `log_dir`); the optimized apodizer solution (stored in `solution_dir`); and a PDF of the analysis products (in `analysis_dir`).

