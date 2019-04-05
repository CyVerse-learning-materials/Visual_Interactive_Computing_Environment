|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Building VICE tools and apps**
--------------------------------

Once you build your Docker image (following the guidelines), the next step is building the VICE tools. For this you'll need a Docker image, port number, User ID and Working directory.

1. Docker image
===============

The Docker image of your tool is mandatory and it should be available on public registries such as `Dockerhub <https://hub.docker.com>`_ or `quay.io <http://quay.io>`_. Alternatively you can provide us the Dockerfile and we will build the Docker image for you. If there is no Dockerfile for the tool that you are interested in, then tell us what tool you are interesting in making us as VICE app.

2. Get the port
===============

You'll need to figure out the port that the tool uses to present its web interface. This is mandatory and you can integrate a tool without knowing the port it runs on. If you don't know, you can find the ports that a container image exposes with this command

.. code-block:: bash

  $ docker inspect <image-name>:<image-tag> -f '{{range $port, $val := .ContainerConfig.ExposedPorts}}{{$port}} {{end}}'

.. Note ::

  Replace `<image-name>:<image-tag>` with the your Docker image

It's possible that multiple or no ports are listed. If that's the case you'll need to refer to the documentation for the tool to figure out the port it uses. Make a note of the port, you'll need it later when integrating the tool in DE.
Here are the tools and their ports for common tools such as Jupyter notebook, Rstudio and Shiny. If you are developing any applications based on these tools, you can use these ports while integrating the tool in DE.

+------------+---------+
| Type       | Port    |
+------------+---------+
| Jupyter    | 8888    |
+------------+---------+
| Rstudio    | 80      |
+------------+---------+
| Shiny      | 3838    |
+------------+---------+

3. Get the UID of the tool's user
=================================

You'll need to figure out the ``UID`` of the of the user the app runs as. Many tools will start up as root and then use another user for the actual process, so it might take a little investigation to figure this out. To start this figure out the user that the container is configured to start up using:

.. code-block:: bash

  $ docker inspect <image-name>:<image-tag> -f '{{.ContainerConfig.User}}'

If you're lucky that will contain the numerical UID of the user. In that case you can make a note of the UID and move on. Otherwise you have more work to do. The User field can also be empty or set to the username. If its empty, then the user is ``root``. If it's a username then you'll need to get the ``UID`` from inside the container.

To get the ``UID`` for a username run this:

.. code-block:: bash

  $ docker run --rm -it --entrypoint "id" <image-name>:<image-tag> -u <username>

.. Note ::

  Replace `<image-name>:<image-tag>` with the your Docker image

If the User field is empty or ``root``, you need to be sure that the process inside the container actually runs as ``root``. There are a few ways to check this:

* Fire up the container, exec into it, and do a ``ps aux`` to see the user the process is running as.

.. code-block:: bash

  $ docker run -d --name app <image-name>:<image-tag>

  $ docker exec -it app ps aux

* Print out the contents of ``/etc/passwd`` and check for hints:

.. code-block:: bash

  docker run --rm -it --entrypoint "cat" <image-name>:<image-tag> /etc/passwd

* Alternatively check the documentation for the tool.

.. Note::

  The UID of the tool can be empty but setting the UID will make sure that the user can write to the input files in the container.

Make a note of the UID, you'll need it later when putting together the JSON for the tool and app. 

4. Get the working directory
============================

You'll need the working directory for the process in the tool container, which may not correspond to the default working directory for the container.

To get the default working directory for the container run this:

.. code-block:: bash

  $ docker inspect <image-name>:<image-tag> -f '{{.ContainerConfig.WorkingDir}}'

* If that prints out an empty string, then the default working directory is ``/.``

* If the container fires up as root but the tool runs as another user, then the working directory may need to be that user's home directory.

* If the container changes to another directory after it starts up, then the working directory may need to be that directory.

* If all else fails, check the documentation and/or try out the container locally to figure out what it does.

.. Important ::

  Keep in mind that the working directory is where the input files will be made available. Similar to UID, working directory is not mandatory but given jupyter lab's default behavior of showing things in subdirectories of the place it's started. So if you're loading notebooks and data from the Datastore, you want the working directory (where those files are loaded into the container) to be in the right spot

Make a note of the working directory, you'll need it later when putting together the JSON for the tool and app.

5. Add Tool in DE 
=================

The final step in building the VICE tool is to fill up the "Add Tool" form in DE.

Brifely here are the following steps.

* Log in CyVerse `Discovery Environment <https://de.cyverse.org/de/>`_

* Click on the Apps window and click Manage Tools button on the far right hand side of the window

* Click on Tools button and then finally Add Tools button

You'll see a Add Tool form like this

|add-tools|

- ``Tool name`` is the name of the tool. This will appear in the DE's tool listing dialog. This is mandatory field. Eg. "jupyterlab-circos"

- ``description`` is a brief description of the tool. This will appear in the DE's tool listing dialog. Eg. "Circos is a software package for visualizing data and information that was created by Martin Krzywinski"

- ``version`` is the version of the tool. This will appear in the DE's tool listing dialog. This is mandatory field. Eg. "1.0"

- ``Image name`` is the name of the image specifier minus the image tag. The image must exist on Dockerhub or quay.io. This is mandatory field. E.g "fomightez/circos-vice"

- ``Tag`` is the image tag. If you don't specify the tag, the DE will look for the "latest" tag which is the default tag.

- ``Docker Hub URL`` is the url of the image on the Dockerhub. E.g https://hub.docker.com/r/fomightez/circos-vice

- ``Type`` is the type of Tool. For VICE apps, chose "interactive".

- ``OSG Image Path`` is path of the image on the OSG. You can skip this for interactive tools.

- ``Entrypoint`` is the Entrypoint for your tool. Entrypoint should be present in the Docker image and if not, you should specify it here.

- ``Working Directory`` this is the working directory of the tool and must be filled in with the value you gathered above. E.g /home/jovyan/vice

- ``UID`` is a number and must be filled in with the value you gathered from above. E.g 1000

- ``Max CPU Cores`` is the number of cores for your tool. Eg. 4

- ``Memory Limit`` is the memory for your tool. Eg. 16 GB

- ``Min Disk Space`` is the minimum disk space. Eg. 266 GB

- ``Container Ports`` must be a list of maps with only a single entry. The key in that entry must be container_port and should be filled in with the number value you gathered above.

5. Creating VICE app for your tool
==================================

To create a new app, follow the instructions in `here <https://wiki.cyverse.org/wiki/display/DEmanual/Designing+the+Interface>`_

----

**Fix or improve this documentation:**

- On Github: `Repo link <https://github.com/CyVerse-learning-materials/sciapps_guide>`_
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_

----

  |Home_Icon|_
  `Learning Center Home <http://learning.cyverse.org/>`_

.. |add-tools| image:: ../img/add-tools.png

.. |CyVerse logo| image:: ../img/cyverse_rgb.png
    :width: 500
    :height: 100
.. _CyVerse logo: http://learning.cyverse.org/
.. |Home_Icon| image:: ../img/homeicon.png
    :width: 25
    :height: 25
.. _Home_Icon: http://learning.cyverse.org/
