|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Building VICE tools and apps**
--------------------------------

Once you build your Docker image (following the guidelines), the next step is building the VICE tools. For this you'll need a Docker image, port number, User ID and Working directory.

1. Get the port
===============

You'll need to figure out the port that the tool uses to present its web interface. You can find the ports that a container image exposes with this command 

.. code-block:: bash

  $ docker inspect <image-name>:<image-tag> -f '{{range $port, $val := .ContainerConfig.ExposedPorts}}{{$port}} {{end}}'

.. Note ::

  Replace `<image-name>:<image-tag>` with the correct Docker image

It's possible that multiple or no ports are listed. If that's the case you'll need to refer to the documentation for the tool to figure out the port it uses. Make a note of the port, you'll need it later when putting together the JSON for the tool.

2. Get the UID of the tool's user
=================================

You'll need to figure out the ``UID`` of the of the user the app runs as. Many tools will start up as root and then use another user for the actual process, so it might take a little investigation to figure this out. To start this figure out the user that the container is configured to start up using:

.. code-block:: bash

  $ docker inspect <image-name>:<image-tag> -f '{{.ContainerConfig.User}}'

If you're lucky that will contain the numerical UID of the user. In that case you can make a note of the UID and move on. Otherwise you have more work to do.

The User field can also be empty or set to the username. If its empty, then the user is ``root``. If it's a username then you'll need to get the ``UID`` from inside the container.

To get the ``UID`` for a username run this:

.. code-block:: bash

  $ docker run --rm -it --entrypoint "id" <image-name>:<image-tag> -u <username>

If the User field is empty or ``root``, you need to be sure that the process inside the container actually runs as ``root``. There are a few ways to check this:

* Fire up the container, exec into it, and do a ``ps aux`` to see the user the process is running as.

.. code-block:: bash

  $ docker run -d --name app <image-name>:<image-tag>

  $ docker exec -it app ps aux

* Print out the contents of ``/etc/passwd`` and check for hints:

.. code-block:: bash

  docker run --rm -it --entrypoint "cat" <image-name>:<image-tag> /etc/passwd

* Alternatively check the documentation for the tool.

Make a note of the UID, you'll need it later when putting together the JSON for the tool and app.

3. Get the working directory
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

  Keep in mind that the working directory is where the input files will be made available.

Make a note of the working directory, you'll need it later when putting together the JSON for the tool and app.

4. Construct the Tool JSON
==========================

Next you'll need to create JSON for the new tool. Below is the example of tool Json for JupyterLab VICE app. The JupyterLab example is chosen here since it uses all of the bits of information that you gathered above:

.. code-block :: bash

  {"tools": [{
        "id" : "2F76C33D-0F70-4107-A2A2-3177468CC829",
        "description" : "Jupyter Lab based on jupyter/datascience-notebook",
        "interactive" : true,
        "name" : "jupyter-lab-datascience-notebook",
        "type" : "interactive",
        "restricted" : false,
        "container" : {
            "min_cpu_cores" : 0.1,
            "max_cpu_cores" : 2.0,
            "memory_limit" : 4000000000,
            "interactive_apps" : {
                "image" : "discoenv/cas-proxy",
                "name" : "cas-proxy",
                "cas_url" : "https://auth.iplantcollaborative.org/cas4/",
                "cas_validate" : "validate"
            },
            "container_ports" : [{
                "container_port" : 8888
            }],
            "network_mode" : "bridge",
            "skip_tmp_mount" : true,
            "working_directory" : "/home/jovyan/",
            "image" : {
                "name" : "test/jupyter-lab",
                "tag" : "beta"
            },
            "uid" : 1000
        },
        "version" : "0.0.1",
        "implementation" : {
            "implementor" : "John Wregglesworth",
            "implementor_email" : "wregglej@cyverse.org",
            "test" : {
                "input_files" : [],
                "output_files" : []
            }
        }
   }]}

- ``id`` is a string and must be a UUID. A value can be generated at https://www.uuidgenerator.net/.

- ``description`` is a string and must be set to the desired description of the tool. This will appear in the DE's tool listing dialog.

- ``name`` is a string and must be set ot the desired name of the tool. This will appear in the DE's tool listing dialog.

- ``container_ports`` must be a list of maps with only a single entry. The key in that entry must be container_port and should be filled in with the number value you gathered in a previous section.

- ``container.working_directory`` is a string and must be filled in with the value you gathered in a previous section. The default is ``/.``

- ``container.image.name`` is a string and must be the image specifier minus the image tag. The image must exist on Dockerhub.

- ``container.image.tag`` is a string and must be the image tag.

- ``container.uid`` is a number and must be filled in with the value you gathered in a previous section.

- ``version`` is a string and must be filled in with the version of the tool. This will appear in the DE's tool listing dialog.

- ``implementation.implementor`` is a string and must be filled in with your name or the name of the organization you work for.

- ``implementation.implementor_email`` is a string and must be filled in with your email or the email address of the organization you work for.

- ``implementation.test`` is a map and must exist. You can get away with setting exactly like it is in the example above.

Leave the rest of the fields as they are and then you can request a new tool to be added in DE by filling up Tool request form in DE - https://wiki.cyverse.org/wiki/display/DEmanual/Adding+or+Requesting+a+New+Tool

.. Note ::

  Copy and past the tool JSON in the "Enter any other information that might be useful" box:

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

.. |CyVerse logo| image:: ../img/cyverse_rgb.png
    :width: 500
    :height: 100
.. _CyVerse logo: http://learning.cyverse.org/
.. |Home_Icon| image:: ../img/homeicon.png
    :width: 25
    :height: 25
.. _Home_Icon: http://learning.cyverse.org/