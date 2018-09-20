|CyVerse logo|_

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**About**
---------

What is VICE?
=============
VICE stands for Visual Interactive Computing Environment. VICE allows users of the CyVerse `Discovery Environment <http://de.cyverse.org>`_ to launch web applications that have been packaged as Docker images. Once the application is launched, the users can access the launched VICE apps through a URL generated in the backend and served up through a public-facing reverse proxy. 

What is its big idea?
=====================
CyVerse Discovery environment hosts a number of GUI applications for researchers to perform their bioinformatic and other kinds of data analysis. Till today they could not run adhoc scripts, arbitrary tools or interactive analysis within DE. This is major stumbling block for data analysis becauase initial analyses of data often involve exploratory data analysis (EDA) using tools such as Jupyter notebooks and Rstudio. VICE will help both the new and experienced users do a thorugh exploratory data analysis as well as run adhoc scripts and arbitrary tools using Jupyter Notebooks and Rstudio and analayze and communicate your data story using Shiny

How is it different than other DE apps?
=======================================
The other apps available on DE, doesn't let you do exploratory analysis or interact with your data directly. You have to wait for the analysis to finish before you know the result or use the interactive tools on your computer. VICE let users interact with data and analysis in their favorite programming languages mainly through Notebooks, Rstudio and Shiny. Researchers can now explore their datasets interactively by easily changing parameters of selected analysis applications without having to download data from storage to an active workspace. VICE uses executable notebooks such as Jupyter, RShiny, and RStudio to allow researchers to iteratively manipulate your data files manually and process the outputs in the same place. VICE brings well-known, open source web applications, e.g., Jupyter Notebook, Rstudio and Rshiny, to the Discovery Environment so you can tweak your workflow parameters to best match your data analysis needs and perform a variety of new tasks like visualizations, statistical analyses, simulations, etc. – all without leaving the Discovery Environment.

Conclusion
==========
Installing Jupyter notebook, Rstudio and Rshiny software on your computer has restriction in that it will only allow certain types of tasks to perform (mainly because of software depedencies and memory requriements). VICE combines the power of DE computation with the interactivity of the modern web.

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