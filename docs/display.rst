.. _display:

======================
THis is a dispaly file
======================

maxdepth
---------------

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   pygate
   repalce <pygate>
   test_v
   https://www.appinn.com/markdown/index.html#autolink
   name<https://www.appinn.com/markdown/index.html#autolink>

numbered
---------
.. toctree::
   :numbered:
   
   pygate
   name<https://www.appinn.com/markdown/index.html#autolink>
   test_v
   
titlesonly
----------
.. toctree::
   :titlesonly:

   pygate
   test_v

glob
-----
.. toctree::
   :glob:
   :titlesonly:

   pygate*
   test_v/*
   *

hidden
-------
.. toctree::
   :hidden:

   pygate
   test_v



asdasdasda


.. automodule:: docs1
.. automodule:: __init__
.. autodoc:: docs1
   



py domain
----------

.. py:function:: format_exception(etype, value, tb[, limit=None])

   Format the exception with a traceback.

   :param etype: exception type
   :param value: exception value
   :param tb: traceback object
   :param limit: maximum number of stack frames to show
   :type limit: integer or None
   :rtype: list of strings