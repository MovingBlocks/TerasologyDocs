# Project

[Sphinx](http://www.sphinx-doc.org) based documentation for [Terasology](https://github.com/MovingBlocks/Terasology). Aim of this project is to bundle existing documentation and re-structure it in a more user-friendly way.

Preview is available at https://oniatus.github.io/.

Separate JavaDoc for the engine is available at https://oniatus.github.io/javadoc.

# Contributing

### Download
Requires `sphinx`, `sphinx-autobuild`, `javasphinx`, `sphinx_rtd_theme` and `sphinxcontrib.youtube` to be installed (install via python `pip`).

**Note** If you are using python3, `pip` will install `sphinx-autobuild` version 0.1.2 which is incompatible with python3. In this case, you might need to download https://github.com/shomah4a/sphinxcontrib.youtube and run `python setup.py install` to install it.  

### Build

Running the server for live-editing: `sphinx-autobuild source build/html` then open [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.

Build the page: `sphinx-build -b html source build`.
