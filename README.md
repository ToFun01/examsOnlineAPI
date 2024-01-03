# 在线考试系统

#### 简述

本项目为前后端分离的Web网站，后端采用Python开源框架Django+DRF（Django REST framework）编写

前端采用uniapp构建PC到移动端自适应的用户界面

```bash
#启动开发服务器
python manage.py runserver
```



## API开发文档

#### Django项目的创建

```bash
# 执行命令创建项目目录，并且进入到项目目录 

mkdir examsOnline && cd examsOnline
```



##### 虚拟环境创建

创建虚拟环境venv，并安装项目依赖

```bash
python -m venv venv
```

激活虚拟环境

```bash
venv\Scripts\activate
#退出虚拟环境
deactivate
```

安装Django和DRF

```bash
pip install django djangorestframework
```

项目依赖管理及版本控制（可选）

```bash
pip freeze > requirements.txt
```

当前依赖包版本（可选）

```tex
asgiref==3.7.2
Django==5.0
djangorestframework==3.14.0
mysqlclient==2.2.1
pytz==2023.3.post1
sqlparse==0.4.4
tzdata==2023.3
```

后续可通过以下终端命令安装依赖（可选）

```bash
pip install -r requirements.txt
```



##### 创建项目配置文件

```bash
#在项目目录下创建config配置文件
django-admin startproject config .
```

注意有个小点，在本级目录下创建

###### 在Django项目中引入DRF：

在config目录下打开**settings.py**文件找到**INSTALLED_APPS**，在列表中加入'**rest_framework**'

```python
INSTALLED_APPS = [
    # ...
    'rest_framework',
    # ...
]
```

###### 配置MySQL数据库：

在**settings.py**中修改**DATABASES**列表

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'examsOnline',
        'USER': '用户名',
        'PASSWORD': '密码',
        'HOST': '18.141.95.29',
        'PORT': '3306',
    }
}
```

安装MySQL官方C驱动的用于连接MySQL数据库的Python客户端

```bash
pip install mysqlclient
```

#### 建立数据表

##### 创建应用

在终端中运行一下命令创建一个叫common的app用作定义数据库模型类

```bash
python manage.py startapp common
```

##### 注册应用

在config/settings.py中的INSTALLED_APPS列表中加入应用配置类common.apps.CommonConfig

```python
INSTALLED_APPS = [
    # ...
    'common.apps.CommonConfig',
    # ...
]
```

##### 建立表结构

根据需求创建好models后，运行

```python
#生成数据库迁移文件
python manage.py makemigrations
#应用迁移文件中的变更
python manage.py migrate
```

