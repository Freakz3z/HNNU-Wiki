# Python 入门指南

## 为什么选择 Python？

Python 是最适合编程初学者的语言，原因如下：

1. **语法简洁** - 接近英语，易于理解
2. **应用广泛** - 数据分析、AI、Web开发、自动化等
3. **生态丰富** - 海量的第三方库
4. **学习资源多** - 免费教程和社区支持

## 第一步：安装 Python

### Windows
1. 访问 [Python官网](https://www.python.org/downloads/)
2. 下载最新版安装包（3.10或更高版本）
3. **重要**：安装时勾选 "Add Python to PATH"
4. 验证安装：打开命令行输入 `python --version`

### macOS
```bash
# 推荐使用 Homebrew 安装
brew install python3

# 验证安装
python3 --version
```

### Linux
```bash
# 通常系统已自带，或使用包管理器安装
sudo apt install python3  # Ubuntu/Debian
sudo yum install python3   # CentOS/RHEL
```

## 第二步：选择开发工具

### 推荐使用 VS Code

1. [下载 VS Code](https://code.visualstudio.com/)
2. 安装 Python 扩展
   - 打开 VS Code
   - 点击左侧扩展图标（或按 `Ctrl+Shift+X`）
   - 搜索 "Python" 并安装 Microsoft 的 Python 扩展

### 其他选择
- **PyCharm Community**（免费，功能强大）
- **Jupyter Notebook**（适合数据分析和学习）
- **Thonny**（专为初学者设计）

## 第三步：Python 基础语法

### 1. Hello World

```python
# 这是你第一个程序
print("Hello, World!")
```

### 2. 变量和数据类型

```python
# 变量赋值（不需要声明类型）
name = "张三"        # 字符串
age = 20            # 整数
height = 1.75       # 浮点数
is_student = True   # 布尔值

# 打印变量
print(f"我叫{name}，今年{age}岁")
```

### 3. 基本运算

```python
# 算术运算
a = 10
b = 3

print(a + b)   # 13 加法
print(a - b)   # 7  减法
print(a * b)   # 30 乘法
print(a / b)   # 3.333... 除法
print(a // b)  # 3  整除
print(a % b)   # 1  取余
print(a ** b)  # 1000 幂运算

# 字符串拼接
greeting = "你好"
name = "小明"
message = greeting + "，" + name
print(message)  # 输出：你好，小明
```

### 4. 列表（List）

```python
# 创建列表
fruits = ["苹果", "香蕉", "橙子"]

# 访问元素（索引从0开始）
print(fruits[0])  # 输出：苹果

# 添加元素
fruits.append("葡萄")

# 删除元素
fruits.remove("香蕉")

# 切片
print(fruits[1:3])  # 输出第2到第3个元素

# 遍历列表
for fruit in fruits:
    print(fruit)
```

### 5. 条件语句

```python
age = 18

if age >= 18:
    print("你已经成年")
elif age >= 13:
    print("你是青少年")
else:
    print("你是儿童")

# 布尔运算
score = 85
if score >= 60 and score < 70:
    print("及格")
elif score >= 70 and score < 90:
    print("良好")
elif score >= 90:
    print("优秀")
```

### 6. 循环

```python
# for 循环
for i in range(5):  # 0, 1, 2, 3, 4
    print(f"第{i+1}次循环")

# while 循环
count = 0
while count < 3:
    print("计数:", count)
    count += 1

# 遍历字典
person = {"name": "小明", "age": 20}
for key, value in person.items():
    print(f"{key}: {value}")
```

### 7. 函数

```python
# 定义函数
def greet(name):
    return f"你好，{name}！"

# 调用函数
message = greet("小红")
print(message)

# 带默认参数的函数
def introduce(name, age=18):
    print(f"我叫{name}，今年{age}岁")

introduce("小李")        # 使用默认年龄
introduce("小王", 25)    # 指定年龄

# Lambda 函数（匿名函数）
multiply = lambda x, y: x * y
print(multiply(3, 4))  # 输出：12
```

### 8. 字典（Dictionary）

```python
# 创建字典
student = {
    "name": "小明",
    "age": 20,
    "major": "计算机科学"
}

# 访问值
print(student["name"])          # 输出：小明
print(student.get("age"))       # 输出：20

# 添加/修改键值对
student["grade"] = "大二"       # 添加
student["age"] = 21             # 修改

# 删除键值对
del student["major"]

# 检查键是否存在
if "name" in student:
    print("存在name键")
```

## 第四步：实用项目练习

### 项目1：猜数字游戏

```python
import random

def guess_number_game():
    number = random.randint(1, 100)
    attempts = 0

    print("欢迎来到猜数字游戏！")
    print("我想了一个1到100之间的数字，你来猜猜看。")

    while True:
        guess = int(input("请输入你的猜测: "))
        attempts += 1

        if guess < number:
            print("太小了，再大一点！")
        elif guess > number:
            print("太大了，再小一点！")
        else:
            print(f"恭喜你猜对了！用了{attempts}次尝试。")
            break

# 运行游戏
guess_number_game()
```

### 项目2：待办事项列表

```python
def todo_list():
    tasks = []

    while True:
        print("\n=== 待办事项列表 ===")
        print("1. 添加任务")
        print("2. 查看任务")
        print("3. 删除任务")
        print("4. 退出")

        choice = input("请选择操作 (1-4): ")

        if choice == "1":
            task = input("请输入任务: ")
            tasks.append(task)
            print("任务添加成功！")
        elif choice == "2":
            if not tasks:
                print("暂无任务")
            else:
                print("\n任务列表：")
                for i, task in enumerate(tasks, 1):
                    print(f"{i}. {task}")
        elif choice == "3":
            if not tasks:
                print("暂无任务")
            else:
                for i, task in enumerate(tasks, 1):
                    print(f"{i}. {task}")
                index = int(input("请输入要删除的任务编号: ")) - 1
                if 0 <= index < len(tasks):
                    removed = tasks.pop(index)
                    print(f"已删除任务：{removed}")
        elif choice == "4":
            print("再见！")
            break
        else:
            print("无效输入，请重试")

# 运行程序
todo_list()
```

### 项目3：简单计算器

```python
def calculator():
    print("简单计算器")
    print("支持：+ - * /")

    while True:
        try:
            num1 = float(input("请输入第一个数字: "))
            operator = input("请输入运算符 (+, -, *, /): ")
            num2 = float(input("请输入第二个数字: "))

            if operator == "+":
                result = num1 + num2
            elif operator == "-":
                result = num1 - num2
            elif operator == "*":
                result = num1 * num2
            elif operator == "/":
                if num2 == 0:
                    print("错误：除数不能为零")
                    continue
                result = num1 / num2
            else:
                print("无效的运算符")
                continue

            print(f"结果: {num1} {operator} {num2} = {result}")

        except ValueError:
            print("错误：请输入有效的数字")

        another = input("\n是否继续计算? (y/n): ")
        if another.lower() != 'y':
            print("再见！")
            break

# 运行计算器
calculator()
```

## 第五步：常用库推荐

### 数据处理
```bash
pip install pandas numpy
```

### Web开发
```bash
pip install flask django
```

### 数据可视化
```bash
pip install matplotlib seaborn
```

### 网络爬虫
```bash
pip install requests beautifulsoup4
```

## 学习建议

1. **多动手实践** - 不要只看书，多写代码
2. **从简单项目开始** - 完成小项目建立信心
3. **学会查文档** - 遇到问题先查官方文档
4. **参与社区** - 加入Python学习群，与他人交流
5. **保持耐心** - 编程需要时间积累，不要急于求成

## 常见问题

### Q1: Python 2 和 Python 3 有什么区别？
**A**: Python 2 已于2020年停止维护，新手直接学习 Python 3 即可。

### Q2: 遇到报错怎么办？
**A**:
1. 仔细阅读错误信息
2. 复制错误信息到搜索引擎
3. 检查代码的语法和逻辑
4. 使用 print() 调试

### Q3: 如何提升编程能力？
**A**:
1. 坚持每天写代码
2. 做项目练习
3. 阅读优秀代码
4. 学习算法和数据结构

## 下一步学习

完成入门后，你可以：

1. **深入Python** - 学习面向对象编程、装饰器、生成器等
2. **选择方向** - Web开发、数据分析、AI、自动化等
3. **做项目** - 个人博客、爬虫、数据分析项目等
4. **学习其他语言** - JavaScript、C++、Go等

## 免费学习资源

- [Python官方教程](https://docs.python.org/zh-cn/3/tutorial/)
- [廖雪峰Python教程](https://www.liaoxuefeng.com/wiki/1016959663602400)
- [菜鸟教程Python](https://www.runoob.com/python3/python3-tutorial.html)
- [B站黑马程序员Python教程](https://www.bilibili.com/video/BV1q54y1s75o)

祝你学习愉快！🐍
