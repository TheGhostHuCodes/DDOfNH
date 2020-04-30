#################################################
Discovering Disease Outbreaks from News Headlines
#################################################

|license|

My workspace containing code listings from the Manning liveProject
"`Discovering Disease Outbreaks from News Headlines
<https://www.manning.com/liveproject/discovering-disease-outbreaks-from-news-headlines>`_",
by Leonard Apeltsin and Will Koehrsen.

************
Dependencies
************

This project uses `poetry <https://python-poetry.org/>`_ for dependency
management.

Project Dependencies
====================

The project dependency `basemap <https://matplotlib.org/basemap/>`_ is
`deprecated <https://matplotlib.org/basemap/#deprecation-notice>`_ in favor of
the `cartopy <https://scitools.org.uk/cartopy/docs/latest/>`_ project. However,
installing ``cartopy`` is not particularly straightforward. First the ``goes``
compiled binary dependency needs to be installed::

   brew install geos

This will take a while because it will pull in ``gcc``.

The ``cartopy`` library also has a dependency on `shapely
<https://shapely.readthedocs.io/en/latest/>`_, which both have a dependency on
``goes``. To ensure that they are both using the same version of ``goes`` that
we just installed, we need to tell ``poetry`` `not to install the binary that
is included
<https://github.com/python-poetry/poetry/issues/1316#issuecomment-585356227>`_
with ``shapely`` or ``cartopy`` so that it will pick up the system version of
this binary.

Finally, the current stable version of ``cartopy`` is not building on macOS.
However, the latest release candidate is, so we will ask poetry to install the
RC. In the ``fish`` shell this can be done with::

   env PIP_NO_BINARY=shapely poetry add shapely
   env PIP_NO_BINARY=cartopy poetry add cartopy==0.18.0rc1

Development Dependencies
========================

In addition to the listed dev dependencies in the ``pyproject.toml`` file,
there are also two Jupyter labextension libraries that are used for
development:

- `@ryantam626/jupyterlab_code_formatter
  <https://jupyterlab-code-formatter.readthedocs.io/en/latest/>`_
- `@axlair/jupyterlab_vim
  <https://www.npmjs.com/package/@axlair/jupyterlab_vim>`_

Note that ``@axlair/jupyterlab_vim`` is a custom build which is a temporary
solution to getting vim bindings working in JupyterLab 2.X until `this
<https://github.com/jwkvam/jupyterlab-vim/pull/115#issuecomment-596098108>`_ PR
is merged.

.. |license| image:: https://img.shields.io/github/license/TheGhostHuCodes/DDOfNH
