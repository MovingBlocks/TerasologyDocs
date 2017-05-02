.. _contributing:

Contributing
============

After going through the :ref:`first steps <getting_started>`, one can start with contributing to the actual project or a module.

There are two ways to submit changes back to GitHub,
either gaining write ("push") access to any of the root repositories or by forking personal copies of any of them.

The following examples below are fairly light and expect some minimal knowledge of git.
You may consider to use a native client like `GitHub Desktop <https://desktop.github.com/>`_ if available to you.
There are also plenty of good git tutorials on the web, http://learngitbranching.js.org/ is only one example to start with.

Creating a Fork
---------------
To get your own personal copy of a repo on GitHub you simply click the "Fork" button at the main page of any repo.
You'll have full rights on the resulting fork.

You can see how a root repo (in this case MovingBlocks/Terasology) and its forks relate
by checking the `network graph <https://github.com/MovingBlocks/Terasology/network>`_.
Each dot is a unique commit containing a change, each label is a branch,
and each section beyond MovingBlocks is somebody's personal fork of Terasology's main project repo that contains unique changes.
If you made a commit in your fork of the Terasology repo it would show up as its own dot in your username's section.

More information about the fork concept is available at https://help.github.com/articles/fork-a-repo/.

Updating a Fork
---------------
After you made a fork, you need to create a second remote reference in your local git root. There are better guides to git elsewhere but in short:

- If you cloned `MovingBlocks/Terasology <https://github.com/MovingBlocks/Terasology>`_ then that will be your remote named :code:`origin` but you will not have push rights to it.
  Instead, you have to push your changes to your fork and create a pull request from there, as described in the next section.
- If you cloned your fork, then that will be your :code:`origin` remote and you can add a second remote to `MovingBlocks/Terasology <https://github.com/MovingBlocks/Terasology>`_.
  You could name it :code:`movingblocks` or :code:`upstream` and use it to pull updates when changes are made.

Example:

In the following diagram, our mascot Gooey (GitHub username `GooeyHub <https://github.com/GooeyHub>`_) cloned `MovingBlocks/Terasology <https://github.com/MovingBlocks/Terasology>`_ first.
After that, Gooey added a remote named :code:`gooey` pointing to the fork repository by using :code:`git remote add gooey https://github.com/GooeyHub/Terasology`.

.. image:: img/forks.png

With two remotes defined, you can now pull and push code between your local workspace and GitHub. A regular workflow for the previous example could go like:

- Write some code.
- Make a local commit in your :code:`develop` branch or create a separate feature branch for your changes.
- Push your local changes to your fork: :code:`git push gooey develop`.
- Create a PR (see the next section).
- Wait for it to be accepted, optionally submit more changes (keep pushing commits to the same branch on your fork, the PR updates by itself).
- After the PR is merged, update your local workspace with :code:`git pull origin develop`.

.. _create_pr:

Creating a Pull Request
-----------------------

When you have suitable changes to be submitted to somebody else's repo on GitHub from your fork you can issue a Pull Request ("PR") to get their attention and review for your changes.

At your repo page, for instance https://github.com/GooeyHub/Terasology, you should see a summary comparing your selected branch to the matching branch in the repo you forked from, listing outstanding differences if any.

Simply click the "Pull Request" button to get started. Make sure your target (may be called "base fork") and source (may be called "head fork" - your fork) are correct and the changes are what you expect.

In your description please describe the changes you've made and how to test them, along with any particular review notes / justification for why you made the change, if needed.
Submit the PR then please wait for project staff to review your request - could take a little while :-)

.. note::
   While normally you would PR a change from one repo (like a fork) to another (like the root repo),
   nothing prevents you from using a PR inside a single repo to go from one branch to another.
   Some stay organized and review their code that way.

Direct Write Access
-------------------
While you can fork module repos we hand out write access to modules pretty easily.
So long as you've made a good impression, proven yourself able to make changes with Git,
and have an interest in working on a module not actively being worked by somebody else, you're in!

Multiple people can work directly on a single module repo if they coordinate well,
but this is where it becomes useful to work via Pull Requests.

To get access, ask in our `forum <http://forum.terasology.org/forum>`_ or :ref:`on IRC <using_irc>` - and be patient please :-)

Trusted long-term contributors can eventually get these rights to the main repos under the `MovingBlocks <https://github.com/MovingBlocks>`_ organization on GitHub.
