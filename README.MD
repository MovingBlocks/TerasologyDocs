# Project

[Sphinx](http://www.sphinx-doc.org) based documentation for [Terasology](https://github.com/MovingBlocks/Terasology). Aim of this project is to bundle existing documentation and re-structure it in a more user-friendly way.

The page of this documentation is available  https://metaterasology.github.io/docs/.

# Contributing

Something is missing in the docs? Feel free to fork and submit a PR or open an [issue](https://github.com/MovingBlocks/TerasologyDocs/issues).

## Workspace setup
Requires `sphinx`, `sphinx-autobuild`, `javasphinx`, `sphinx_rtd_theme` and `sphinxcontrib.youtube` to be installed (install via python `pip`).

**Note** If you are using python3, `pip` will install `sphinx-autobuild` version 0.1.2 which is incompatible with python3. In this case, you might need to download https://github.com/shomah4a/sphinxcontrib.youtube and run `python setup.py install` to install it.  

Any editor for the `.rst` sources is fine, e.g. for Eclipse the [ReST Editor](http://marketplace.eclipse.org/content/rest-editor).

## Build

Running the server for live-editing: `sphinx-autobuild source build/html` then open [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.

Build the page: `sphinx-build -b html source build`.


# Page setup

All page settings are configured in `conf.py`.

## Mapping for the edit-on-github buttons:
```
edit_on_github_project = 'MovingBlocks/TerasologyDocs'
edit_on_github_branch = 'master/source'
```

## Javadoc location:
```
javadoc_url_map = {
    'org.terasology' : ('https://oniatus.github.io/javadoc', 'javadoc8')
}
```

For the setup inside the github page, create the javadoc with `./gradlew engine:javadoc` in the Terasology project, then copy the `engine/build/docs/javadoc` directory to the github page.