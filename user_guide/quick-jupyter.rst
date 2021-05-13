.. include:: ../cyverse_rst_defined_substitutions.txt
.. include:: ../custom_urls.txt

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Jupyter Lab**
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
	Terminating an App will stop it from writing outputs to your data store ``analyses/`` directory.

|jupyter2-2|

.. Note::
	The input files and/or folders can be selected under the 'Parameters' tab.

.. Tip::
	If you have an existing Jupyter workbook, you can import it into the app using input files and/or folder in the Parameters .


3. Navigate to JupyterLab url
==============================

After you start the VICE App, you will be taken to a loading screen.

|app-waiting|

Once the app is ready, it will transition to the Jupyter Lab interface

.. Important::
	Normal wait times for a featured VICE App are less than 2 minutes. If you're experiencing a significantly longer wait, consider terminating  the app and re-starting. 
	
**The Jupyter Lab Interface:** Jupyter Lab provides flexible building blocks for interactive, exploratory computing. While Jupyter Lab has many features found in traditional integrated development environments (IDEs), it remains focused on interactive, exploratory computing. The Jupyter Lab interface consists of a main work area containing tabs of documents and activities, a collapsible left sidebar, and a menu bar. The left sidebar contains a file browser, the list of running kernels and terminals, the command palette, the notebook cell tools inspector, and the tabs list.

More information about the Jupyter Lab can be found `here <https://jupyterlab.readthedocs.io/en/stable/user/interface.html>`_.

4. Create Jupyter notebook
==========================

Jupyter notebooks are documents that combine live runnable code with narrative text (Markdown), equations (LaTeX), images, interactive visualizations and other rich output. Jupyter notebooks (.ipynb files) are fully supported in JupyterLab.

If you want to create a notebook, you can do so by clicking the ``+`` button in the file browser and then selecting a kernel in the new Launcher tab. Currently there are 3 different notebooks available - Python3, Julia and R. Click on `Python 3` under Notebook section in the JupyterLab Interface, which will open a new Jupyter Notebook. A new file is created with a default name. Rename a file by right-clicking on its name in the file browser and selecting “Rename” from the context menu.

To know more about notebooks in JupyterLab click `here <https://jupyterlab.readthedocs.io/en/stable/user/notebook.html>`_

.. Tip::

	To open the classic Notebook from Jupyter Lab, select “Launch Classic Notebook” from the Help Menu.

|jupyter2-5|

.. Note::

	There are plenty other cool stuff that you can do in Jupyter Lab such as using `consoles <https://jupyterlab.readthedocs.io/en/stable/user/code_console.html>`_, using `terminal <https://jupyterlab.readthedocs.io/en/stable/user/terminal.html>`_ and using `text editor <https://jupyterlab.readthedocs.io/en/stable/user/file_editor.html>`_.

5. Write your code
==================

Once you open a new notebook, you can start writing your code, put markdown text, generate plots, save plots etc.

|jupyter2-6|

6. Complete and Save Outputs
============================

After finishing your analysis, you can save outputs to data store by clicking the Analysis window, then select the VICE analysis that you are running and select `Complete and Save Outputs` under the "Analyses" button.

|jupyter2-7|

After you had done this, you can find the outputs that you generated (if any) using the same steps as before, but this time selecting 'Go To Output Folder'.

.. Warning::
	Currently, VICE can run for 48 hrs beyond which the apps will be terminated. If you have opted for email notifications from DE, then you'll get a notification 1 day before and 1 hour before the app gets terminated. If you want to extend the time, you need to login to http://cyverse.run, find your analysis and then click the hour glass which automatically extends the app run time to 3 more days.

**Fix or improve this documentation**

- On Github: `Repo link <https://github.com/CyVerse-learning-materials/sciapps_guide>`_
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_

7. Jupyter-lab with SQL
=======================

Now you can run SQL queries inside a notebook. Here is a quick launch 

.. raw:: html

	<a href="https://de.cyverse.org/de/?type=quick-launch&quick-launch-id=266f8f99-63c6-4bfa-977b-aab8ebd087b3&app-id=d61d9a26-e921-11e9-8fe0-008cfa5ae621" target="_blank"><img src="https://de.cyverse.org/Powered-By-CyVerse-blue.svg"></a>
