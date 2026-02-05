# 后端项目实战：Flask REST API

本项目将通过构建一个完整的 REST API，帮助你掌握后端开发的核心技能。

## 项目概述

我们将构建一个**图书管理 API**，实现以下功能：
- ✅ 创建图书（POST）
- ✅ 获取所有图书（GET）
- ✅ 获取单本图书（GET）
- ✅ 更新图书（PUT）
- ✅ 删除图书（DELETE）
- ✅ 数据验证
- ✅ 错误处理
- ✅ API 文档

## 技术栈

- **Flask** - Python Web 框架
- **SQLite** - 轻量级数据库
- **SQLAlchemy** - ORM 框架
- **Flask-RESTful** - REST API 扩展
- **Flask-CORS** - 跨域支持

## 项目结构

```
book-api/
├── app.py              # 主应用文件
├── models.py           # 数据模型
├── requirements.txt    # 依赖列表
└── database.db         # SQLite 数据库（自动生成）
```

## 第一步：环境准备

### 1. 安装依赖

创建 `requirements.txt`：

```txt
Flask==3.0.0
Flask-RESTful==0.3.10
Flask-CORS==4.0.0
Flask-SQLAlchemy==3.1.1
marshmallow==3.20.1
```

安装依赖：

```bash
pip install -r requirements.txt
```

### 2. 创建数据库模型

创建 `models.py`：

```python
from flask_sqlalchemy import SQLAlchemy
from datetime import datetime

db = SQLAlchemy()

class Book(db.Model):
    """图书模型"""
    __tablename__ = 'books'

    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100), nullable=False)
    author = db.Column(db.String(50), nullable=False)
    isbn = db.Column(db.String(20), unique=True, nullable=False)
    price = db.Column(db.Float, nullable=False)
    stock = db.Column(db.Integer, default=0)
    description = db.Column(db.Text)
    created_at = db.Column(db.DateTime, default=datetime.utcnow)
    updated_at = db.Column(db.DateTime, default=datetime.utcnow, onupdate=datetime.utcnow)

    def to_dict(self):
        """转换为字典"""
        return {
            'id': self.id,
            'title': self.title,
            'author': self.author,
            'isbn': self.isbn,
            'price': self.price,
            'stock': self.stock,
            'description': self.description,
            'created_at': self.created_at.isoformat(),
            'updated_at': self.updated_at.isoformat()
        }

    def __repr__(self):
        return f'<Book {self.title}>'
```

## 第二步：创建 REST API

创建 `app.py`：

```python
from flask import Flask, request, jsonify
from flask_restful import Api, Resource
from flask_cors import CORS
from models import db, Book
from datetime import datetime

# 创建 Flask 应用
app = Flask(__name__)

# 配置
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///book_api.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

# 初始化扩展
db.init_app(app)
api = Api(app)
CORS(app)  # 允许跨域请求

# 创建数据库表
with app.app_context():
    db.create_all()

# 数据验证函数
def validate_book_data(data, required=True):
    """验证图书数据"""
    errors = {}

    if required:
        if not data.get('title'):
            errors['title'] = '书名不能为空'
        if not data.get('author'):
            errors['author'] = '作者不能为空'
        if not data.get('isbn'):
            errors['isbn'] = 'ISBN不能为空'
        if not data.get('price'):
            errors['price'] = '价格不能为空'

    # 验证价格
    if data.get('price') and float(data.get('price', 0)) <= 0:
        errors['price'] = '价格必须大于0'

    # 验证库存
    if data.get('stock') and int(data.get('stock', 0)) < 0:
        errors['stock'] = '库存不能为负数'

    # 验证 ISBN 格式（简单验证）
    if data.get('isbn') and len(data['isbn']) not in [10, 13]:
        errors['isbn'] = 'ISBN格式不正确'

    return errors

# 资源类：图书列表
class BookList(Resource):
    def get(self):
        """获取所有图书"""
        # 支持查询参数
        page = request.args.get('page', 1, type=int)
        per_page = request.args.get('per_page', 10, type=int)
        search = request.args.get('search', '')

        # 搜索查询
        query = Book.query
        if search:
            query = query.filter(
                db.or_(
                    Book.title.like(f'%{search}%'),
                    Book.author.like(f'%{search}%')
                )
            )

        # 分页
        pagination = query.paginate(page=page, per_page=per_page, error_out=False)

        return {
            'books': [book.to_dict() for book in pagination.items],
            'total': pagination.total,
            'pages': pagination.pages,
            'current_page': page
        }

    def post(self):
        """创建新图书"""
        data = request.get_json()

        # 验证数据
        errors = validate_book_data(data)
        if errors:
            return {'errors': errors}, 400

        # 检查 ISBN 是否已存在
        if Book.query.filter_by(isbn=data['isbn']).first():
            return {'error': '该ISBN已存在'}, 400

        # 创建图书
        try:
            book = Book(
                title=data['title'],
                author=data['author'],
                isbn=data['isbn'],
                price=float(data['price']),
                stock=int(data.get('stock', 0)),
                description=data.get('description', '')
            )
            db.session.add(book)
            db.session.commit()

            return {
                'message': '图书创建成功',
                'book': book.to_dict()
            }, 201

        except Exception as e:
            db.session.rollback()
            return {'error': f'创建失败: {str(e)}'}, 500

# 资源类：单本图书
class BookResource(Resource):
    def get(self, book_id):
        """获取单本图书"""
        book = Book.query.get(book_id)
        if not book:
            return {'error': '图书不存在'}, 404

        return {'book': book.to_dict()}

    def put(self, book_id):
        """更新图书"""
        book = Book.query.get(book_id)
        if not book:
            return {'error': '图书不存在'}, 404

        data = request.get_json()

        # 验证数据
        errors = validate_book_data(data, required=False)
        if errors:
            return {'errors': errors}, 400

        # 检查 ISBN 重复
        if data.get('isbn') and data['isbn'] != book.isbn:
            if Book.query.filter_by(isbn=data['isbn']).first():
                return {'error': '该ISBN已存在'}, 400

        # 更新图书
        try:
            if 'title' in data:
                book.title = data['title']
            if 'author' in data:
                book.author = data['author']
            if 'isbn' in data:
                book.isbn = data['isbn']
            if 'price' in data:
                book.price = float(data['price'])
            if 'stock' in data:
                book.stock = int(data['stock'])
            if 'description' in data:
                book.description = data['description']

            book.updated_at = datetime.utcnow()
            db.session.commit()

            return {
                'message': '图书更新成功',
                'book': book.to_dict()
            }

        except Exception as e:
            db.session.rollback()
            return {'error': f'更新失败: {str(e)}'}, 500

    def delete(self, book_id):
        """删除图书"""
        book = Book.query.get(book_id)
        if not book:
            return {'error': '图书不存在'}, 404

        try:
            db.session.delete(book)
            db.session.commit()

            return {'message': '图书删除成功'}, 200

        except Exception as e:
            db.session.rollback()
            return {'error': f'删除失败: {str(e)}'}, 500

# 注册路由
api.add_resource(BookList, '/api/books')
api.add_resource(BookResource, '/api/books/<int:book_id>')

# 首页
@app.route('/')
def index():
    return {
        'message': '欢迎使用图书管理 API',
        'version': '1.0.0',
        'endpoints': {
            'GET /api/books': '获取所有图书',
            'POST /api/books': '创建新图书',
            'GET /api/books/<id>': '获取单本图书',
            'PUT /api/books/<id>': '更新图书',
            'DELETE /api/books/<id>': '删除图书'
        }
    }

# 错误处理
@app.errorhandler(404)
def not_found(error):
    return jsonify({'error': '请求的资源不存在'}), 404

@app.errorhandler(500)
def internal_error(error):
    return jsonify({'error': '服务器内部错误'}), 500

if __name__ == '__main__':
    app.run(debug=True, port=5000)
```

## 第三步：运行项目

```bash
# 启动服务器
python app.py
```

访问 http://localhost:5000 查看 API 信息。

## API 使用示例

### 1. 创建图书

**请求：**
```bash
POST /api/books
Content-Type: application/json

{
    "title": "Python编程：从入门到实践",
    "author": "Eric Matthes",
    "isbn": "9781593276034",
    "price": 89.00,
    "stock": 50,
    "description": "一本优秀的Python入门书籍"
}
```

**响应：**
```json
{
    "message": "图书创建成功",
    "book": {
        "id": 1,
        "title": "Python编程：从入门到实践",
        "author": "Eric Matthes",
        "isbn": "9781593276034",
        "price": 89.0,
        "stock": 50,
        "description": "一本优秀的Python入门书籍",
        "created_at": "2024-01-15T10:30:00",
        "updated_at": "2024-01-15T10:30:00"
    }
}
```

### 2. 获取所有图书

**请求：**
```bash
GET /api/books?page=1&per_page=10&search=Python
```

**响应：**
```json
{
    "books": [...],
    "total": 25,
    "pages": 3,
    "current_page": 1
}
```

### 3. 获取单本图书

**请求：**
```bash
GET /api/books/1
```

### 4. 更新图书

**请求：**
```bash
PUT /api/books/1
Content-Type: application/json

{
    "price": 79.00,
    "stock": 45
}
```

### 5. 删除图书

**请求：**
```bash
DELETE /api/books/1
```

## 使用 cURL 测试 API

```bash
# 创建图书
curl -X POST http://localhost:5000/api/books \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Flask Web开发",
    "author": "Miguel Grinberg",
    "isbn": "9781491991732",
    "price": 99.00,
    "stock": 30
  }'

# 获取所有图书
curl http://localhost:5000/api/books

# 获取单本图书
curl http://localhost:5000/api/books/1

# 更新图书
curl -X PUT http://localhost:5000/api/books/1 \
  -H "Content-Type: application/json" \
  -d '{"price": 89.00}'

# 删除图书
curl -X DELETE http://localhost:5000/api/books/1
```

## 核心概念讲解

### 1. RESTful API 设计

RESTful API 遵循以下原则：
- 使用 HTTP 动词（GET、POST、PUT、DELETE）
- 资源通过 URL 标识
- 无状态通信
- 使用 JSON 格式传输数据

### 2. ORM（对象关系映射）

使用 SQLAlchemy 将数据库表映射为 Python 类：

```python
class Book(db.Model):
    """图书模型"""
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100), nullable=False)
    # ...
```

### 3. 数据验证

在处理用户输入时必须验证：

```python
def validate_book_data(data):
    errors = {}
    if not data.get('title'):
        errors['title'] = '书名不能为空'
    # ...
    return errors
```

### 4. 错误处理

统一的错误响应格式：

```python
@app.errorhandler(404)
def not_found(error):
    return jsonify({'error': '请求的资源不存在'}), 404
```

## 进阶功能

### 1. 添加用户认证

```python
from flask_httpauth import HTTPBasicAuth

auth = HTTPBasicAuth()

@auth.verify_password
def verify_password(username, password):
    # 验证用户名和密码
    user = User.query.filter_by(username=username).first()
    return user and user.check_password(password)

@auth.login_required
class BookResource(Resource):
    def get(self, book_id):
        # ...
```

### 2. 添加日志记录

```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@app.route('/api/books', methods=['POST'])
def create_book():
    logger.info('Creating new book')
    # ...
```

### 3. 添加缓存

```python
from flask_caching import Cache

cache = Cache(app, config={'CACHE_TYPE': 'simple'})

@app.route('/api/books/<int:book_id>')
@cache.cached(timeout=60)
def get_book(book_id):
    # ...
```

### 4. 添加单元测试

```python
import unittest
from app import app

class BookAPITestCase(unittest.TestCase):
    def setUp(self):
        self.app = app.test_client()
        # 创建测试数据库

    def test_create_book(self):
        response = self.app.post('/api/books',
            json={'title': 'Test Book', ...})
        self.assertEqual(response.status_code, 201)
```

## 部署到生产环境

### 使用 Gunicorn

```bash
# 安装 Gunicorn
pip install gunicorn

# 启动服务
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

### 使用 Docker

创建 `Dockerfile`：

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "app:app"]
```

构建并运行：

```bash
docker build -t book-api .
docker run -p 5000:5000 book-api
```

## 学习资源

- [Flask 官方文档](https://flask.palletsprojects.com/)
- [RESTful API 设计指南](https://restfulapi.net/)
- [SQLAlchemy 文档](https://docs.sqlalchemy.org/)

## 下一步学习

完成本项目后，你可以：

1. **学习数据库设计** - 索引优化、事务处理
2. **学习异步编程** - FastAPI、asyncio
3. **学习微服务** - Docker、Kubernetes
4. **学习消息队列** - Redis、RabbitMQ
5. **学习 API 网关** - Nginx、Kong

祝学习愉快！🚀
