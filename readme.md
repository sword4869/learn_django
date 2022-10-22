
# 安装
```bash
pip install django
```

```bash
# 创建项目
$ django-admin startproject <project name>

$ tree
.
├── Ki                  项目的管理,启动项目,创建APP,数据管理
│   ├── asgi.py         [固定]接受异步的网络请求
│   ├── __init__.py     
│   ├── settings.py     *[关键]项目配置文件,数据库
│   ├── urls.py         *[关键]URL和函数的对应关系
│   └── wsgi.py         [固定]接受同步的网络请求
└── manage.py
```
```bash
# 创建app
$ python manage.py startapp <app name>

$ tree
.
├── app01
│   ├── admin.py            [固定]默认admin后台管理
│   ├── apps.py             [固定]app启动
│   ├── __init__.py
│   ├── migrations          [固定]数据库变更记录
│   │   └── __init__.py
│   ├── models.py           *[关键]操作数据库
│   ├── tests.py            [固定]单元测试
│   └── views.py            *[核心]url对应的函数
├── Ki
│   ├── asgi.py
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py

```

# 启动

```python
$ python manage.py runserver
```

open <http://127.0.0.1:8000/index/>