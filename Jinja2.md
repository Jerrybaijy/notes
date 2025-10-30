---
title: python
author: Jerry.Baijy
tags:
  - 应用科学
  - it
  - code-language
  - backend
  - python
  - flask
---

# Jinja2

**Jinja2** 是一个流行的 Python 模板引擎，主要用于将数据传递到 HTML、XML 或其他标记语言中，从而生成动态内容。它通常用于 Web 框架中，比如 Flask 和 Django（Django 使用的是自己的模板引擎，但与 Jinja2 类似）。

**Jinja2 的核心特性**：

- **变量替换**：使用 `{{ ... }}` 输出变量值。
- **控制结构**：支持循环、条件语句等逻辑控制结构。
- **过滤器**：对变量进行操作，比如格式化、转换等。
- **宏与模板继承**：可以创建可重用的模板块和继承模板。
- **上下文操作**：可以传递数据到模板，并在模板中动态处理。

# 变量

- **语法**：`{{ VARIABLE_NAME }}`

  ```jinja2
  <p>Welcome, {{ username }}!</p>
  ```

# 控制结构

- **条件语句**

  ```jinja2
  {% if user.is_admin %}
    Welcome, Admin!
  {% else %}
    Welcome, User!
  {% endif %}
  ```

- **循环语句**

  ```jinja2
  <ul>
    {% for item in items %}
      <li>{{ item }}</li>
    {% endfor %}
  </ul>
  ```

# 过滤器

**语法**

```jinja2
{{ "hello world" | capitalize }}  # Hello world
```

# 模板继承

**模板继承**允许创建一个基础模板（也称为 “父模板”），其中包含网站的通用布局，如头部、导航栏和底部。然后，可以创建多个子模板，这些子模板继承自父模板，并可以重写或扩展父模板中的特定块。

在父模板 `base.html` 中可以定义这样的结构：

```jinja2
<html>
  <head>
    <title>{% block title %}{% endblock %}</title>
  </head>

  <body>
    <header>
      <h1>My Website</h1>
    </header>
    <nav>
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
      </ul>
    </nav>
    <main>{% block content %}{% endblock %}</main>
    <footer>&copy; 2024 My Company</footer>
  </body>
</html>
```

在子模板 `home.html` 中，可以继承 `base.html` 并填充 `title` 和 `content` 块：

```jinja2
{% extends "base.html" %}
{% block title %}Home Page{% endblock %}
{% block content %}
  <p>Welcome to the home page!</p>
{% endblock %}
```

# 动态路径 `url_for`

`url_for()` 函数是 Flask 框架中定义 URL 的方式，用于生成 URL（统一资源定位符），主要的优势在于它能够根据定义的路由视图函数名动态地构建 URL，而不是在代码中硬编码 URL 字符串。这样做的好处是，如果路由规则发生变化（例如，路由路径被修改或者添加了新的参数），`url_for` 函数调用的地方不需要手动修改 URL，从而提高了代码的可维护性。

# Flask 示例

- `app.py`

  ```python
  from flask import Flask, render_template
  
  app = Flask(__name__)
  
  @app.route("/")
  def index():
      return render_template("index.html", name="Alice", items=["Apple", "Banana", "Cherry"])
  
  if __name__ == "__main__":
      app.run(debug=True)
  ```

- `templates/index.html`

  ```html
  <body>
    <h1>Hello, {{ name }}!</h1>
    <ul>
      {% for item in items %}
      <li>{{ item }}</li>
      {% endfor %}
    </ul>
  </body>
  ```
