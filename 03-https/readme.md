- [1. 安装](#1-安装)
- [2. 项目配置](#2-项目配置)
- [3. 正式工作](#3-正式工作)
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
# 3. 正式工作
1. 在02-html的hello.html基础上.
2. 添加Host
    不然报错`DisallowedHost`
    项目配置文件`Ki/settings.py`
```python
ALLOWED_HOSTS = ['*']
```

2. 安装插件

```bash
pip install django-extensions, django-werkzeug-debugger-runserver, pyOpenSSL
```
3. 项目配置文件`Ki/settings.py`中`INSTALLED_APPS`, 添加
```python
'werkzeug_debugger_runserver',  # 开启https需要的服务
'django_extensions',  # 开启https需要的服务
```

# 4. 启动

```python
# runserver_plus 表示使用 https
# --cert server.crt 表示证书
$ python manage.py runserver_plus --cert server.crt 0.0.0.0:8000
```

open <https://0.0.0.0:8000>

运行后会发现生成的证书: `server.crt`, `server.key`