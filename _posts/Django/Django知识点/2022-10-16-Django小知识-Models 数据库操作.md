---
ifupdate: false
layout: post
title: Django小知识-Models 数据库操作
subtitle: Django知识点
date: 2022-10-16
author: Carlos
header-img: img/bg-cook.jpg
catalog: true
tags:
 - Django
---
{% raw %}# Django中Models 数据库操作-创建model

在Django中，`Model`是应用程序的数据存储和业务逻辑的核心，用于定义如何管理数据，以及如何与数据进行交互和修改。使用`Model`可以轻松地创建数据库表以及对其进行操作，极大地提升了应用程序的开发效率和可维护性。本文将介绍如何在Django中创建`Model`，并对其进行常见操作。

## 准备工作

1.在settings 文件中，INSTALLED_APPS 添加App“SFT”。 Django 在启动时会自动加载 'SFT' 应用，使其成为可用的应用程序，可以在项目中使用这个自定义应用的模型、视图和其他组件。

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # 添加 
    'SFT',
]
```

2.在settings 文件中，DATABASES 支持的数据库后端有多种，如MySQL、PostgreSQL、SQLite等，可以根据不同的需求进行选择。其中，每个数据库后端需要安装对应的驱动程序才能正常使用，如使用MySQL时需要安装`mysqlclient`或`pymysql`等驱动程序。

```python
# 连接本地SQLite 数据库
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# 连接mysql 数据库
DATABASES = {
     'default': {
         'ENGINE': 'django.db.backends.mysql',
         'NAME': 'user_manage', #db名称
         'USER': 'root',
         'PASSWORD': '123456',
         'HOST': '127.0.0.1',
         'PORT': '3306',
     }
 }  
```

### 创建Model

在Django中，`models.py`文件用于定义数据表的结构和字段属性。下面是列出所有定义数据表的结构和字段属性的用法

#### 导入模块

```python
from django.db import models
```

#### 创建模型

```python
class City(models.Model):
    name = models.CharField(max_length=50, verbose_name='城市名称')
    code = models.CharField(max_length=20, verbose_name='城市编码')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='创建日期')
    description = models.TextField(null=True, blank=True, verbose_name='城市描述')
    image = models.ImageField(upload_to='city_images/', null=True, blank=True, verbose_name='城市图片')
```

#### 定义模型属性

上面的代码中，我们定义了一个名为`City`的模型类，它继承自`models.Model`。这个模型类有四个属性，分别name、code、created_at、description、image。

#### 定义字段类型

- `CharField`：用于存储字符串类型的数据，对应数据库中的VARCHAR类型。在创建时需要指定最大长度。
- `DateField`：用于存储日期类型的数据，对应数据库中的DATE类型。
- `DecimalField`：用于存储精确到小数点后若干位的数字类型的数据，对应数据库中的DECIMAL类型。在创建时需要指定数字的总位数和小数位数。
- `IntegerField`：用于存储整数类型的数据，对应数据库中的INT或BIGINT类型。
- `BooleanField`：布尔值对应数据中的BOOLE类型
- `FileField` : 用于存储文件相关数据，对应数据库中的FILE类型

还有其他许多字段类型可供选择，如`TextField`、`BooleanField`、`ForeignKey`、`ManyToManyField`等。

#### 定义字段属性

1. `unique`

该选项用于设置字段是否唯一。如果设置为`True`，则该字段的值在整个表中必须是唯一的。

```python
class MyModel(models.Model):
    my_field = models.CharField(max_length=50, unique=True)
```

2. `max_length`

该选项用于限制字符串类型字段的最大长度。

```python
class MyModel(models.Model):
    my_field = models.CharField(max_length=50)
```

3. `default`

该选项用于设置字段的默认值。

```python
class MyModel(models.Model):
    my_field = models.CharField(max_length=50, default='default value')
```

4. `null`

该选项用于设置字段是否为`NULL`。如果设置为`True`，则允许该字段的值为空值。

```python
class MyModel(models.Model):
    my_field = models.CharField(max_length=50, null=True)
```

5. `blank`

该选项用于设置字段是否可以为空字符串。如果设置为`True`，则该字段的值可以为空字符串。

```python
class MyModel(models.Model):
    my_field = models.CharField(max_length=50, blank=True)
```

6. `choices`

该选项用于设置枚举类型的字段。可以设置一个二元组列表，其中每个二元组包含两个值，分别是值和显示值。

```python
class MyModel(models.Model):
    COLOR_CHOICES = [
        ('red', 'Red'),
        ('green', 'Green'),
        ('blue', 'Blue'),
    ]
    color = models.CharField(max_length=10, choices=COLOR_CHOICES)
```

7. `min_value` 和 `max_value`

这两个选项用于限制整数类型字段的取值范围，分别表示最小值和最大值。

```python
class MyModel(models.Model):
    my_field = models.IntegerField(min_value=0, max_value=100)
```

8. `auto_now` 和 `auto_now_add`

这两个选项用于设置 时间类型 字段的自动更新。`auto_now` 用于记录每次修改的时间，`auto_now_add` 用于记录创建的时间。

```python
class MyModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

9. `decimal_places` 和 `max_digits`

这两个选项用于设置浮点数类型字段的精度，分别表示小数位数和数字总位数。

```python
class MyModel(models.Model):
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

除了定义属性，我们还可以在模型中定义方法。例如：

```python
class City(models.Model):
    name = models.CharField(max_length=50, verbose_name='城市名称')
    code = models.CharField(max_length=20, verbose_name='城市编码')
    created_at = models.DateTimeField(auto_now_add=True, verbose_name='创建日期')
    description = models.TextField(null=True, blank=True, verbose_name='城市描述')
    image = models.ImageField(upload_to='city_images/', null=True, blank=True, verbose_name='城市图片')

    def __str__(self):
        return self.city
```

上述代码中，我们定义了一个`__str__`方法，当我们在Python交互环境中输出该模型实例时，它将返回书籍的名称。

以上便是在Django中定义数据表的结构和字段属性的基本用法。通过这种方式，我们可以轻松地创建数据库表并操作其中的数据。

### 生成数据库表

在新建或修改完`Model`之后，需要通过Django的迁移工具来同步数据库表。迁移是Django自带的一个管理数据库模式变化的工具，它可以记录每次对模型的更改，然后根据这些更改生成相应的SQL语句，最终同步到数据库中。

首先需要运行以下命令来创建迁移文件：

```python
python3 manage.py makemigrations (your_app_name)
```

其中，`your_app_name`是你的应用程序的名称。执行上述命令后，Django会扫描`your_app_name`目录下的所有模型，不填写`your_app_name`则扫描所有app下目录的模型，并检测模型的变化情况，然后生成一个包含这些变化的迁移文件。接下来，需要再执行以下命令来将迁移文件同步到数据库中：

```python
python3 manage.py migrate
```

运行以上命令后，Django就会根据迁移文件来创建或修改数据库表结构。

![](C:\Users\carlos\AppData\Roaming\marktext\images\2023-05-24-17-07-43-image.png)

![](C:\Users\carlos\AppData\Roaming\marktext\images\2023-05-24-17-07-30-image.png)
{% endraw %}