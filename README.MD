[Sphinx](http://www.sphinx-doc.org) based documentation for Terasology.

Requires `sphinix`, `sphinx-autobuild` and `sphinx_rtd_theme` to be installed (install via python `pip`).

Running the server for live-editing: `sphinx-autobuild source build/html` then open [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.

Building the html: `sphinx-build -b html source build`