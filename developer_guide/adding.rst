.. include:: ../cyverse_rst_defined_substitutions.txt
.. include:: ../custom_urls.txt


|CyVerse_logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

=============================================
Guidelines for adding interactive tools in DE
=============================================

Prerequisites
-------------

Adding VICE Tools in DE is different from non-interactive Tools. VICE applications like Jupyter and RStudio run on an open port for enabling their web UI.

1. Ensure that the listen port for the web UI has a sane default and is set in the Dockerfile.
2. The working directory is set 
3. All commonly needed dependencies are installed in the container image - you will not have `root` privileges later
4. The default user set
5. Disable any additional authentication (CyVerse provides CAS authentication and authorization).
6. URLs will work sanely behind a reverse proxy. If they don't, you may need to add nginx to the container.=


Community images as your base image
-----------------------------------

If you need to set the configurations at all (see above), you'll need to create a new Dockerfile that uses the community-provided image as a base. Your new Dockerfile should deal with custom configurations and dependency installations. 

- Jupyter Lab (https://hub.docker.com/r/cyversevice/jupyterlab-base)
- RStudio Verse (https://hub.docker.com/r/cyversevice/rstudio-verse)
- Shiny Verse (https://hub.docker.com/r/cyversevice/shiny-verse)

See some examples of VICE apps that uses community images as base image in the Dockerfile

- MMTF (https://github.com/sbl-sdsc/mmtf-genomics/blob/master/vice/Dockerfile)
- Rstudio-Bioconductor (https://github.com/cyverse/docker-builds/blob/master/rstudio-bioconductor/Dockerfile)
- Patmatch (https://github.com/fomightez/patmatch-binder/tree/master/vice)

Test your Docker image
----------------------

Since the images are built based using Dockerfile, make sure you test the Dockerfile before providing it to us. Dockerfile must have Entrypoint. If you cannot provide us the Dockerfile, you can request integration of the app by doing a tool request. 

**Fix or improve this documentation:**

- On Github: `Repo link <https://github.com/CyVerse-learning-materials/sciapps_guide>`_
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_

