.. _introduction:

###################################################
Introduction
###################################################

``aplc-optimization`` is a software toolkit developed to simplify the organization, execution and evaluation of apodized
pupil Lyot coronagraph design surveys.


Apodized Pupil Lyot Coronagraphs (APLCs)
=========================================

The apodized pupil Lyot coronagraph (APLC) is one of several coronagraph design families that the community is
assessing as part of NASAs Exoplanet Exploration Program Segmented aperture coronagraph design and analysis (SCDA) team.
The APLC is a Lyot-style coronagraph that suppresses starlight through a series of amplitude operations on the on-axis field.
A diagram of the APLC concept is shown in Figure 1. The mask architecture combines an entrance pupil apodization in plane A,
a downstream focal plane mask (FPM) in plane B, and the Lyot stop in the relayed pupil plane C to form the coronagraphic
image on a detector located in the re-imaged focal plane D. A perfect solution is when the transmission profile of the
apodizer in plane A is optimized so that the two scalar field ocmonents of the field in the Lyot plane approximately cancel.


APLCs are sensitive to several design parameters: telescope aperture shape and segmentation, central obscuration,
lyot stop shape and size, focal plane mask size, dark hole size, and bandwidth. To map the multi-dimensional parameter
space, ``aplc-optimization`` has been developed to manage large sets of mask optimization programs and execute them
on a computing cluster.

Design Survey Strategy
========================
Apodizer optimization
---------------------
Our optimization method stems from the one originally devised for the shaped pupil coronagraph:
a linear program determines the apodizer/shaped pupil with maximum transmission, given a contrast goal and dark zone
bounds. This linear optimization approach was adapted to the APLC design case by exmapnding the numberical propogation model to include
the masks at intermediate planes. A detailed







.. warning::

   Pardon our dust, this space is under construction.




*********************
Algorithms Overview
*********************

***************************
aplc-optimization workflow
***************************
Once you have installed the software, we recommend you begin with the ``aplc-optimization`` workflow guide.


