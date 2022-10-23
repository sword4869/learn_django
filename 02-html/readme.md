- [1. 安装](#1-安装)
- [2. 项目配置](#2-项目配置)
- [3. (new)一阶段](#3-new一阶段)
  - [3.1. 创建网页](#31-创建网页)
  - [3.2. 编写 app01中的views.py的index()函数](#32-编写-app01中的viewspy的index函数)
  - [3.3. 将函数和url配对](#33-将函数和url配对)
  - [3.4. 使用js](#34-使用js)
- [4. 启动](#4-启动)
# 1. 安装
```bash
pip install django
```


# 2. 项目配置

项目配置文件`Ki/settings.py`中`INSTALLED_APPS`. 添加App, `"app01.apps.App01Config"`即`app01/apps.py`的类名
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

# 3. (new)一阶段

## 3.1. 创建网页
app01中创建`templates`文件夹, 创建`hello.html`. (`app01/templates/hello.html`)
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Hello</title>
  </head>
  <body>
    <p>Hello</p>
  </body>
</html>
```

## 3.2. 编写 app01中的views.py的index()函数
```python
from django.shortcuts import render

# Create your views here.
def index(request):
    return render(request, "hello.html")
    pass
```

## 3.3. 将函数和url配对
修改项目配置文件`Ki/urls.py`中`urlpatterns`
```python
from django.urls import path
# 导入 app01
from app01 import views
urlpatterns = [
    # path("admin/", admin.site.urls),
    # 映射 index链接到 app01中的views.py的index()函数
    path("index/", views.index),
]
```

## 3.4. 使用js

1. 创建文件夹`app01/static/js`, 添加`main.js`文件
```js
alert('World')
```
2. 修改项目配置`Ki/settings.py`

```python
STATIC_URL = "static/"

STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```
3. 整一个名为`world.html`网页
   
   在最上面添加`{% load static %}`
   js文件`src="{% static 'js/main.js' %}"`
```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>World</title>
  </head>
  <body>
    <p>World</p>
  </body>
  <script src="{% static 'js/main.js' %}"></script>
</html>
```
```python
def world(request):
    return render(request, 'world.html')
```
```python
urlpatterns = [
    # path("admin/", admin.site.urls),
    # 映射 index链接到 app01中的views.py的index()函数
    path("index/", views.index),
    path("", views.world),
]
```
# 4. 启动

```python
$ python manage.py runserver
```

open <http://127.0.0.1:8000/index/>