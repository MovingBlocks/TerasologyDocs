#Project

[Sphinx](http://www.sphinx-doc.org) based documentation for [Terasology](https://github.com/MovingBlocks/Terasology). Aim of this project is to bundle existing documentation and re-structure it in a more user-friendly way.

Preview is available at https://oniatus.github.io/

#Contributing

Requires `sphinx`, `sphinx-autobuild` and `sphinx_rtd_theme` to be installed (install via python `pip`).

Running the server for live-editing: `sphinx-autobuild source build/html` then open [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.

Build the page: `sphinx-build -b html source build`.