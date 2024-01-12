---
ifupdate: false
layout: post
title: Flask 连接 mysql 基本操作
subtitle: falsk_数据库相关操作
date: 2022-04-17
author: Carlos
header-img: img/bg-cook.jpg
catalog: true
tags:
 - Flask
---
{% raw %}# Flask 连接数据库基本操作

## 1. 数据库连接

在 Flask 中连接数据库是一项常见任务。我们可以使用 SQLAlchemy 扩展来连接 MySQL 数据库。下面是一个连接 MySQL 数据库的示例代码：

```
import pymysql
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)

# 公共方法连接数据库
def connect_flask_mysql(app, username="root", password="123456", host='127.0.0.1', port=3306, db='flask_study'):
    app.config['SQLALCHEMY_DATABASE_URI'] = f'mysql+pymysql://{username}:{password}@{host}:{port}/{db}?charset=utf8'
    app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
    db = SQLAlchemy(app)
    return db

# 连接 MySQL 数据库
db = connect_flask_mysql(app)  # 将数据库连接对象保存为 db
```

## 2. 创建数据表单

在 Flask 中，我们可以使用 SQLAlchemy 来创建数据表单。下面是一个创建书籍信息数据表的示例代码：

```
class Book(db.Model):
    __tablename__ = 'books'

    id = db.Column(db.Integer, primary_key=True)
    category = db.Column(db.String(100), nullable=False)
    title = db.Column(db.String(100), nullable=False)
    price = db.Column(db.Float, nullable=False)
    region = db.Column(db.String(100), nullable=False)

    def __repr__(self):
        return f"<Book {self.title}>"

# 创建数据库和表
with app.app_context():
    db.create_all()
```

## 3. 添加书籍信息

Flask 提供了路由函数来处理不同的 URL 请求。下面是一个将书籍信息添加到数据库的示例代码：

```
@app.route('/create_book')
def create_book():
    import random

    categories = ['科幻', '小说', '历史', '教育']  # 图书分类列表
    titles=['三体','三国演义','双人成行','未成年早期教育']
    regions=['A01','Z03','h22','l99']
    new_book = Book(
        category=random.choice(categories),
        title=random.choice(titles),
        price=random.uniform(10.0, 100.0),
        region=random.choice(regions)
    )
    db.session.add(new_book)
    db.session.commit()
    return f"Book created successfully! {new_book.title}"
```

## 4. 查询书籍信息

我们可以使用 SQLAlchemy 的查询功能来从数据库中获取书籍信息。下面是一个查询所有书籍信息并显示在网页上的示例代码：

```
@app.route('/')
def get_books():
    books = Book.query.all()
    return render_template('books_manage.html', books=books)
```

## 5. 更新书籍信息

我们可以使用路由函数来处理更新书籍信息的请求。下面是一个将书籍标题更新为 "New Title" 的示例代码：

```
@app.route('/update_book/<int:book_id>')
def update_book(book_id):
    book = Book.query.get(book_id)
    if book:
        book.title = "New Title"
        db.session.commit()
        return f"Book {book_id} updated successfully!"
    else:
        return f"Book {book_id} not found."
```

## 6. 删除书籍信息

类似于更新书籍信息，我们可以使用路由函数来处理删除书籍的请求。下面是一个删除书籍信息的示例代码：

```
@app.route('/delete_book/<int:book_id>')
def delete_book(book_id):
    book = Book.query.get(book_id)
    if book:
        db.session.delete(book)
        db.session.commit()
        return f"Book {book_id} deleted successfully!"
    else:
        return f"Book {book_id} not found."
```

## 7. 模板渲染

Flask 使用 Jinja2 模板引擎来渲染网页模板。下面是一个简单的图书列表网页模板示例：

```
<!DOCTYPE html>
<html>
<head>
    <title>图书管理系统</title>
    <style>
        table {
            border-collapse: collapse;
            width: 100%;
        }

        th, td {
            padding: 8px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }

        tr:hover {background-color:#f5f5f5;}

        .button-container {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>图书管理系统</h1>

    <!-- 创建图书表单 -->
    <form action="/create_book" method="get">
        <input type="submit" value="创建图书">
    </form>

    <!-- 图书列表 -->
    <h2>图书列表</h2>
    <table>
        <tr>
            <th>分类</th>
            <th>书名</th>
            <th>价格</th>
            <th>区域</th>
            <th>操作</th>
        </tr>
        {% for book in books %}
            <tr>
                <td>{{ book.category }}</td>
                <td>{{ book.title }}</td>
                <td>{{ book.price }}</td>
                <td>{{ book.region }}</td>
                <td>
                    <a href="/update_book/{{ book.id }}">编辑</a>
                    <a href="/delete_book/{{ book.id }}" onclick="return confirmDelete()">删除</a>
                </td>
            </tr>
        {% endfor %}
    </table>

    <script>
        function confirmDelete() {
            return confirm("确定删除该图书吗？");
        }
    </script>
</body>
</html>
```

## 8. 效果图

![](https://cdn.nlark.com/yuque/0/2023/png/38423761/1689237872148-b3e09e4a-592b-41cb-9ac3-239d8dd3c5fc.png#averageHue=%23fdfcfc&clientId=u90da3bc2-19dd-4&from=paste&height=504&id=u74952481&originHeight=504&originWidth=1764&originalType=binary&ratio=1&rotation=0&showTitle=false&size=35043&status=done&style=none&taskId=ud1a347f9-8f48-4955-8b6f-b70ffad5783&title=&width=1764)

以上是关于 Flask 基本操作的示例代码和效果图，希望对你的学习有所帮助！
{% endraw %}