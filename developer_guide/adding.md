> \<a href=\"<https://atmo.cyverse.org>\"
> target=\"blank\"\>Atmosphere\</a>

> \<a
> href=\"<https://wiki.cyverse.org/wiki/display/atmman/Atmosphere+Manual+Table+of+Contents>\"
> target=\"blank\"\>Atmosphere Manual\</a>

> \<a
> href=\"<https://learning.cyverse.org/projects/atmosphere-guide/en/latest/>\"
> target=\"blank\"\>Atmosphere Guide\</a>

> \<a href=\"<https://bisque.cyverse.org/client_service/>\"
> target=\"blank\"\>BisQue\</a>

> \<a href=\"<https://wiki.cyverse.org/wiki/display/BIS>\"
> target=\"blank\"\>BisQue Manual\</a>

> \<a href=\"<https://user.cyverse.org/>\" target=\"\_blank\"\>CyVerse
> User Portal\</a>

> \<a href=\"<http://learning.cyverse.org>\" target=\"blank\"\>CyVerse
> Learning Center\</a>

> \<a href=\"<https://wiki.cyverse.org>\" target=\"blank\"\>CyVerse
> Wiki\</a>

> \<a href=\"<http://www.cyverse.org/data-store>\"
> target=\"\_blank\"\>Data Store\</a>

> \<a
> href=\"<https://wiki.cyverse.org/wiki/display/DS/Data+Store+Table+of+Contents>\"
> target=\"blank\"\>Data Store Manual\</a>

> \<a
> href=\"<https://learning.cyverse.org/projects/data_store_guide/en/latest/>\"
> target=\"blank\"\>Data Store Guide\</a>

> \<a href=\"<https://de.cyverse.org/de/>\" target=\"blank\"\>Discovery
> Environment\</a>

> \<a
> href=\"<https://wiki.cyverse.org/wiki/display/DEmanual/Table+of+Contents>\"
> target=\"blank\"\>DE Manual\</a>

> \<a
> href=\"<http://learning.cyverse.org/projects/cyverse-discovery-environment-guide/>\"
> target=\"blank\"\>Discovery Environment Guide\</a>

> \<a href=\"<https://dnasubway.cyverse.org/>\" target=\"blank\"\>DNA
> Subway\</a>

> \<a
> href=\"<https://learning.cyverse.org/projects/dnasubway_guide/en/latest/>\"
> target=\"blank\"\>DNA Subway Manual\</a>

> \<a
> href=\"<https://learning.cyverse.org/projects/dnasubway_guide/en/latest/>\"
> target=\"blank\"\>DNA Subway Guide\</a>

> \<a href=\"<https://www.sciapps.org/>\" target=\"blank\"\>SciApps\</a>

> \<a
> href=\"<https://learning.cyverse.org/projects/sciapps_guide/en/latest/>\"
> target=\"blank\"\>SciApps Manual\</a>

> \<a
> href=\"<https://learning.cyverse.org/projects/sciapps_guide/en/latest/>\"
> target=\"blank\"\>SciApps Guide\</a>

> \<a href=\"<https://cyverse-de.github.io/api/>\"
> target=\"blank\"\>Terrain DE API Docs\</a>

> \<a href=\"<https://www.tacc.utexas.edu/tapis>\"
> target=\"blank\"\>Tapis TACC API\</a>

> \<a href=\"<http://ask.iplantcollaborative.org/questions>\"
> target=\"blank\"\>Ask CyVerse\</a>

> \<a href=\"<http://learning.cyverse.org/en/latest/>\"
> target=\"blank\"\>Agave Guide\</a>

> \<a href=\"<http://developer.agaveapi.co/#introduction>\"
> target=\"blank\"\>Agave API\</a>

> \<a href=\"<https://agaveapi.co>\" target=\"blank\"\>Agave Live
> Docs\</a>

> \<a href=\"<http://learning.cyverse.org/en/latest/>\"
> target=\"blank\"\>BisQue Guide\</a>

> \<a
> href=\"<https://github.com/CyVerse-learning-materials/Visual_Interactive_Computing_Environment>\"
> target=\"blank\"\>Github Repo Link\</a>

> \<a href=\"<https://hub.docker.com/u/jupyter>\"
> target=\"blank\"\>Project Jupyter Images\</a>

\_

\_ [Learning Center Home](http://learning.cyverse.org/)

# Guidelines for adding interactive tools in DE

## Prerequisites

Adding VICE Tools in DE is different from non-interactive Tools. VICE
applications like Jupyter and RStudio run on an open port for enabling
their web UI.

1.  Ensure that the listen port for the web UI has a sane default and is
    set in the Dockerfile.
2.  The working directory is set
3.  All commonly needed dependencies are installed in the container
    image - you will not have [root]{.title-ref} privileges later
4.  The default user set
5.  Disable any additional authentication (CyVerse provides CAS
    authentication and authorization).
6.  URLs will work sanely behind a reverse proxy. If they don\'t, you
    may need to add nginx to the container.=

## Community images as your base image

If you need to set the configurations at all (see above), you\'ll need
to create a new Dockerfile that uses the community-provided image as a
base. Your new Dockerfile should deal with custom configurations and
dependency installations.

-   Jupyter Lab (<https://hub.docker.com/r/cyversevice/jupyterlab-base>)
-   RStudio Verse (<https://hub.docker.com/r/cyversevice/rstudio-verse>)
-   Shiny Verse (<https://hub.docker.com/r/cyversevice/shiny-verse>)

See some examples of VICE apps that uses community images as base image
in the Dockerfile

-   MMTF
    (<https://github.com/sbl-sdsc/mmtf-genomics/blob/master/vice/Dockerfile>)
-   Rstudio-Bioconductor
    (<https://github.com/cyverse/docker-builds/blob/master/rstudio-bioconductor/Dockerfile>)
-   Patmatch
    (<https://github.com/fomightez/patmatch-binder/tree/master/vice>)

## Test your Docker image

Since the images are built based using Dockerfile, make sure you test
the Dockerfile before providing it to us. Dockerfile must have
Entrypoint. If you cannot provide us the Dockerfile, you can request
integration of the app by doing a tool request.

**Fix or improve this documentation:**

-   On Github:
-   Send feedback: [Tutorials\@CyVerse.org](Tutorials@CyVerse.org)
