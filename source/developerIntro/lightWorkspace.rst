.. _light_workspace_setup:

Light Workspace Setup
=====================

Every day, bit by bit, Terasology is growing. From the smallest of jobs like adding readmes to slightly larger jobs like adding code, people from all around the world wish to contribute to the project. However, for many the process is far more complex than required. For instance, one doesn't need to clone a complete Git-linked repository to one's system just to edit a readme. This guide will guide you through setting up a light environment so that you can do these relatively small tasks without much tedium.

Using the GitHub Web Interface
------------------------------

GitHub's web interface is great for tasks involving small edits to code or edits to text files (like readmes) or wikis. It allows the user to edit and commit right from the browser window.

Creating a Fork
~~~~~~~~~~~~~~~

To create a fork of Terasology, visit `Terasology's GitHub repository <https://github.com/MovingBlocks/Terasology>`_ and click the "Fork" button near the top right corner of the screen. This will create a fork of the repository in your GitHub account.

.. image:: img/Fork.png

Creating and Deleting Branches
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since you are going to be making changes, it might be a good idea to create a branch before. You can create a branch by clicking on the repository's branch selector and typing in the name of the branch. If the branch doesn't exist, GitHub will offer to create it for you.

You can go to the **Branches** page of your repository by clicking on the number of branches displayed on the home page of the repository. This will take you to an overview of all your branches. From here, you can delete branches by clicking the little red trash can icons.

.. image:: img/Branch1.png

.. image:: img/Branch2.png

Editing
~~~~~~~

Creating a File
###############

1. Navigate to the main page of your repository.
2. Browse to the folder where you want to create a file.
3. Click the **Create new file** button above the file list.
4. Type the name and extension of the file you want to create in the name field. You may also create subdirectories here by using the ``/`` directory separator.
5. Add contents to the file in the **Edit new file** tab. You may preview your file while editing using the **Preview** tab.
6. At the bottom of the page, type a commit message, choose the branch you want to commit to, and then click the **Commit New File** button.

.. image:: img/Create.png

Editing, Renaming or Moving Files
#################################

1. Browse to the file you want to make changes to.
2. In the upper right hand corner, click the little pencil icon to open the editor.
3. You can change the name of the file at the top of the page. You can also move the file by using the ``/`` separator to make/access subdirectories (use ``..`` to go to the parent directory).
4. Make the changes you want to make in the **Edit** tab. You may preview the changes using the **Preview** tab.
5. Scroll to the bottom of the page, type a commit message, choose the branch you want to commit to, and click the **Commit Changes** button.

.. image:: img/Edit1.png

.. image:: img/Edit2.png

Deleting files
##############

1. Browse to the file you want to delete.
2. At the top of the file, click the little trashcan icon.
3. Scroll to the bottom of the page, type a commit message, choose a branch, and commit.

.. image:: img/Delete.png

Opening a Pull Request
~~~~~~~~~~~~~~~~~~~~~~

1. Navigate to the home page of your repository.
2. Press the **Pull Request** button at the top of the page.
3. Give a title and description to the pull request.
4. Press the **Create a pull request** button.

.. image:: img/PR.png

Using the GitHub Desktop Client
-------------------------------

For many changes, especially more elaborate ones, you may prefer downloading the repository on your system, making changes, testing them and then committing them. This can be achieved by various means, the most popular of which is git's command-line interface. However, this may be daunting for many users, especially beginners. This is where GitHub's desktop client comes in. The GitHub desktop client is an easy way to clone and edit repositories on your system. Here are a few tips to help you get started.

Note that to access your environment via the desktop client, you first need to fork the `Terasology repository <https://github.com/MovingBlocks/Terasology>`_ using the process mentioned before in this document.

Setting Up the Client
~~~~~~~~~~~~~~~~~~~~~

The GitHub desktop client can be downloaded from `the GitHub desktop home page <https://desktop.github.com>`_. The client is available for MacOS and for Windows. Sadly, there is no Linux client yet.
On launching the client for the first time, you will be asked to enter your GitHub account username and password, after which you will be led through a short tutorial on the basics of using the client.

Cloning Your Repository
~~~~~~~~~~~~~~~~~~~~~~~

1. Launch the client.
2. Press the "+" dropdown in the top left corner.
3. Go to the **Clone** tab.
4. Select the name of the forked repository from the list of all your repositories.

.. image:: img/Clone.png

Creating a Branch
~~~~~~~~~~~~~~~~~

1. Click on the create branch icon.
2. Type in a name and select the original branch from which to branch off.
3. Press the **Create Branch** button.

.. image:: img/Branch.png

Making Changes and Committing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sadly, the desktop client doesn't support making changes or browsing the repo. You will need to browse the repo and make changes using the operating system's file explorer and appropriate editing tools on your system. To commit, simply select the repository in the tray on the left hand side, select which files to commit, type a commit message and description and press the **Commit** button. You can push committed changes by pressing ``Control+P`` (``Cmd+P`` on Mac) or by using the **Publish** button at the top right corner of the screen. You can also use the toolbar item at Repository -> Push.

Opening Pull Requests
~~~~~~~~~~~~~~~~~~~~~

1. Select your repository in the tray at the left.
2. Press the **Pull Request** button in the top right corner.
3. Provide a title and description.
4. Press **Send Pull Request**.

.. image:: img/PR_desktop.png

-- written by Mandar Juvekar
