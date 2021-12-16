.. include:: ../cyverse_rst_defined_substitutions.txt
.. include:: ../custom_urls.txt

|Home_Icon|_
`Learning Center Home <http://learning.cyverse.org/>`_

**Cloud Shell**
---------------

1. Log into Discovery Environment
=================================

Log into `CyVerse DE <https://de.cyverse.org/de/>`_ with your CyVerse credentials. 

If you have not yet created an account, go to the `User Portal <https://user.cyverse.org>`_ and do so.

The ``Cloud Shell`` App is already pinned to the Discovery Environment Tool Bar (left side of screen): 

.. rst-class:: fa fa-terminal 
   
      Alternately, use the search to specify 'Apps' then type keyword `Shell` or `Cloud Shell`


.. rst-class:: fa fa-bars 
   
     You can see ``Cloud Shell`` listed when you expand the three bars Menu icon.


|cloudshell-0|

2. Launch analysis
==================

|cloudshell-1|

Instant Launches start the App immediately without the opportunity to add any input data or increase the VM size.

Clicking on the **Apps** will show the Cloud Shell in "Featured Apps".

By default the Analysis Name is the name of the App plus the date and time.

The output folder will use this same name and be written to the ``/iplant/home/username/analyses/`` directory **AFTER** the interactive analysis is completed. 

.. Note::

	Deleting a running Analysis will stop it from writing outputs to your data store ``analyses/`` directory.

.. Note::

	The input files and/or folders can be selected under the 'Parameters' tab.

.. Tip::

	If you have an existing set of files or directories, you can import these into the app using input files and/or folder in the Parameters .


3. Navigate to the App
======================

After you have started a VICE App, your browser will open a new tab and automatically be taken to the loading screen.

|cloudshell-2|

Once the app is ready, it will transition to the user interface (in this example, a Linux terminal)

There should be a "message of the day", some information about the machine you're using, and your CyVerse username for when you initiate an iCommands connection.

.. Important::
	Normal wait times for a featured VICE App are less than 2 minutes. If you're experiencing a significantly longer wait, consider terminating  the app and re-starting. 

If you have closed the window, and are returning to the Discovery Environment in a new login session, you can find the running App in the "Analyses" section

.. rst-class:: fa fa-external-link-alt

|cloudshell-3|

4. Activate a ``conda`` environment
===================================

The Cloud Shell comes with multiple languages and package managers pre-installed. These include ``go``, ``python``, and ``rust``.

Package managers include ``conda`` and ``cargo`` in addition to linux `apt` and `apt-get`.

Your identity inside the container is ``user`` and you have limited ``sudo`` privileges to install new packages into the container. 

These changes are not saved after the analyses ends, or when you start a new Cloud Shell Analyses later.

.. Tip::

  The cloud shell is running a terminal multiplexer called `tmux` which keeps your session active even after you've closed your browser tab. 
  
  ``tmux`` keyboard commands should function normally.  

To activate conda:

```
conda init
```

and then

```
conda activate base
```

If you recieve a message about refreshing your screen, you can ``exit`` the cloud shell by typing "exit" and then hitting the refresh button on your browser tab.


5. Adding data to your analysis
===============================

To connect to the CyVerse DataStore, you can initiate an iRODS iCommands ``iinit`` 

You should now be connected to your ``/iplant/home/username`` home directory. 

```
ils
```

or

```
ils /iplant/home/username/
```

To view the 'shared' directory try:

```
ils /iplant/home/shared
```

Download data into your Cloud Shell with `iCommands <https://docs.irods.org/master/icommands/user/>`_ by running ``iget``

```
iget -KPbvrf /iplant/home/shared/cyverse_training/
```

6. Complete and Save Outputs
============================

After finishing your analyses, you can save the outputs back to Data Store.

You can either use ``iput`` to copy your new files back to your user space, or if you've left your new work in the ``/home/user/work`` folder, it will be copied back to your ``/iplant/home/username/Analyses/`` directory.

You can find the outputs you generated (if any) using the same steps as before, but this time select the 'Go To Output Folder'.

7. Terminate your app
=====================

The Discovery Environment is a shared system. In fairness to the community, we ask uses to "Terminate" any apps they have started when they are no longer running analyses.

In the Analyses window, select the app with the checkbox, then select "More Actions" and "Terminate" to shut the app down. 

Any new data in the `/home/user/work` directory will begin copying back to your folder at this time. 

Any input data which you added when the app started using the conventional launch feature will not be copied.

.. Warning::

	VICE apps only run for a pre-determined amount of time, typically between 4 and 48 hours. If you have opted for email notifications from DE, then you'll get a notification 1 day before and 1 hour before the app gets terminated. If you want to extend the time, you need to login to https://de.cyverse.org, find your analysis and then click the hour glass which automatically extends the app run time.


**Fix or improve this documentation**

- On Github: |Github Repo Link|
- Send feedback: `Tutorials@CyVerse.org <Tutorials@CyVerse.org>`_
