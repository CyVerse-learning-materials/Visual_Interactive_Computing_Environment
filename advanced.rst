|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Advanced**
------------

Adding VICE tools and apps in DE
================================

Figure out if you're going to need additional configuration for the tool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some tools will require additional configuration in order to get them working correctly with the VICE feature. Some things you'll need/want to configure:

- Ensure that the listen port for the web UI has a sane default and is set.
- Ensure that the working directory is sane and working.
- Ensure that the commonly needed dependencies are installed in the container image.
- Ensure that the default user is already available.
- If possible, disable authentication (we provide CAS authentication and authorization).
- Make sure the URLs will work sanely behind a reverse proxy. If they don't you may need to add nginx to the container.

Create a new container image using the community one as a base
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you need to set the configurations at all (see above), you'll need to create a new Dockerfile that uses the community provided image as a base. Your new Dockerfile should deal with custom configurations and dependency installations.

Some examples are available here:

https://github.com/cyverse-de/dockerfiles/tree/master/shiny
https://github.com/cyverse-de/dockerfiles/tree/master/rstudio-nginx/3.5.0
https://github.com/cyverse-de/dockerfiles/tree/master/jupyter/lab/beta

.. Note::

	The rstudio-nginx one is the more complicated one out of the three

Provide us the Dockerfile
~~~~~~~~~~~~~~~~~~~~~~~~~

Since the images are built based on Dockerfile, make sure you test out the Dockerfile before providing that to us. Dockerfile must have Entrypoint

Request VICE apps in DE
=======================

If you cannot provide us the Dockerfile, you can request what app should be integrated by doing tool request - 


**Fix or improve this documentation:**

- On Github: `Repo link <https://github.com/CyVerse-learning-materials/sciapps_guide>`_
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_

----

  |Home_Icon|_
  `Learning Center Home <http://learning.cyverse.org/>`_

.. |CyVerse logo| image:: ./img/cyverse_rgb.png
    :width: 500
    :height: 100
.. _CyVerse logo: http://learning.cyverse.org/
.. |Home_Icon| image:: ./img/homeicon.png
    :width: 25
    :height: 25
.. _Home_Icon: http://learning.cyverse.org/



