---
ifupdate: false
layout: post
title: Flask-Migrate 迁移 ORM 模型
subtitle: falsk_数据库相关操作
date: 2022-12-28
author: Carlos
header-img: img/bg-cook.jpg
catalog: true
tags:
 - Flask
---
{% raw %}# Flask Migrate 迁移 ORM 模型

Flask-Migrate 是 Flask 的一个扩展库，用于管理和迁移数据库。它基于 SQLAlchemy，提供了简单易用的方法来创建、修改和更新数据库表格结构。本文将介绍如何使用 Flask-Migrate 迁移 ORM 模型，并对 Flask-Migrate 迁移方法进行详细解释。

## 1. 安装和配置

首先，我们需要安装 Flask-Migrate 及其依赖库。可以使用以下命令进行安装：

```bash
pip install pymysql flask flask_sqlalchemy flask_migrate
```

在安装完成后，我们可以开始配置和连接数据库。在示例中，我们选择使用 MySQL 数据库。通过调用 `SQLAlchemy` 的 `create_engine` 方法，创建并返回一个数据库对象 `db`，用于后续的数据库操作。

```python
import pymysql
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)

def connect_flask_mysql(app, username="root", password="123456", host='127.0.0.1', port=3306, db='Flask_Migrate_study'):
    app.config['SQLALCHEMY_DATABASE_URI'] = f'mysql+pymysql://{username}:{password}@{host}:{port}/{db}?charset=utf8'
    app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
    db = SQLAlchemy(app)
    return db

# 使用 SQLAlchemy 提供的模型类定义表格结构
db = connect_flask_mysql(app)
```

## 2. 创建模型类

在连接数据库后，我们使用 SQLAlchemy 提供的模型类来定义数据库中的表格结构。在示例中，我们创建了两个模型类 `Student` 和 `Class`，分别表示学生和班级。

```python
class Student(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    class_id = db.Column(db.Integer, db.ForeignKey('class.id'))

    if random.choice([False,True]):
        age=db.db.Column(db.Integer)  # 新增字段

class Class(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)

    if random.choice([False,True]):
        count=db.db.Column(db.Integer)  # 新增字段
```

在模型类中，我们使用 `db.Column` 来定义表格的各个字段，包括字段的类型、约束等。根据随机选择的条件，可能会添加额外的 `age` 和 `count` 字段。通过这种方式，我们可以灵活地调整和修改表格结构。

## 3. 数据库迁移方法

Flask-Migrate 提供了一套便捷的数据库迁移方法，通过命令行工具或 Flask 的命令行脚本来执行。下面是 Flask-Migrate 迁移方法的详细说明：

### 3.1 初始化迁移环境

在第一次使用 Flask-Migrate 之前，需要初始化迁移环境，执行以下命令：

```bash
flask db init
```

该命令会在项目根目录下创建一个名为 `migrations` 的文件夹，用于存放迁移脚本和版本控制。

### 3.2 创建或更新迁移脚本

每当我们修改了模型类的定义，需要创建或更新迁移脚本来映射这些变化。执行以下命令：

```bash
flask db migrate -m "创建或者更新数据表"
```

该命令会根据模型类的变化生成一个新的迁移脚本，并记录在 `migrations` 文件夹中。

### 3.3 执行数据库迁移

一旦我们生成了迁移脚本，可以执行数据库迁移操作，应用这些变化到实际的数据库中。执行以下命令：

```bash
flask db upgrade
flask --app app.py db init    #--app 选项并指定应用程序名称
```

该命令会运行迁移脚本，修改数据库结构，使其与模型类的定义保持一致。

### 3.4 回滚迁移

在特殊情况下，可能需要回滚已经执行的迁移脚本。首先，可以通过以下命令查看迁移版本历史：

```bash
flask db history
```

然后，可以选择回滚到指定的版本，或者回滚到上一个版本：

```bash
flask db downgrade  # 回滚到上一个版本
flask db downgrade <版本号>  # 回滚到指定版本
```

注意：回滚迁移可能会丢失已有数据，请谨慎操作。

### 3.5 删除内容和版本记录

场景一:连接mysql时，直接删除migrations和将models文件内容进行修改，重新运行创建即可
场景二:连接sqlite3时，需要将sqlite.db文件和migrations一起删除，重新运行创建即可
注意：删除已有数据，请谨慎操作。

## 4. migrations 文件夹内容介绍

在使用 Flask-Migrate 进行迁移操作后，会在项目根目录下的 `migrations` 文件夹中生成一些文件和文件夹。这里简要介绍一下主要的文件：
![image.png](https://cdn.nlark.com/yuque/0/2023/png/38423761/1689326256560-dddf0a60-eb20-4832-8d83-baeb98a6243e.png#averageHue=%23373e42&clientId=uf644f6db-9401-4&from=paste&height=168&id=u6c4910ac&originHeight=168&originWidth=351&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9789&status=done&style=none&taskId=uaac8283f-50ff-4e2f-a3d4-bae74ee7238&title=&width=351)

- `alembic.ini`：用于配置 Alembic，Flask-Migrate 的底层工具。
- `env.py`：Alembic 的环境脚本，包含数据库连接等相关配置。
- `versions` 文件夹：存储着每个迁移版本的具体实现。

在 `versions` 文件夹中，每个迁移版本都以时间戳命名，并包含一个包含迁移操作的 Python 脚本。这些脚本是自动生成的，可以使用文本编辑器打开查看其具体内容。每个迁移脚本包含了数据库表格的创建、修改或删除等操作。

## 总结

本文介绍了如何使用 Flask-Migrate 迁移 ORM 模型，包括安装和配置、创建模型类、数据库迁移方法以及 migrations 文件夹内容介绍。通过 Flask-Migrate，我们可以轻松管理和迁移数据库，方便地更新和调整表格结构。
{% endraw %}