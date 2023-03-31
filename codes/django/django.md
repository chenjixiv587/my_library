## 如何使用django框架开发网页
- 安装 django 
- 创建项目 
- 创建应用
- 设计表
- 数据迁移
  - `py manage.py makemigrations`
  - `py manage.py migrate`
- 创建一个管理模型的页面
- 创建 views templates urls
- 理解 django 的接受与发出 

django 使用的是  **MTV (Model-Template-View)**  形式。

- Model – Defines the logical data structure and is the data handler between the database and 
the View. 定义数据,沟通数据库与路由
- Template – Is the presentation layer. Django uses a plain-text template system that keeps 
everything that the browser renders. 模板文件主要做展示
- View – Communicates with the database via the Model and transfers the data to the Template 
for viewing. 主要是 起路由作用, 展示模板 view → template

## how django solves the request and give the response
This is how Django handles HTTP requests and generates responses:
    
    
>    1. A web browser requests a page by its URL and the web server passes the HTTP request to Django.
    
    
>    2. Django runs through its configured URL patterns and stops at the first one that matches the 
    requested URL.
    
    
>    3. Django executes the view that corresponds to the matched URL pattern.
    
    
>    4. The view potentially uses data models to retrieve information from the database.
    
    
>    5. Data models provide the data definition and behaviors. They are used to query the database.
    
    
>    6. The view renders a template (usually HTML) to display the data and returns it with an HTTP 
    response



Slug 是一个报纸术语, 其实就相当于是一种标签，`django` 以前是为开发新闻网站而生的，这可能是slug的由来，他对应的 `field` 是 `models.SlugField(max_length=50, **options)`,`max_length` 如果不指定的话，默认就是 50，
`slug` 是一个简短的标签，只包含字母、数字、下划线或连字符。它们一般用于 URL 中。 主要是为了简化链接，有利于 SEO 。

在 模型里 定义 `def __str__(self):
        return self.title` 是为了这样表现对象。


`models.xxField()` 对应 `SQL` 字段类型

-  `models.CharField()` 在`SQL`中对应`VARCHAR`字段类型
-  `models.SlugField()` 在`SQL`中对应`VARCHAR`字段类型
-  `models.TextField()` 在`SQL`中对应字段 `TEXT` 字段类型
-  `models.DateTimeField()` 在`SQL`中对应的字段`DATETIME`字段类型 `DateTimeField(auto_now=False, auto_now_add=False, **options)` `auto_now_add`表示添加一个对象时，日期会自动保存，`auto_now` 表示是当保存一个对象的时候，日期会自动更新。



![owIU6.png](https://c.1ovv.com/2023/03/31/owIU6.png)

在 python3 中 所有的字符串都被当做是  `Unicode`码


在 many-to-one 中 many 与 one有联系的那个字段作为外键 


在 model 中 可以自己设置属性 的 `primary_key = True` 来指定这个属性是 主键， 从而覆盖掉系统的设置


数据从模型到数据库 
- `py manage.py makemigrations`
- `py manage.py migrate`
- 对模型进行增加删除改动的话 都必须重新执行以上的命令。


创建超级用户
- `py manage.py createsuperuser`






