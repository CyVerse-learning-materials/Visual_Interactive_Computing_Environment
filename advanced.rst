|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Adding VICE tools and apps in DE**
------------------------------------

Adding VICE tools and apps in DE is different from adding regular DE tools and apps. Unlike regular DE tools and apps, the process is not automated. For now, you'll have to follow certain guidelines which are listed below:

**1. Figure out if you're going to need additional configuration for the tool**

Some tools will require additional configuration in order to get them working correctly with the VICE feature. So please make sure  

- To ensure that the listen port for the web UI has a sane default and is set.
- To ensure that the working directory is sane and working.
- To ensure that the commonly needed dependencies are installed in the container image.
- To ensure that the default user is already available.
- To disable authentication (CyVerse provides CAS authentication and authorization).
- URLs will work sanely behind a reverse proxy. If they don't, you may need to add nginx to the container.

**2. Create a new Docker image using the community one as a base image**

If you need to set the configurations at all (see above), you'll need to create a new Dockerfile that uses the community-provided image as a base. Your new Dockerfile should deal with custom configurations and dependency installations. Some examples are available here:

- https://github.com/cyverse-de/dockerfiles/tree/master/shiny
- https://github.com/cyverse-de/dockerfiles/tree/master/rstudio-nginx/3.5.0
- https://github.com/cyverse-de/dockerfiles/tree/master/jupyter/lab/beta

.. Note::

	The rstudio-nginx example is the more complicated one out of the three above.

**3. Test your Docker image**

Since the images are built based using Dockerfile, make sure you test the Dockerfile before providing it to us. Dockerfile must have Entrypoint. If you cannot provide us the Dockerfile, you can request integration of the app by doing a tool request. 

Once you have fulfilled all the above requirements, the next step is `building VICE tools and apps <>`_

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



