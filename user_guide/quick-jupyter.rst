.. include:: ../cyverse_rst_defined_substitutions.txt
.. include:: ../custom_urls.txt

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**JupyterLab**
---------------

1. Search for JupyterLab
========================

Log into `CyVerse DE <https://de.cyverse.org/de/>`_

Use the search bar to specify 'Apps' or type keywords `Jupyter` or `JupyterLab Datascience`

|jupyter2-0|

2. Launch analysis
==================

|jupyter2-1|

Instant Launches will start the App immediately.

Clicking on **Apps** find the JupyterLab you're interested in and then click on the blue run button.

By default the Analysis Name is the name of the App, and the Output Folder is where any work done in the container will be written to ``/iplant/home/username/analyses/analysis_name/`` directory **AFTER** the interactive analysis is completed. 

.. Note::
	Deleting a running Analysis will stop it from writing outputs to your data store ``analyses/`` directory.

|jupyter2-2|

.. Note::
	The input files and/or folders can be selected under the 'Parameters' tab.

.. Tip::
	If you have an existing Jupyter workbook, you can import it into the app using input files and/or folder in the Parameters .


3. Navigate to JupyterLab url
==============================

After you start the VICE App, you will be taken to a loading screen.

|app-loading|

Once the app is ready, it will transition to the Jupyter Lab interface

.. Important::
	Normal wait times for a featured VICE App are less than 2 minutes. If you're experiencing a significantly longer wait, consider terminating  the app and re-starting. 
	
|jupyter2-3|	
	
**The Jupyter Lab Interface:** Jupyter Lab provides flexible building blocks for interactive, exploratory computing. While Jupyter Lab has many features found in traditional integrated development environments (IDEs), it remains focused on interactive, exploratory computing. The Jupyter Lab interface consists of a main work area containing tabs of documents and activities, a collapsible left sidebar, and a menu bar. The left sidebar contains a file browser, the list of running kernels and terminals, the command palette, the notebook cell tools inspector, and the tabs list.

More information about the Jupyter Lab can be found `here <https://jupyterlab.readthedocs.io/en/stable/user/interface.html>`_.

4. Create Jupyter notebook
==========================

Jupyter notebooks (``.ipynb``) combine code with narrative text (Markdown), equations (LaTeX), images and interactive visualizations. 

To create a notebook, click the ``+`` button, this opens the new Launcher tab. 

The JupyterLab Datascience containers have three pre-installed kernels: Python3, Julia, and R. 

`Jupyter notebooks <https://jupyterlab.readthedocs.io/en/stable/user/notebook.html>`_

.. Tip::

	To open the classic Notebook view from JupyterLab, select “Launch Classic Notebook” from the Help Menu.

To connect to the CyVerse DataStore, click the little CyVerse orb in the left side of the Lab. 

|jupyter2-4|

You should now be connected to your ``/iplant/home/username`` home directory. Navigate to the 'shared' directory by clicking one order higher on the ``/home`` directory, you should now see your username and the ``/shared`` path.

Navigate to ``/shared/cyverse_training/platform_guides/discovery_environment/jupyterlab`` and open the `Penguins <https://github.com/JohnMount/Penguins>`_ sample dataset 

|jupyter2-5|

.. Note::

	There are plenty other cool stuff that you can do in Jupyter Lab such as using `consoles <https://jupyterlab.readthedocs.io/en/stable/user/code_console.html>`_, using `terminal <https://jupyterlab.readthedocs.io/en/stable/user/terminal.html>`_ and using `text editor <https://jupyterlab.readthedocs.io/en/stable/user/file_editor.html>`_.

5. Write your own code
======================

Once you open a new notebook, you can start writing your code, put markdown text, generate plots, save plots etc.

|jupyter2-6|

6. Complete and Save Outputs
============================

|jupyter2-7|

After finishing your analysis, you can save outputs to Data Store by clicking the Analysis window, then select the VICE analysis that you are running and select `Terminate` under the "Analyses" button.

|jupyter2-8|

After you had done this, you can find the outputs that you generated (if any) using the same steps as before, but this time selecting 'Go To Output Folder'.

.. Warning::
	VICE apps only run for a pre-determined amount of time, typically between 4 and 48 hours. If you have opted for email notifications from DE, then you'll get a notification 1 day before and 1 hour before the app gets terminated. If you want to extend the time, you need to login to https://de.cyverse.org, find your analysis and then click the hour glass which automatically extends the app run time.

**Fix or improve this documentation**

- On Github: `Repo link <https://github.com/CyVerse-learning-materials/sciapps_guide>`_
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_

