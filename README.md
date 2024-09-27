# jupyterlab-quickopen

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/jupyterlab-contrib/jupyterlab-quickopen/master?urlpath=lab%2Ftree%2Fbinder%2Ftutorial.ipynb)

Quickly open a file in JupyterLab by typing part of its name

![Animation showing entering partial filenames in the quick open sidebar and the corresponding file editor opening](https://raw.githubusercontent.com/jupyterlab-contrib/jupyterlab-quickopen/master/doc/quickopen.gif)

## Compatibility

- Python >=3.8.x
- [JupyterLab](https://github.com/jupyterlab/jupyterlab) >=3.2,<4.0
- [Jupyter Server](https://github.com/jupyter/jupyter_server) >=1.6,<2.0
- Configurations where notebook documents and other files reside on a filesystem local to the
  Jupyter Server (which is the the default), not remote storage (e.g., S3)

## Install

Starting in version 1.0 of this extension, the frontend portion of this extension is pre-compiled
and included in the `pip` installed package thanks to [changes in the JupyterLab 3.0 packaging
system](https://jupyterlab.readthedocs.io/en/stable/getting_started/changelog.html#extensions-can-be-installed-without-building-jupyterlab-with-nodejs).

To install the Jupyter Notebook server extension under `PREFIX` (e.g., the active virtualenv or conda
env), run the following:

```bash
pip install jupyterlab-quickopen
```

## Configure

### Using a custom Keyboard Shortcut

The default keyboard shortcut for opening the quickopen panel is `Accel Ctrl P`.

You can assign your own keyboard shortcut to show the quickopen panel at any time. Open the keyboard editor
by clicking _Settings &rarr; Advanced Settings Editor &rarr; Keyboard Shortcuts_. Then enter JSON in
the _User Overrides_ text area like the following, adjusting the `keys` value to assign the shortcut
of your choosing:

```json
{
  "shortcuts": [
    {
      "command": "quickopen:activate",
      "keys": ["Accel Ctrl P"],
      "selector": "body",
      "title": "Activate Quick Open",
      "category": "Main Area"
    }
  ]
}
```

### Patterns to Exclude

You can control which files to exclude from the quick open list using Notebook server settings,
JupyterLab settings, or both.

On the server side, use the `ContentsManager.allow_hidden` and/or `ContentsManager.hide_globs`
settings. See the
[documentation about Jupyter Server options](https://jupyter-server.readthedocs.io/en/latest/operators/configuring-extensions.html)
for details.

In the JupyterLab web app, open the _Settings_ menu, click the _Advanced Settings Editor_ option,
select the _Quick Open_ item in the _Raw View_ sidebar, and enter JSON in the _User Overrides_ text
area to override the default values.

![Screenshot of the quick open settings editor](./doc/settings.png)

### Development install

Note: You will need NodeJS to build the extension package.

The `jlpm` command is JupyterLab's pinned version of
[yarn](https://yarnpkg.com/) that is installed with JupyterLab. You may use
`yarn` or `npm` in lieu of `jlpm` below.

```bash
# Clone the repo to your local environment
# Change directory to the jupyterlab_quickopen directory
# Install package in development mode
pip install -e .
# Link your development version of the extension with JupyterLab
jupyter labextension develop . --overwrite
# Server extension must be manually installed in develop mode
jupyter server extension enable jupyterlab_quickopen
# Rebuild extension Typescript source after making changes
jlpm build
```

You can watch the source directory and run JupyterLab at the same time in different terminals to watch for changes in the extension's source and automatically rebuild the extension.

```bash
# Watch the source directory in one terminal, automatically rebuilding when needed
jlpm watch
# Run JupyterLab in another terminal
jupyter lab
```

With the watch command running, every saved change will immediately be built locally and available in your running JupyterLab. Refresh JupyterLab to load the change in your browser (you may need to wait several seconds for the extension to be rebuilt).

By default, the `jlpm build` command generates the source maps for this extension to make it easier to debug using the browser dev tools. To also generate source maps for the JupyterLab core extensions, you can run the following command:

```bash
jupyter lab build --minimize=False
```

### Releasing

See [RELEASE](RELEASE.md)

### Acknowledgements

This extension was originally created by [Peter Parente](https://github.com/parente) and was
later moved to the `jupyterlab-contrib` GitHub organization.
