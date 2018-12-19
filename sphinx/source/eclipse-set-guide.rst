.. _intro:

What is EniwareNetwork?
=======================

EniwareNetwork is an open source software platform designed for building, deploying and running Industrial Internet applications. 

EniwareNetwork helps companies of all sizes to:

* Collecting and analyzing massive amounts of industrial data;
* Create a representation of assets;
* Improve faster: quickly build and deploy apps;
* Use an environment of manage services presented by Eniware Open Source.

EniwareNetwork contains a cloud services that run in a cloud structure managed by you, and can get a complete insight into your assets, using the services and infrastructure built. This allows better optimization of part of the system, also of the whole structure.

EniwareNetwork provides documentation to build a cloud that meets your data collection and processing needs, while improving the security, support, management, and control of output data.


.. _eclipse-setup:

Eclipse Setup Guide
===================

This guide explains how to setup a development environment for contributing to or modifying EniwareNetwork code using the popular Eclipse IDE. Although Eclipse is not actually required to work with EniwareNetwork code, it is a very good option and the remainder of this guide will describe setting up Eclipse for viewing and running the code for development purposes.

The EniwareNetwork projects consists of many small OSGi bundle projects that, when combined and run in an OSGi container, form a complete application. Each OSGi bundle comes configured as an Eclipse IDE plug-in project (Eclipse refers to OSGi bundles as "plug-ins" and its OSGi development tools are collectively known as the Eclipse Plugin Development Environment or just PDE.



.. _eclipse-download:

1. Eclipse Setup
^^^^^^^^^^^^^^^^^

In our case, we use Eclipse Oxygen which can be download from here: `Eclipse Oxygen 3a Packages <http://www.eclipse.org/downloads/packages/release/oxygen/3a/>`_. The `Eclipse IDE for Java Developers <http://www.eclipse.org/downloads/packages/release/oxygen/3a/eclipse-ide-java-developers>`_ edition is usually the best option.

Most likely, you will want to start with a new workspace for EniWARE Network development. When you launch Eclipse it might ask you for a workspace location, at which time you can point it at a new directory, or once Eclipse is running, you can choose **File > Switch Workspace > Other...** to create a new one.



.. _eclipse-git:

2. Eclipse Git support (older versions of Eclipse only)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Older versions of Eclipse (before Eclipse Mars) did not come with Git support by default. If you are using an older version, once you have Eclipse installed and running you will need to install support for Git, via the **EGit** plug-in. Navigate to **Help > Eclipse Marketplace** and search for *egit*. Install the **EGit - Git Team Provider** plug-in.

.. _eclipse-egit:

.. figure:: /images/0-eclipse-egit-install.png
   :alt: EGit - Git Team Provider



.. _eclipse-osgi:

3. Eclipse OSGi enterprise support (optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Another optional, but useful set of plug-ins for EniwareNetwork development in Eclipse are from `Project Libra <https://www.eclipse.org/libra/>`_. Navigate to **Help > Install New Software...**, select the project release update site URL in the **Work with** menu (for example ``http://download.eclipse.org/releases/oxygen`` if you're using Eclipse Oxygen) and look under **Web, XML, Java EE and OSGi Enterprise Development** for these plug-ins:

* OSGi Bundle Facet
* OSGi Framework  Editor
* OSGi Framework Launchers

.. _eclipse-osgi-install:

.. figure:: /images/1-available-software.png
   :alt: OSGi enterprise support


   
.. _eclipse-eniware-repo:   

4. Clone EniwareNetwork Git Repositories
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^   

The EniwareNetwork platform is broken up into multiple Git repositories. You will need to clone a few of them to work on any EniwareNetwork application. You can clone a Git repository by going to open a GIT Perspective: **Window > Perspective > Open Perspective > Other > Git**. 
In the top right corner of Eclipse window you will see the icon of *GIT Perspective*.

After you open the *GIT Perspective* you need to clone the following `EniwareNetwork <https://github.com/eniware-org>`_ repositories from GitHub:

* `org.eniware.build <https://github.com/eniware-org/org.eniware.build>`_;
* `org.eniware.common <https://github.com/eniware-org/org.eniware.common>`_;
* `org.eniware.edge <https://github.com/eniware-org/org.eniware.edge>`_;
* `org.eniware.external <https://github.com/eniware-org/org.eniware.external>`_;
* `org.eniware.central <https://github.com/eniware-org/org.eniware.central>`_

.. _eniware-repo-install:

.. figure:: /images/2-org-eniawre-build.png
   :alt: EniwareNetwork repository

To clone the repository switch to GIT Perspective and click on **Clone a Git Repository and add the clone to this view** button: 

.. _eniware-repo-clone:

.. figure:: /images/3-new-eclipse.png
   :alt: Clone repository
 
Then fill in the desired repository URI:

.. _eniware-repo-uri:

.. figure:: /images/4-clone-git-repository.png
   :alt: Repository URI

 

Then click **Next** button to select the branch in **Branch Selection** screen. The master branch should be selected for you.
 

.. _eniware-repo-branch:

.. figure:: /images/5-branch-selection.png
   :alt: Branch selection
   

Click the **Next** button. In the next window, you have to choose the **Local Destination** (a directory to clone the repository into), and mark the **Import all existing Eclipse project after clone finishes** checkbox:

.. _eniware-local-destination:

.. figure:: /images/6-local-destination.png
   :alt: Local Destination 

Click the **Finish** button to check out the projects. 

Once the clone of repositories to your Eclipse is complete, you can switch to the Java Perspective and you will see the bundle projects. It should look similar to the following:
 
.. _eniware-packet-explorer:

.. figure:: /images/7-new-eclipse-projects.png
   :alt: Package Explorer 



.. _eclipse-target:   
   
5. Set up Eclipse Target Platform
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Next, we have to configure the Eclipse. This will happened in few steps:

1) In Eclipse open the **eniware-osgi-target** project and then the ``defs/org.eniware-gemini.target`` file.
2) Set up the target platform by click on the **Set as Active Target Platform** button on the **Target Definition** screen.

   .. _eniware-target-definition:
   
   .. figure:: /images/8-org.eniware-gemini.png
      :alt: Target Definition

This will create and activate the Eclipse target platform, and all Eclipse errors for all projects should go away. If any errors remain, select those projects and choose **Project > Clean...** to have Eclipse re-compile those projects again. Sometimes Eclipse incorrectly reports problems, and cleaning those projects will resolve the errors. You will find references to this situation on the web called *the Eclipse dance*.

.. note:: Click on the **Environment** tab at the bottom, then under the **Arguments** section select **VM**. Select this entire block of text and copy it, as you will need to paste this into the runtime configuration, discussed in the next section.




.. _eclipse-osgi-runtime:

6. Configure OSGi Runtime
^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order to run the EniwareNetwork platform within Eclipse, you must configure the OSGi runtime environment:

1) First, create the directory ``/eniware-osgi-target/config``. Then copy all the files from ``/eniware-osgi-target/example/config`` into that directory.
2) Go to **Run > Run** configuration. From Run configuration choose **OSGI Framework** and specify **EniwareNetwork** as the runtime name.

   .. _eniware-target-platform:
   
   .. figure:: /images/9-eniware-network.png
      :alt: Run configuration

3) Next, you must change some of the start levels for a handful of bundles, to ensure the platform can start up correctly. Modify the start levels of the bundles to the following:

  +-------------------------------------+-------------+
  | Plugin                              | Start Level |
  +=====================================+=============+
  | org.apache.felix.eventadmin         | 1           |
  +-------------------------------------+-------------+
  | org.apache.felix.fileinstall        | 2           |
  +-------------------------------------+-------------+
  | org.apache.servicemix.bundles.derby | 1           |
  +-------------------------------------+-------------+
  | org.eclipse.equinox.cm              | 1           |
  +-------------------------------------+-------------+
  | org.eclipse.gemini.web.extender     | 5           |
  +-------------------------------------+-------------+

	   
   .. _eniware-bundles:
   
   .. figure:: /images/10-bundles.png
      :alt: Bundles

4) Next, click on the **Arguments** tab and change the **Working directory** to **Other** and specify ``${workspace_loc:eniware-osgi-target}`` as the path. In the **VM arguments** section, paste in the arguments you copied from the target platform configuration in the previous section, which should look something like:

.. code::
   
   -Dsn.home=${workspace_loc:eniware-osgi-target}
   -Dderby.system.home=${workspace_loc:eniware-osgi-target}/var/db
   -Djava.util.logging.config.file=config/jre-logging.properties
   -Dosgi.java.profile=file:config/java6-server.profile
   -Dorg.apache.felix.eventadmin.Timeout=120000
   -Dfelix.fileinstall.dir=configurations/services
   -Dfelix.fileinstall.filter=.*\.cfg
   -Dfelix.fileinstall.noInitialDelay=true
   -Declipse.ignoreApp=true
   -Dosgi.noShutdown=true
   -Dxml.catalog.files=${workspace_loc:eniware-osgi-lib}/xml-catalog/catalog.xml

5) Next, click on the **Settings** tab and change the JRE to use the **Execution environment** value of **JavaSE-1.6**.

You should click **Apply** and then the **Close** button to dismiss the runtime configuration dialog.

With this final step, the Eclipse is ready to be used as a development environment for EniwareNetwork platform.