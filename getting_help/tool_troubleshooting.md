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

# **Tool Troubleshooting**

## 1. Get the port

You\'ll need to figure out the port that the tool uses to present its
web interface. This is mandatory and you can integrate a tool without
knowing the port it runs on. If you don\'t know, you can find the ports
that a container image exposes with this command

``` bash
$ docker inspect <image-name>:<image-tag> -f '{{range $port, $val := .ContainerConfig.ExposedPorts}}{{$port}} {{end}}'
```

> Replace [\<image-name>:\<image-tag>]{.title-ref} with the your Docker
> image

It\'s possible that multiple or no ports are listed. If that\'s the case
you\'ll need to refer to the documentation for the tool to figure out
the port it uses. Make a note of the port, you\'ll need it later when
integrating the tool in DE. Here are the tools and their ports for
common tools such as Jupyter notebook, Rstudio and Shiny. If you are
developing any applications based on these tools, you can use these
ports while integrating the tool in DE.

  ------------ ---------
  Type         Port

  Jupyter      8888

  Rstudio      80

  Shiny        3838
  ------------ ---------

## 2. Get the UID of the tool\'s user

You\'ll need to figure out the `UID` of the of the user the app runs as.
Many tools will start up as root and then use another user for the
actual process, so it might take a little investigation to figure this
out. To start this figure out the user that the container is configured
to start up using:

``` bash
$ docker inspect <image-name>:<image-tag> -f '{{.ContainerConfig.User}}'
```

If you\'re lucky that will contain the numerical UID of the user. In
that case you can make a note of the UID and move on. Otherwise you have
more work to do. The User field can also be empty or set to the
username. If its empty, then the user is `root`. If it\'s a username
then you\'ll need to get the `UID` from inside the container.

To get the `UID` for a username run this:

``` bash
$ docker run --rm -it --entrypoint "id" <image-name>:<image-tag> -u <username>
```

> Replace [\<image-name>:\<image-tag>]{.title-ref} with the your Docker
> image

If the User field is empty or `root`, you need to be sure that the
process inside the container actually runs as `root`. There are a few
ways to check this:

-   Fire up the container, exec into it, and do a `ps aux` to see the
    user the process is running as.

``` bash
$ docker run -d --name app <image-name>:<image-tag>

$ docker exec -it app ps aux
```

-   Print out the contents of `/etc/passwd` and check for hints:

``` bash
docker run --rm -it --entrypoint "cat" <image-name>:<image-tag> /etc/passwd
```

-   Alternatively check the documentation for the tool.

::: note
::: title
Note
:::

The UID of the tool can be empty but setting the UID will make sure that
the user can write to the input files in the container.
:::

Make a note of the UID, you\'ll need it later when putting together the
JSON for the tool and app.

## 3. Get the working directory

You\'ll need the working directory for the process in the tool
container, which may not correspond to the default working directory for
the container.

To get the default working directory for the container run this:

``` bash
$ docker inspect <image-name>:<image-tag> -f '{{.ContainerConfig.WorkingDir}}'
```

-   If that prints out an empty string, then the default working
    directory is `/.`
-   If the container fires up as root but the tool runs as another user,
    then the working directory may need to be that user\'s home
    directory.
-   If the container changes to another directory after it starts up,
    then the working directory may need to be that directory.
-   If all else fails, check the documentation and/or try out the
    container locally to figure out what it does.

> Keep in mind that the working directory is where the input files will
> be made available. Similar to UID, working directory is not mandatory
> but given jupyter lab\'s default behavior of showing things in
> subdirectories of the place it\'s started. So if you\'re loading
> notebooks and data from the Datastore, you want the working directory
> (where those files are loaded into the container) to be in the right
> spot

Make a note of the working directory, you\'ll need it later when putting
together the JSON for the tool and app.
