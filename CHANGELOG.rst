Changelog
---------


0.9.0 (2015-09-20)
++++++++++++++++++++

* **不兼容** 将拼音词典库里的国际音标字母替换为 ASCII 字母. Thanks `@MingStar`_ :
    * ``ɑ -> a``
    * ``ɡ -> g``


0.8.5 (2015-08-23)
++++++++++++++++++++

* **bugfix** 修复 zh, ch, sh, z, c, s 顺序问题导致获取声母有误


0.8.4 (2015-08-23)
++++++++++++++++++++

* ``y``, ``w`` 也不是声母. (`hotoo/pinyin#57 <https://github.com/hotoo/pinyin/issues/57>`__)


0.8.3 (2015-08-20)
++++++++++++++++++++

* 上传到 PyPI 出了点问题，但是又 `没法重新上传 <http://sourceforge.net/p/pypi/support-requests/468/>`__ ，只好新增一个版本


0.8.2 (2015-08-20)
++++++++++++++++++++

* **bugfix** 修复误把 yu 放入声母列表里的 BUG(`#22`_). Thanks `@MingStar`_


0.8.1 (2015-07-04)
++++++++++++++++++++

* **bugfix** 重构内置的分词功能，修复“无法正确处理包含空格的字符串的问题”


0.8.0 (2015-06-27)
+++++++++++++++++++++

* **新增** 内置简单的分词功能，完善处理没有拼音的字符
  （如果不需要处理多音字问题, 现在可以不用安装 ``jieba`` 或其他分词模块了）::

        # 之前, 安装了结巴分词模块
        lazy_pinyin(u'你好abc☆☆')
        [u'ni', u'hao', 'a', 'b', 'c', u'\u2606', u'\u2606']

        # 现在, 无论是否安装结巴分词模块
        lazy_pinyin(u'你好abc☆☆')
        [u'ni', u'hao', u'abc\u2606\u2606']

* | **[变更]** 当 ``errors`` 参数是回调函数时，函数的参数由 ``单个字符`` 变更为 ``单个字符或词组`` 。
  | 即: 对于 ``abc`` 字符串, 之前将调用三次 ``errors`` 回调函数: ``func('a') ... func('b') ... func('abc')``
  | 现在只调用一次: ``func('abc')`` 。
* **[变更]** 将英文字符也纳入 ``errors`` 参数的处理范围::

        # 之前
        lazy_pinyin(u'abc', errors='ignore')
        [u'abc']

        # 现在
        lazy_pinyin(u'abc', errors='ignore')
        []

0.7.0 (2015-06-20)
+++++++++++++++++++++

* **修复** Python 2 下无法使用 ``from pypinyin import *`` 的问题
* **新增** 支持以下环境变量:

  * ``PYPINYIN_NO_JIEBA=true``: 禁用“自动调用结巴分词模块”
  * ``PYPINYIN_NO_PHRASES=true``: 禁用内置的“词组拼音库”


0.6.0 (2015-06-10)
+++++++++++++++++++++

* **新增** ``errors`` 参数支持回调函数(`#17`_): ::

    def foobar(char):
        return 'a'
    pinyin(u'あ', errors=foobar)

0.5.7 (2015-05-17)
+++++++++++++++++++

* 纠正包含 "便宜" 的一些词组的读音


0.5.6 (2015-02-26)
+++++++++++++++++++

* **fix** "苹果" pinyin error. `#11`__
* 精简 phrases_dict
* **fix** 重复 import jieba 的问题
* 更新文档

__ https://github.com/mozillazg/python-pinyin/issues/11


0.5.5 (2015-01-27)
+++++++++++++++++++

* **fix** phrases_dict error


0.5.4 (2014-12-26)
+++++++++++++++++++

* **修复** 无法正确处理由分词模块产生的中英文混合词组（比如：B超，维生素C）的问题.  `#8`__

__ https://github.com/mozillazg/python-pinyin/issues/8


0.5.3 (2014-12-07)
+++++++++++++++++++

* 更新拼音库


0.5.2 (2014-09-21)
++++++++++++++++++

* 载入拼音库时，改为载入其副本。防止内置的拼音库被破坏
* **修复** ``胜败乃兵家常事`` 的音标问题


0.5.1 (2014-03-09)
++++++++++++++++++

* **新增** 参数 ``errors`` 用来控制如何处理没有拼音的字符:

  * ``'default'``: 保留原始字符
  * ``'ignore'``: 忽略该字符
  * ``'replace'``: 替换为去掉 ``\u`` 的 unicode 编码字符串(``u'\u90aa'`` => ``u'90aa'``)

  只处理 ``[^a-zA-Z0-9_]`` 字符。


0.5.0 (2014-03-01)
++++++++++++++++++

* **使用新的单字拼音库内容和格式**

  | 新的格式：``{0x963F: u"ā,ē"}``
  | 旧的格式：``{u'啊': u"ā,ē"}``


0.4.4 (2014-01-16)
++++++++++++++++++

* 清理命令行命令的输出结果，去除无关信息
* **修复** “ImportError: No module named runner”


0.4.3 (2014-01-10)
++++++++++++++++++

* **修复** 命令行工具在 Python 3 下的兼容性问题


0.4.2 (2014-01-10)
++++++++++++++++++

* **去除** 拼音风格前的 ``STYLE_`` 前缀（兼容包含 ``STYLE_`` 前缀的拼音风格）
* **增加** 命令行工具，具体用法请见： ``pypinyin -h``


0.4.1 (2014-01-04)
++++++++++++++++++

* **新增** 支持自定义拼音库，方便用户修正程序结果


0.4.0 (2014-01-03)
++++++++++++++++++

* **变更** 将 ``jieba`` 模块改为可选安装，用户可以选择使用自己喜爱的分词模块对汉字进行分词处理
* **新增** 支持 Python 3


0.3.1 (2013-12-24)
++++++++++++++++++

* **增加** ``lazy_pinyin`` ::

    >>> lazy_pinyin(u'中心')
    ['zhong', 'xin']


0.3.0 (2013-09-26)
++++++++++++++++++

* **修复** 首字母风格无法正确处理只有韵母的汉字

* **新增** 三个拼音风格:
    * ``pypinyin.STYLE_FINALS`` ：       韵母风格1，只返回各个拼音的韵母部分，不带声调。如： ``ong uo``
    * ``pypinyin.STYLE_FINALS_TONE`` ：   韵母风格2，带声调，声调在韵母第一个字母上。如： ``ōng uó``
    * ``pypinyin.STYLE_FINALS_TONE2`` ：  韵母风格2，带声调，声调在各个拼音之后，用数字 [0-4] 进行表示。如： ``o1ng uo2``


0.2.0 (2013-09-22)
++++++++++++++++++

* 完善对中英文混合字符串的支持::

    >> pypinyin.pinyin(u'你好abc')
    [[u'n\u01d0'], [u'h\u01ceo'], [u'abc']]


0.1.0 (2013-09-21)
++++++++++++++++++

* Initial Release

.. _#17: https://github.com/mozillazg/python-pinyin/pull/17
.. _#22: https://github.com/mozillazg/python-pinyin/pull/22
.. _@MingStar: https://github.com/MingStar
