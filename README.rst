.. _l-README:

README
======

.. contents::
   :depth: 3


Introduction
------------

This project is a skeleton for any new project. It contains:
    * a source folder: ``src``
    * a unit test folder: ``_unittests``, go to this folder and run ``run_unittests.py``
    * a _doc folder: ``_doc``, it will contains the documentation
    * a file ``setup.py`` to build and to install the module
    * a file ``make_help.py`` to build the sphinx documentation
    
To create your own project, you need to rename the folder ``project_name`` in ``src``
by your true module name. You also need to replace ``project_name`` wherever it is found:
    * ``project_var_name  = 'project_name'`` in ``setup.py``, ``make_help.py`` and ``_doc/sphinxdoc/source/conf.py``
    * ``from src.project_name.subproject.myexample import myclass`` in ``_unittests/ut_example/test_example.py``
    * many places in ``_doc/sphinxdoc/source/index.rst``
    * many places in ``README.rst``
    
Prerequisites
-------------

To build the documentation, you need:
    * `numpy <http://www.numpy.org/>`_
    * `Sphinx <http://sphinx-doc.org/>`_
    * `pyhome3 <http://www.xavierdupre.fr/site2013/index_code.html>`_
    
    
Automation
----------
    
Unit tests
++++++++++
    
The project includes an easy to write and run unit tests:
    * the file ``_unittests/run_unittests.py`` runs all of them.
    * you can add a new one in a folder: ``_unittests/<subfolder>/test_<filename>.py``.
    
This test file must begin by ``test_`` and must look like the following::

    """
    @brief      test log(time=1s)

    You should indicate a time in seconds. The program ``run_unittests.py``
    will sort all test files by increasing time and run them.
    """

    import sys, os, unittest
    from pyhome3 import fLOG  # it requires pyhome3.

    # to import files from the module
    try :
        import src
    except ImportError :
        path = os.path.normpath(os.path.abspath( os.path.join( os.path.split(__file__)[0], "..", "..")))
        if path not in sys.path : sys.path.append (path)
        import src

    # import the file you want to test 
    from src.project_name.subproject.myexample import myclass

    class TestExample (unittest.TestCase):
        
        def test_split_cmp_command(self) :

            # to log information
            fLOG (__file__, self._testMethodName, OutputPrint = __name__ == "__main__")
            
            # you test content
            # it must raises an exception if a test fails.

    if __name__ == "__main__"  :
        unittest.main ()        

Generation of the documentation
+++++++++++++++++++++++++++++++

The program ``make_help.py`` without any required change except mention in the introduction.
Just run it. It will go through the following steps:
    * it will copy all files found in ``src`` in folder ``_doc/sphinxdoc/source/project_name``
    * it will generates a file .rst for each python file in ``_doc/sphinxdoc/source/project_name``
    * it will run the generation of the documentation using Sphinx.
    
The results are stored in folder ``_doc/sphinxdoc/build``.

Generation of the setup
+++++++++++++++++++++++

Unless you add an extension or some data to your module (images, text files),
no modification are required. To generate a zip or gz setup::

    %pythonexe% setup.py sdist --formats=gztar,zip
    
To generate an executable setup on Windows::

    %pythonexe% setup.py bdist_wininst

On Windows, the file ``build_setup_help_on_windows.bat`` does everything for you.


Source
------

The following folders contain:

* ``_doc``: Sphinx documentation.
* ``_unittests``: unit tests, you can run them by running the function :func:`check <__init__.check>` (as root on linux)
* ``src``: the sources
