.. zhixuewang documentation master file, created by
   sphinx-quickstart on Fri Mar 20 09:03:58 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

安装
======================================
使用 pip 安装(推荐)
---------------------
::

    pip install zhixuewang

下载 源码 安装
---------------------
把项目源码下载后, 在项目根目录输入::

    python setup install

或直接::

    git clone https://github.com/anwenhu/zhixuewang
    cd zhixuewang
    python setup.py install


简单实例
======================================
保证你已经安装好zhixuewang后, 通过这样来获取自己最新一次考试成绩并打印到屏幕上::

    from zhixuewang import login
    username = input("你的用户名:").strip()
    password = input("你的密码:").strip()
    zxw = login(username, password)
    print(zxw.get_self_mark())

在输入智学网用户名和密码后, 屏幕上会显示形如::

    name 语文:
    分数: 105
    name 数学:
    分数: 120
    name 英语:
    分数: 132
    name 物理:
    分数: 68
    name 化学:
    分数: 52
    name 政治:
    分数: 49
    name 历史:
    分数: 59
    name 总分:
    分数: 585

其中 `name` 的位置应该显示你的名字

(注: 因为智学网移除了部分接口, 所以查询班级平均分, 班级最高分等功能暂时失效)

如果你想要查询指定考试的成绩, 如查询"某中学第二次月考", 可这样做(假定你已经运行了前面的代码)::

    print(zxw.get_self_mark("某中学第二次月考"))


登录
======================================

登录的函数有

.. autofunction:: zhixuewang.login
    :noindex:
.. autofunction:: zhixuewang.login_id
    :noindex:
.. autofunction:: zhixuewang.login_student
    :noindex:
.. autofunction:: zhixuewang.login_teacher
    :noindex:
.. autofunction:: zhixuewang.login_student_id
    :noindex:
.. autofunction:: zhixuewang.login_teacher_id
    :noindex:


你可以通过::

    from zhixuewang import *

来导入它们

其中 `login(username: str, password: str)` 与 `login_id(user_id: str, password: str)` 属于通用函数, 可以支持学生, 老师登录.


API列表
======================================

学生账号
------------------

.. autoclass:: zhixuewang.student.Student
    :members:
    :undoc-members:
    :noindex:

老师账号
------------------

.. autoclass:: zhixuewang.teacher.Teacher
    :members:
    :undoc-members:
    :noindex:

常见问题
======================================

如果您在使用的过程中遇到任何问题，欢迎前往 [Issue](https://github.com/anwenhu/zhixuewang/issues)提问
当然也可以加入这个QQ群讨论：862767072

高级功能
======================================

自定义展示
------------------
只需重写相应类的 `__str__` 方法, 可通过装饰器简化操作
例如:如果你想展示加权后的成绩, 比如说计算 `语文*0.8+数学*0.7+英语*0.5` 后的成绩, 可以这么做::

    from zhixuewang import rewrite_str
    import zhixuewang

    @rewrite_str(zhixuewang.models.examModel.Mark)
    def _(self):
        score = 0
        for subject in self:
            if subject.subject.name == "语文":
                score += subject.score * 0.8
            elif subject.subject.name == "数学":
                score += subject.score * 0.7
            elif subject.subject.name == "英语":
                score += subject.score * 0.5
        return f"加权后的分数为: {score}"

详细文档
==================
* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
