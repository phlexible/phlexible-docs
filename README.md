phlexible Documentation
=======================

This documentation is rendered online at [phlexible Documentation](https://public.brainbits.net/bamboo/browse/BB-PHLEXDOC0-13/artifact/JOB1/docs-html/index.html)

Contributing
------------

**Note**

>Each phlexible version has its own branch (e.g. **1.0**). Do **not** edit the
>master branch, but checkout (or create) the correct branch for your version.

If you want to contribute, you need to become familiar with the markup language
[reStructuredText](http://docutils.sourceforge.net/rst.html) used by the documentation.

Additionally we use [Sphinx](http://sphinx-doc.org/) to build the output (HTML, PDF, ...).

Fist you have to install Sphinx. See their documentation on how to do that.
After Sphinx is installed, you need to add "our" theme by executing:

``` bash
$ easy_install sphinx_rtd_theme
```

When you're ready, clone this repository...

``` bash
$ git clone ssh://git@git.brainbits.net/bb/phlexible-docs.git
```

...and checkout the desired branch (for example 1.0):

``` bash
$ git checkout 1.0
```

Now you have to install necessary Sphinx extensions. Just change into the checked out
directory and type:

``` bash
$ git submodule update --init
```

Run `make html` to (re-)build the documentation and view the generated HTML in the `_build`
directory.
