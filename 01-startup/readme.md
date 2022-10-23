- [1. 安装](#1-安装)
- [2. 项目配置](#2-项目配置)
- [3. 正式工作](#3-正式工作)
  - [3.1. 编写 app01中的views.py的函数](#31-编写-app01中的viewspy的函数)
  - [3.2. 将函数和url配对](#32-将函数和url配对)
- [4. 启动](#4-启动)
# 1. 安装
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

# 2. 项目配置

项目配置文件`Ki/settings.py`中`INSTALLED_APPS`. 添加App, `"app01.apps.App01Config"`即`app01/apps.py`的类名`App01Config`
```python
#  app01/apps.py
class App01Config(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "app01"
```
```python
# Ki/settings.py
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "app01.apps.App01Config"
]
```

# 3. 正式工作

## 3.1. 编写 app01中的views.py的函数
```python
from django.shortcuts import render
# 导入 HttpResponse
from django.shortcuts import HttpResponse

# Create your views here.
def hello(request):
    return HttpResponse("hello")
    pass
```

## 3.2. 将函数和url配对

修改项目配置文件`Ki/urls.py`中`urlpatterns`
```python
from django.urls import path
# 导入 app01
from app01 import views
urlpatterns = [
    # path("admin/", admin.site.urls),
    # 根映射
    path("", views.hello),
]
```
映射<http://127.0.0.1:8000/hello/>链接到 app01中的views.py的hello()函数, `path("hello/", views.hello),`

# 4. 启动

```python
$ python manage.py runserver
```

open <http://127.0.0.1:8000>