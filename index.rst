.. include:: cyverse_rst_defined_substitutions.txt
.. include:: custom_urls.txt

|CyVerse_logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

VICE Documentation
==================

The Visual and Interactive Computing Environment (VICE) is the latest feature in CyVerse's Discovery Environment (DE) for running interactive applications. 

**User Guide** instructs users on basic functions of the DE: (a) how to launch an interactive app, (b) bring your data into the container, (c) run an analysis, and (d) save or upload your results to the cloud.

**Developer Guide** gives advanced tips about how to (a) build your own VICE-ready containers, (b) host them on a public registry, and (c) integrate them into VICE and make them available to your user community.

Last, we provide a brief list of featured VICE apps in the DE.

.. toctree::
   :maxdepth: 1
   :caption: Getting Started

   getting_started/about
   getting_started/prerequisites
   getting_started/apptypes

.. toctree::
   :maxdepth: 1
   :caption: User Guide

   user_guide/quick-cloudshell
   user_guide/quick-jupyter
   user_guide/quick-rstudio
   .. user_guide/quick-rshiny
   user_guide/sharing

.. toctree::
   :maxdepth: 1
   :caption: Developer Guide

   developer_guide/workflow
   developer_guide/adding
   developer_guide/building

.. toctree::
   :maxdepth: 1
   :caption: VICE Apps
   
   vice_apps/examples

.. toctree::
   :maxdepth: 1
   :caption: Getting Help

   getting_help/faq
   getting_help/bestpractices
   getting_help/tool_troubleshooting
   getting_help/contact

..
	#### Comment:This tutorial can have multiple pages. The Table of Contents assumes
	you have an additional page called 'First Step' with content located in 'step1.rst'.
	Copy step1.rst. step2.rst has slightly different formatting to end the document.
	Edit these titles and filenames as needed ####

----

**Fix or improve this documentation**

- Search for an answer:
  |CyVerse Learning Center|
- Ask us for help:
  click |Intercom| on the lower right-hand side of the page
- Report an issue or submit a change:
  |Github Repo Link|
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_


.. Comment: images

.. |CyVerse_logo| image:: ./img/cyverse_learning.png
    :width: 500

.. _CyVerse_logo: http://learning.cyverse.org/

.. |Home_Icon| image:: ./img/homeicon.png
    :width: 25
    :height: 25

.. _Home_Icon: http://learning.cyverse.org/

.. |Intercom| image:: ./img/intercom.png
    :width: 25
    :height: 25
