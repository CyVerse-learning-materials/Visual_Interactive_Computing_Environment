|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Building VICE tools and apps**
--------------------------------

Get the port
============

You'll need to figure out the port that the tool uses to present its web interface. You can find the ports that a container image exposes with this command (replace `gims.cyverse.org:5000/<image-name>:<image-tag>` with the correct container image):

.. code-block:: bash

  $ docker inspect gims.cyverse.org:5000/<image-name>:<image-tag> -f '{{range $port, $val := .ContainerConfig.ExposedPorts}}{{$port}} {{end}}'

It's possible that multiple or no ports are listed. If that's the case you'll need to refer to the documentation for the tool to figure out the port it uses.

Make a note of the port, you'll need it later when putting together the JSON for the tool and app.

Get the UID of the tool's user
==============================

You'll need to figure out the `UID` of the of the user the app runs as. Many apps will start up as root and then use another user for the actual process, so it might take a little investigation to figure this out.

To start with figure out the user that the container is configured to start up using:

.. code-block:: bash

  $ docker inspect gims.cyverse.org:5000/<image-name>:<image-tag> -f '{{.ContainerConfig.User}}'

If you're lucky that will contain the numerical UID of the user. In that case you can make a note of the UID and move on. Otherwise you have more work to do.

The User field can also be empty or set to the username. If its empty, then the user is ``root``. If it's a username then you'll need to get the ``UID`` from inside the container.

To get the ``UID`` for a username (replace the image tag and username as needed):

.. code-block:: bash

  $ docker run --rm -it --entrypoint "id" gims.cyverse.org:5000/<image-name>:<image-tag> -u <username>

If the User field is empty or root, you need to be sure that the process inside the container actually runs as root. There are a few ways to check this:

- Fire up the container, exec into it, and do a ``ps aux`` to see the user the process is running as.

.. code-block:: bash

  $ docker run -d --name app gims.cyverse.org:5000/<image-name>:<image-tag>

  $ docker exec -it app ps aux

- Print out the contents of ``/etc/passwd`` and check for hints:

.. code-block:: bash

  docker run --rm -it --entrypoint "cat" gims.cyverse.org:5000/<image-name>:<image-tag> /etc/passwd

- Check the documentation for the tool.

Make a note of the UID, you'll need it later when putting together the JSON for the tool and app.

Get the working directory
=========================

You'll need the working directory for the process in the tool container, which may not correspond to the default working directory for the container.

To get the default working directory for the container:

.. code-block:: bash

  $ docker inspect gims.cyverse.org:5000/<image-name>:<image-tag> -f '{{.ContainerConfig.WorkingDir}}'

- If that prints out an empty string, then the default working directory is ``/.``

- If the container fires up as root but the tool runs as another user, then the working directory may need to be that user's home directory.

- If the container changes to another directory after it starts up, then the working directory may need to be that directory.

- If all else fails, check the documentation and/or try out the container locally to figure out what it does.

- Keep in mind that the working directory is where the input files will be made available.

- Make a note of the working directory, you'll need it later when putting together the JSON for the tool and app.

Construct the JSON
==================

**Tool JSON**
~~~~~~~~~~~~~

First you'll need to create JSON for the new tool. The jupyter-lab image example is chosen here since it uses all of the bits of information that you gathered above:

.. code-block:: bash

  {
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
              "name" : "gims.cyverse.org:5000/jupyter-lab",
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
  }

- ``id`` is a string and must be a UUID. A value can be generated at https://www.uuidgenerator.net/.

- ``description`` is a string and must be set to the desired description of the tool. This will appear in the DE's tool listing dialog.

- ``interactive`` is a boolean and must be ``true``.

- ``name`` is a string and must be set ot the desired name of the tool. This will appear in the DE's tool listing dialog.

- ``type`` is a string and must be ``interactive``.

- ``restricted`` is a boolean and must be ``false``.

- ``container.min_cpu_cores`` is a number and should be ``0.1``.

- ``container.max_cpu_cores`` is a number and should be should be ``2.0``.

- ``container.memory_limit`` is a number and should be ``4000000000``. Its unit is bytes.

- ``container.interactive_apps`` must be filled out exactly as it is above.

- ``container_ports`` must be a list of maps with only a single entry. The key in that entry must be container_port and should be filled in with the number value you gathered in a previous section.

- ``container.network_mode`` is a string and must be ``bridge``.

- ``container.skip_tmp_mount`` is a boolean and should be ``true``. It tells the ``interapps-runner`` utility to skip mounting the ``/tmp`` from the hosts working directory, which causes issues in a number of VICE apps.

- ``container.working_directory`` is a string and must be filled in with the value you gathered in a previous section. The default is ``/.``

- ``container.image.name`` is a string and must be the image specifier minus the image tag. It should start with ``gims.cyverse.org:5000/`` since you should have pushed the image to our local container image repository.

- ``container.image.tag`` is a string and must be the image tag.

- ``container.uid`` is a number and must be filled in with the value you gathered in a previous section.

- ``version`` is a string and must be filled in with the version of the tool. This will appear in the DE's tool listing dialog.

- ``implementation.implementor`` is a string and must be filled in with your name or the name of the organization you work for.

- ``implementation.implementor_email`` is a string and must be filled in with your email or the email address of the organization you work for.

- ``implementation.test`` is a map and must exist. You can get away with setting exactly like it is in the example above.

**App JSON**
~~~~~~~~~~~~~

Next up is the App JSON:

.. code-block:: bash

  {
    "id": "5DB1D48C-B484-44DE-A6D7-31B1039989CB",
    "name": "jupyter-lab",
    "description": "Jupyter Lab based on jupyter/datascience-notebook",
    "system_id": "de",
    "tools": [
      {
        "name": "jupyter-lab-datascience-notebook",
        "deprecated": false,
        "type": "interactive",
        "description": "Jupyter Lab based on jupyter/datascience-notebook",
        "id": "2F76C33D-0F70-4107-A2A2-3177468CC829",
        "version": "0.0.1"
      }
    ],
    "references": [],
    "groups": [
      {
        "id": "633384F8-C882-4986-B872-D65BE9B1A541",
        "name": "Parameters",
        "label": "Input Files and Folders",
        "isVisible": true,
        "parameters": [
          {
            "description": "Select a folder to load as input.",
            "name": "",
            "type": "FolderInput",
            "omit_if_blank": false,
            "validators": [],
            "label": "Input Folder",
            "id": "e85cb31f-9442-43c0-9509-b3b040b9abbb",
            "file_parameters": {
              "format": "Unspecified",
              "file_info_type": "File",
              "is_implicit": true,
              "repeat_option_flag": false,
              "data_source": "file",
              "retain": false
            },
            "order": 0,
            "isVisible": true,
            "defaultValue": null,
            "required": false
          }
        ]
      }
    ]
  }


- ``id`` is a string and must be a UUID. A value can be generated at https://www.uuidgenerator.net/.

- ``name`` is a string and must be set to the desired name for the app. This will show up in the DE's Apps window.

- ``description`` is a string and must be set to the desired description for the app. This will show up in the DE's Apps window.

- ``system_id`` is a string and must be set to ``de``.

- ``tools`` is a list of maps and must contain a single entry.

- ``tools[0].name`` is a string and must be the same as the name field in the tool JSON. ``tools[0].deprecated`` is a boolean and must be false.

- ``tools[0].type`` is a string and must be the same as thetypefield in the tool JSON, which should be ``interactive``.

-  ``tools[0].description`` is a string must be the same as the description field in the tool JSON.

- ``tools[0].id`` is a string and must be the same as the ``id`` field in the tool JSON.

- ``tools[0].version`` is a string and must be the same as the ``version`` field in the tool JSON.

- ``references`` is a list and must be present, though it can be empty.

- ``groups`` is a list of maps parameters can be set. You'll need at least one entry to allow for input directories to be selected.

- ``groups[0].id`` is a string and must be a UUID. A value can be generated at https://www.uuidgenerator.net/.

- ``groups[0].name`` is a string and must be the desired name of group.

- ``groups[0].label`` is a string and must be the desired label shown in the DE's UI when launching the app.

- ``groups[0].isVisible`` is a boolean and must be true.

- ``groups[0].parameters`` is a list of maps that must contain at least one entry. You can copy-paste the example provided here, but you must change itsid` field to be a new UUID. A value can be generated at https://www.uuidgenerator.net/.

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