|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Applications**
----------------

Currently, VICE apps are categorized broadly into three different spaces: 

1. Integrated Development Environments (Jupyter Lab and RStudio) 
2. Interactive apps (Shiny) 
3. Virtual Desktops (VNC, Apache Guacamole) 

.. Note:: In the future, there will be support for many different types of VICE apps.

Each of these spaces serves a different data science purpose. For example..

* If you are interested in writing Python, Julia, Spark, C++ based data analysis or visualization, Jupyter is most appropriate.

* If you are interested in creating analyses written in R, RStudio would be more appropriate. 

* If you have a pre-built analysis such as Shiny built in R, Shiny is used.

* If you want to work in other Linux-based software, you can launch a virtual deskop using VNC or Apache Guacamole, and work with your tools there.

1. What is JupyterLab?
======================

The `JupyterLab <https://jupyterlab.readthedocs.io/en/stable/index.html>`_ is an interactive development environment for working with notebooks, code and data. Most importantly, JupyterLab has full support for Jupyter Notebooks. Additionally, JupyterLab enables you to use text editors, terminals, data file viewers, and other custom components side-by-side with notebooks in a tabbed work area. JupyterLab provides a high level of integration between notebooks, documents, and activities:

- Drag-and-drop to reorder notebook cells and copy them between notebooks.
- Run code blocks interactively from text files (.py, .R, .md, .tex, etc.).
- Link a code console to a notebook kernel to explore code interactively without cluttering up the notebook with temporary scratch work.
- Edit popular file formats with live preview, such as Markdown, JSON, CSV, Vega, VegaLite, and more.

1.1 What is a Jupyter Notebook?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The `Jupyter Notebook <https://jupyter.readthedocs.io/en/latest/>`_ (formerly IPython Notebook) is Project Jupyter's flagship project for creating reproducible computational narratives. It enables users to create and share documents that combine live code with narrative text, mathematical equations, visualizations, interactive controls, and other rich output. It also provides building blocks for interactive computing with data: a file browser, terminals, and a text editor. Notebook documents (or “notebooks”) are documents produced by the Jupyter Notebook App, which contains both computer code (e.g., python, r, julia) and rich text elements (paragraph, equations, figures, comments, images, links, etc.). 

1.2 JupyterLab VICE 
~~~~~~~~~~~~~~~~~~~

The JupyterLab VICE app is integrated into the DE which includes Jupyter Notebook text editors, terminals, data file viewers, irods plugin and other custom components. Click here to do a quick launch of JupyterLab VICE app in the DE.

2. What is RStudio?
===================

`RStudio <https://www.rstudio.com/>`_ is a free and open source integrated development environment for R, a programming language for statistical computing and graphics. Some of its features include:

- Customizable workbench with all of the tools required to work with R in one place (console, source, plots, workspace, help, history, etc.).
- Syntax highlighting editor with code completion.
- Execute code directly from the source editor (line, selection, or file).
- Full support for authoring Sweave and TeX documents.
- Runs on all major platforms (Windows, Mac, and Linux) and can also be run as a server, enabling multiple users to access the RStudio IDE using a web browser.

2.1 Rstudio VICE 
~~~~~~~~~~~~~~~~

The Rstudio VICE app is integrated into the DE. Click here to do a quick launch of Rstudio VICE app in the DE.

3. What is Shiny?
=================

`Shiny <https://shiny.rstudio.com/>`_ is an open source R package that provides an elegant and powerful web framework for building web applications using R. Shiny helps you turn your analyses into interactive web applications without requiring HTML, CSS, or JavaScript knowledge. Some of its features include:

- Build useful web applications with only a few lines of code—no JavaScript required.
- Shiny applications are automatically “live” in the same way that spreadsheets are live. Outputs change instantly as users modify inputs, without requiring you to reload your browser.
- Shiny user interfaces can be built entirely using R, or can be written directly in HTML, CSS, and JavaScript for more flexibility.
- Works in any R environment (Console R, Rgui for Windows or Mac, ESS, StatET, RStudio, etc.).
- Attractive default UI theme based on Twitter Bootstrap.
- A highly customizable slider widget with built-in support for animation.
- Pre-built output widgets for displaying plots, tables, and printed output of R objects.
- Fast bidirectional communication between the web browser and R using the websockets package.
- Uses a reactive programming model that eliminates messy event handling code, so you can focus on the code that really matters.
- Develop and redistribute your own Shiny widgets that other developers can easily drop into their own applications (coming soon!).

3.1 Shiny VICE 
~~~~~~~~~~~~~~~~

The Shiny VICE app is integrated into the DE. Click here to do a quick launch of Shiny VICE app in the DE.

4. What is Ubuntu Desktop?
=========================

The Ubuntu Desktop has a full Guacamole installation and Ubuntu XFCE desktop. This allows users to have a simple all-in-one desktop through their web browser. Users can run any interactive or visualization tool that can run on the most recent linux distros. Solutions to support the inevitable array of linux applications that user will want. Potential options include:

- Separate image per application
- Network fs (e.g. NFS, Ceph, etc) containing all applications
- Per-application network fs
- On-demand installation of application via script/ansible

4.1 Ubuntu Desktop VICE 
~~~~~~~~~~~~~~~~~~~~~~~

Ubuntu Desktop VICE app is integrated into the DE. Click here to do a quick launch of Linux Desktop VICE app in the DE.

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
