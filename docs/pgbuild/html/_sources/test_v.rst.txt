===========
一级标题
===========

二级
-----

三级
^^^^

四级
~~~~

五级
####

段落与换行
----------
段落顶格写
    缩进被视为引文
  随便缩进
缩进后就是第2个段落了。\
还是第2个段落，没有换行符，段落间要有完整的空行

现在是第三个段落

文字样式
---------

星号: *text* 是强调 (斜体),

双星号: **text** 重点强调 (加粗),

反引号: ``text`` 代码样式.

注意：rst中这些符号前后不能与其他字符相邻，否则就只是本身的符号

图表
-----

=====  =====  ======
   Inputs     Output
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======

列表
-----
无符号列表

* 第一条无符号列表
   + 二级列表
        - 三级列表
            + 嵌套列表
* 第二条
* 第三条

顺序列表

1. 第一条 
#. 第二条，第二条之后可以都用 *#* 代替

a. 小写字母
#. 小写

A. 大写字母

i) 小写罗马数字

(I) 大写罗马数字


文字样式
---------

星号: *text* 是强调 (斜体),

双星号: **text** 重点强调 (加粗),

反引号: ``text`` 代码样式.

..
  样式无法相互嵌套


.. image:: ttt.jpg

.

嵌入程序代码
------------


下面是引用的代码::




这是一段正常文本. 下一段是代码文字::

   它不需要特别处理，仅是
   缩进就可以了.

   它可以有多行.
   *没法嵌入其他样式*
再是正常的文本段.


environment
  一个结构，包含信息是所有文档的保存路径，使用的参考文献等.
  在解析的阶段使用，因此连续运行时仅需解析新的或修改过的文档.

source directory
  根路径，包含子目录，包含一个Sphinx工程的所有源文件.


跳转到文件 :doc:`./display`

跳转到标记文件 :ref:`pygate`

下载文件 :download:`conf.py`

:envvar:``
:token:``
:keyword:``
:option:``
:term:``


:doc:`Text.txt`

:doc:`test_v.md`

.. index:: BNF, grammar, syntax, notation

.. tabularcolumns:: column spec

.. note:: for note
.. warning:: for warning
.. versionadded:: for version
.. centered:: LICENSE AGREEMENT

.. py:function:: Timer.repeat([repeat=3[, number=1000000]])

`def removename(func):`
    `func.__name__ = ''`
    `return func`

def setnewname(name):
    def decorator(func):
        func.__name__ = name
        return func
    return decorator

.. py:decorator:: removename

   Remove name of the decorated function.

.. py:decorator:: setnewname(name)

   Set name of the decorated function to *name*.

.. function:: enumerate(sequence[, start=0])

:py:func: `enumerate` 函数用于 ...


.. py:decorator:: removename

   Remove name of the decorated function.


.. function:: format_exception(etype, value, tb[, limit=None])

   Format the exception with a traceback.

   :param etype: exception type
   :param value: exception value
   :param tb: traceback object
   :param limit: maximum number of stack frames to show
   :type limit: integer or None
   :rtype: list of strings