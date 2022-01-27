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

\_ [Learning Center Home](http://learning.cyverse.org/)

# **Building DE tools and apps**

Once you build your Docker image (following the guidelines), the next
step is building the Tool.

For this you\'ll need a Docker image name, any port numbers `PORT`, User
ID `UID`, working directory `WORKDIR`, and `ENTRYPOINT`.

## Docker images

The Docker image of your tool is mandatory and it should be available on
public registries such as [Dockerhub](https://hub.docker.com) or
[quay.io](http://quay.io). Alternatively you can provide us the
Dockerfile and we will build the Docker image for you. If there is no
Dockerfile for the tool that you are interested in, then tell us what
tool you are interesting in making us as VICE app.

## Add Tool in DE

The final step in building the VICE tool is to fill up the \"Add Tool\"
form in DE.

Brifely here are the following steps.

-   Log in CyVerse [Discovery Environment](https://de.cyverse.org/de/)
-   Click on the Apps window and click Manage Tools button on the far
    right hand side of the window
-   Click on Tools button and then finally Add Tools button

You\'ll see a Add Tool form like this

-   `Tool name` is the name of the tool. This will appear in the DE\'s
    tool listing dialog. This is mandatory field. Eg.
    \"jupyterlab-circos\"
-   `description` is a brief description of the tool. This will appear
    in the DE\'s tool listing dialog. Eg. \"Circos is a software package
    for visualizing data and information that was created by Martin
    Krzywinski\"
-   `version` is the version of the tool. This will appear in the DE\'s
    tool listing dialog. This is mandatory field. Eg. \"1.0\"
-   `Image name` is the name of the image specifier minus the image tag.
    The image must exist on Dockerhub or quay.io. This is mandatory
    field. E.g \"fomightez/circos-vice\"
-   `Tag` is the image tag. If you don\'t specify the tag, the DE will
    look for the \"latest\" tag which is the default tag.
-   `Docker Hub URL` is the url of the image on the Dockerhub. E.g
    <https://hub.docker.com/r/fomightez/circos-vice>
-   `Type` is the type of Tool. For VICE apps, chose \"interactive\".
-   `OSG Image Path` is path of the image on the OSG. You can skip this
    for interactive tools.
-   `Entrypoint` is the Entrypoint for your tool. Entrypoint should be
    present in the Docker image and if not, you should specify it here.
-   `Working Directory` this is the working directory of the tool and
    must be filled in with the value you gathered above. E.g
    /home/jovyan/vice
-   `UID` is a number and must be filled in with the value you gathered
    from above. E.g 1000
-   `Max CPU Cores` is the number of cores for your tool. Eg. 16
-   `Memory Limit` is the memory for your tool. Eg. 64 GB
-   `Min Disk Space` is the minimum disk space. Eg. 200 GB
-   `Container Ports` must be a list of maps with only a single entry.
    The key in that entry must be container_port and should be filled in
    with the number value you gathered above.

::: warning
::: title
Warning
:::

It is strongly recommended you do not set the [bind to host]{.title-ref}
as [true]{.title-ref} for your added ports when creating a new App\*\*
:::

## Creating VICE app for your tool

To create a new app, follow the instructions in
[here](https://wiki.cyverse.org/wiki/display/DEmanual/Designing+the+Interface)

::: important
::: title
Important
:::

For VICE apps, be sure to check the box \"Do not pass this argument to
the command line\" for each option you add (for VICE, this is usually
just input files and folders.
:::

------------------------------------------------------------------------

**Fix or improve this documentation:**

-   On Github:
-   Send feedback: [Tutorials\@CyVerse.org](Tutorials@CyVerse.org)
