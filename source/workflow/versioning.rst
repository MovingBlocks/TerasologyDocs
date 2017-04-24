.. _versions:

Versioning
==========

Terasology follows the `Semantic Versioning <http://semver.org/>`_ for all versioning used across the projects.

In short this means using a version number like :code:`x.y.z` with three scopes:

- :code:`x` is the "major" version. This is incremented when a change is made that is not backwards compatible (the **existing API changed**).
- :code:`y` is the "minor" version. this is incremented when a change adds something to the API but does not break it (the **API is extended**).
- :code:`z` is the "patch" version. This simply means bugs were fixed but no functionality was otherwise changed.

This helps to make dependencies more predictable. If you make a new backwards-incompatible version of a popular library, 
you release it with a new major version number so old things that depend on it do not break, 
assuming they had asked for the specific version they needed.

Module versions are handled in the :ref:`module_txt`, including version ranges for dependencies.

Snapshots
---------

When something new is created, it starts a placeholder :code:`0.0.1-SNAPSHOT` version.
The :code:`-SNAPSHOT` suffix means any build will be of version :code:`0.0.1` yet not cound as release - just an unstable preview.
Snapshots can be built over and over without changing the version.

It is common to stay in this range until a feature is ready and worth a minor or patch increase.
There are two goals to pick from:

1. Staying in the :code:`0.y.z` range. This means the project is not considered as ready for regular use yet, 
   but uses informational test releases. In this case, :code:`y` can be considered for "breaking" changes and :code:`z` not.
2. Above the :code:`1.y.z` range the release counts as published and is available for public. 
   Releasing at :code:`1.0.0` includes the promise not to break anything until :code:`2.0.0`.
   
Making a Release
----------------
In either case if you do a formal release without :code:`-SNAPSHOT` that must remain the only time that release number is ever used! 
No recycling or re-releasing with the same number! Numbers are cheap and there are a lot of them.

We aim to use a release process in our `Jenkins <http://jenkins.terasology.org/>`_ build server to publish a release 
that'll automatically take off the :code:`-SNAPSHOT` at release time after asking you what scope you're releasing at (major, minor, or patch).

Until that is entirely complete (still experimental) we usually just do the scope increment manually, 
run a release build, then increment to the next snapshot by adding :code:`0.0.1-SNAPSHOT` to the released version (so next after :code:`1.0.0` is :code:`1.0.1-SNAPSHOT`)

.. warning::
   For multiplayer in particular it is critically important that we don't release two modules with the same version number 
   but different content. This can cause all kinds of havoc and obscure issues.