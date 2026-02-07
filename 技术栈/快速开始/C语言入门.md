# C/C++ 入门指南

## 为什么选择 C/C++？

由于培养方案的改变，现在大一新生首先接触的编程语言为 Python。但是笔者强烈建议掌握 C/C++，这样可以方便之后的各种学习，因此这篇文章主要介绍 C/C++。

**C/C++ 的优势：**
1. **底层理解** - 帮助理解计算机内存管理和系统运行原理
2. **性能卓越** - 执行效率高，适合系统编程和竞赛
3. **基础重要** - 许多现代语言（如 Java、Go）都受 C/C++ 影响
4. **竞赛必备** - NOI、ACM 等算法竞赛的主要语言
5. **就业需求** - 嵌入式、游戏开发、系统编程等领域广泛使用

## 第一步：安装开发环境

### Windows

#### 方式一：安装 MinGW-w64
1. 访问 [MinGW-w64 下载页](https://www.mingw-w64.org/)
2. 或使用 MSYS2 安装：
   ```bash
   # 下载 MSYS2 后，在 MSYS2 终端执行
   pacman -S mingw-w64-x86_64-gcc
   ```
3. 将 bin 目录添加到系统 PATH
4. 验证安装：打开命令行输入 `gcc --version`

#### 方式二：安装 Visual Studio
1. 下载 [Visual Studio Community](https://visualstudio.microsoft.com/downloads/)（免费）
2. 安装时选择"使用 C++ 的桌面开发"工作负载
3. 包含了完整的编译器和调试工具

#### 方式三：Dev-C++（推荐：适合初学者）
[Dev-C++ 下载](https://sourceforge.net/projects/orwelldevcpp/)
> Dev C++ 是一款免费开源的 C/C++ IDE，内嵌 GCC 编译器，是 NOI、NOIP 等比赛的指定工具。优点是体积小、安装简单，缺点是调试功能较弱。

### macOS
```bash
# 安装 Xcode Command Line Tools
xcode-select --install

# 或使用 Homebrew 安装 GCC
brew install gcc

# 验证安装
gcc --version
g++ --version
```

### Linux
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install build-essential gdb

# CentOS/RHEL
sudo yum groupinstall "Development Tools"

# 验证安装
gcc --version
```

## 第二步：选择开发工具

### 推荐使用 VS Code

1. [下载 VS Code](https://code.visualstudio.com/)
2. 安装必要扩展：
   - **C/C++**（Microsoft 官方）
   - **Code Runner**（快速运行代码）
   - **Chinese (Simplified) Language Pack**（中文界面）

### 其他选择

- **Visual Studio**（Windows，功能最强大）
- **CLion**（JetBrains 出品，收费但强大）
- **Code::Blocks**（免费，跨平台）
- **Vim/Emacs + GCC**（适合进阶用户）

## 第三步：C/C++ 基础语法

### 1. Hello World

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

### 2. 变量和数据类型

```c
// C 语言
int age = 20;              // 整数
float height = 1.75f;      // 单精度浮点数
double weight = 65.5;      // 双精度浮点数
char grade = 'A';          // 字符
char name[] = "张三";       // 字符串（C风格）
bool is_student = 1;       // 布尔值（C99，0或1）

// 打印变量
printf("我叫%s，今年%d岁\n", name, age);
```

```cpp
// C++ 语言
int age = 20;              // 整数
float height = 1.75f;      // 单精度浮点数
double weight = 65.5;      // 双精度浮点数
char grade = 'A';          // 字符
string name = "张三";       // 字符串（C++风格）
bool is_student = true;    // 布尔值

// 打印变量（C++方式）
cout << "我叫" << name << "，今年" << age << "岁" << endl;
```

### 3. 基本运算

```c
int a = 10, b = 3;

printf("%d\n", a + b);    // 13 加法
printf("%d\n", a - b);    // 7  减法
printf("%d\n", a * b);    // 30 乘法
printf("%f\n", a / (double)b);  // 3.333... 除法（注意整数除法）
printf("%d\n", a % b);    // 1  取余
```

### 4. 数组（Array）

```c
// 创建数组
int scores[5] = {90, 85, 78, 92, 88};

// 访问元素（索引从0开始）
printf("%d\n", scores[0]);  // 输出：90

// 修改元素
scores[1] = 95;

// 遍历数组
for (int i = 0; i < 5; i++) {
    printf("第%d门课：%d分\n", i + 1, scores[i]);
}

// C++ 的 vector（动态数组）
#include <vector>
vector<int> nums = {1, 2, 3, 4, 5};
nums.push_back(6);  // 添加元素
```

### 5. 条件语句

```c
int age = 18;

if (age >= 18) {
    printf("你已经成年\n");
} else if (age >= 13) {
    printf("你是青少年\n");
} else {
    printf("你是儿童\n");
}

// 布尔运算
int score = 85;
if (score >= 60 && score < 70) {
    printf("及格\n");
} else if (score >= 70 && score < 90) {
    printf("良好\n");
} else if (score >= 90) {
    printf("优秀\n");
}
```

### 6. 循环

```c
// for 循环
for (int i = 0; i < 5; i++) {
    printf("第%d次循环\n", i + 1);
}

// while 循环
int count = 0;
while (count < 3) {
    printf("计数: %d\n", count);
    count++;
}

// do-while 循环（至少执行一次）
int num;
do {
    printf("请输入一个正数: ");
    scanf("%d", &num);
} while (num <= 0);
```

### 7. 函数

```c
// 函数声明
int add(int a, int b);

// 函数定义
int add(int a, int b) {
    return a + b;
}

// 函数调用
int result = add(3, 5);
printf("3 + 5 = %d\n", result);

// 带默认参数的函数（C++特性）
void greet(string name = "朋友") {
    cout << "你好，" << name << "！" << endl;
}

greet();        // 输出：你好，朋友！
greet("小明");  // 输出：你好，小明！
```

### 8. 指针（C/C++ 特色）

```c
int num = 42;
int *ptr = &num;  // ptr 存储 num 的地址

printf("num 的值: %d\n", num);      // 42
printf("num 的地址: %p\n", &num);   // 地址
printf("ptr 指向的值: %d\n", *ptr); // 42

// 通过指针修改值
*ptr = 100;
printf("修改后 num 的值: %d\n", num);  // 100
```

### 9. 结构体（struct）

```c
// 定义结构体
struct Student {
    char name[50];
    int age;
    double score;
};

// 使用结构体
struct Student stu1;
strcpy(stu1.name, "小明");
stu1.age = 20;
stu1.score = 89.5;

printf("姓名: %s, 年龄: %d, 分数: %.1f\n",
       stu1.name, stu1.age, stu1.score);

// C++ 可以简化写法
struct Student2 {
    string name;
    int age;
    double score;
};

Student2 stu2 = {"小红", 19, 92.0};
```

## 第四步：实用项目练习

### 项目1：猜数字游戏

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void guess_number_game() {
    srand(time(NULL));  // 初始化随机数种子
    int number = rand() % 100 + 1;  // 1-100的随机数
    int guess, attempts = 0;

    printf("欢迎来到猜数字游戏！\n");
    printf("我想了一个1到100之间的数字，你来猜猜看。\n");

    while (1) {
        printf("请输入你的猜测: ");
        scanf("%d", &guess);
        attempts++;

        if (guess < number) {
            printf("太小了，再大一点！\n");
        } else if (guess > number) {
            printf("太大了，再小一点！\n");
        } else {
            printf("恭喜你猜对了！用了%d次尝试。\n", attempts);
            break;
        }
    }
}

int main() {
    guess_number_game();
    return 0;
}
```

### 项目2：学生成绩管理系统

```c
#include <stdio.h>

#define MAX_STUDENTS 100

struct Student {
    char name[50];
    int score;
};

int main() {
    struct Student students[MAX_STUDENTS];
    int count = 0;
    int choice;

    while (1) {
        printf("\n=== 学生成绩管理系统 ===\n");
        printf("1. 添加学生\n");
        printf("2. 显示所有学生\n");
        printf("3. 查找最高分\n");
        printf("4. 计算平均分\n");
        printf("5. 退出\n");

        printf("请选择操作 (1-5): ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                if (count < MAX_STUDENTS) {
                    printf("请输入学生姓名: ");
                    scanf("%s", students[count].name);
                    printf("请输入学生成绩: ");
                    scanf("%d", &students[count].score);
                    count++;
                    printf("添加成功！\n");
                } else {
                    printf("学生数量已达上限！\n");
                }
                break;

            case 2:
                if (count == 0) {
                    printf("暂无学生记录\n");
                } else {
                    printf("\n学生列表：\n");
                    for (int i = 0; i < count; i++) {
                        printf("%d. %s: %d分\n", i + 1,
                               students[i].name, students[i].score);
                    }
                }
                break;

            case 3:
                if (count == 0) {
                    printf("暂无学生记录\n");
                } else {
                    int max_index = 0;
                    for (int i = 1; i < count; i++) {
                        if (students[i].score > students[max_index].score) {
                            max_index = i;
                        }
                    }
                    printf("最高分：%s，%d分\n",
                           students[max_index].name, students[max_index].score);
                }
                break;

            case 4:
                if (count == 0) {
                    printf("暂无学生记录\n");
                } else {
                    int sum = 0;
                    for (int i = 0; i < count; i++) {
                        sum += students[i].score;
                    }
                    printf("平均分：%.2f\n", (double)sum / count);
                }
                break;

            case 5:
                printf("再见！\n");
                return 0;

            default:
                printf("无效输入，请重试\n");
        }
    }
}
```

### 项目3：简单计算器

```c
#include <stdio.h>

int main() {
    double num1, num2, result;
    char operator;

    printf("简单计算器\n");
    printf("支持：+ - * / %%\n");

    while (1) {
        printf("请输入第一个数字: ");
        scanf("%lf", &num1);

        printf("请输入运算符 (+, -, *, /, %%): ");
        scanf(" %c", &operator);

        printf("请输入第二个数字: ");
        scanf("%lf", &num2);

        switch (operator) {
            case '+':
                result = num1 + num2;
                printf("结果: %.2lf + %.2lf = %.2lf\n", num1, num2, result);
                break;
            case '-':
                result = num1 - num2;
                printf("结果: %.2lf - %.2lf = %.2lf\n", num1, num2, result);
                break;
            case '*':
                result = num1 * num2;
                printf("结果: %.2lf * %.2lf = %.2lf\n", num1, num2, result);
                break;
            case '/':
                if (num2 == 0) {
                    printf("错误：除数不能为零\n");
                } else {
                    result = num1 / num2;
                    printf("结果: %.2lf / %.2lf = %.2lf\n", num1, num2, result);
                }
                break;
            case '%':
                if (num2 == 0) {
                    printf("错误：除数不能为零\n");
                } else {
                    result = (int)num1 % (int)num2;
                    printf("结果: %.0lf %% %.0lf = %.0lf\n", num1, num2, result);
                }
                break;
            default:
                printf("无效的运算符\n");
        }

        char another;
        printf("\n是否继续计算? (y/n): ");
        scanf(" %c", &another);
        if (another != 'y' && another != 'Y') {
            printf("再见！\n");
            break;
        }
    }

    return 0;
}
```

## 第五步：常用库推荐

### 标准库
C/C++ 拥有强大的标准库，无需额外安装：
- `stdio.h` / `iostream` - 输入输出
- `stdlib.h` - 通用工具函数
- `string.h` / `string` - 字符串处理
- `math.h` / `cmath` - 数学函数
- `time.h` - 时间处理

### 第三方库
```bash
# 算法竞赛常用
# STL（C++标准模板库）已包含在编译器中

# 数据可视化（需要单独安装）
# matplotlib-cpp（C++版matplotlib）

# 网络编程
# libcurl
```

## 学习建议

1. **理解内存管理** - C/C++ 的特色，掌握指针和内存分配
2. **多动手实践** - 在线判题系统刷题
3. **学习调试** - 学会使用 GDB 或 IDE 调试工具
4. **阅读代码** - 看优秀开源项目的代码
5. **循序渐进** - 先掌握 C 语言基础，再学习 C++ 特性

## 常见问题

### Q1: C 和 C++ 应该先学哪个？
**A**: 建议先学 C 语言打基础，再学 C++ 的面向对象和 STL。C++ 兼容 C，可以逐步过渡。

### Q2: 指针太难了怎么办？
**A**:
1. 理解内存和地址的概念
2. 多画图理解指针关系
3. 从简单的指针应用开始
4. 多做练习加深理解

### Q3: 段错误（Segmentation Fault）怎么办？
**A**:
1. 检查数组越界
2. 检查空指针解引用
3. 检查野指针
4. 使用调试工具定位

### Q4: 如何提升编程能力？
**A**:
1. 刷算法题（洛谷、力扣）
2. 做项目实践
3. 参加编程比赛
4. 学习数据结构和算法

## 下一步学习

完成入门后，你可以：

1. **深入 C++** - 学习面向对象、STL、设计模式
2. **数据结构** - 数组、链表、树、图等
3. **算法** - 排序、搜索、动态规划等
4. **系统编程** - 操作系统、网络编程
5. **竞赛编程** - ACM/ICPC、NOI 等

## 推荐学习资源

### 零基础人群

- [菜鸟教程 C++ 教程](https://www.runoob.com/cplusplus/cpp-tutorial.html)
  > 专为初学者打造，涵盖基础到高级概念

- [OI-Wiki 语言基础](https://oi-wiki.org/lang/)
  > 编程相关知识，包括 C++ 从入门到进阶教程
  > 程序是算法与数据结构的载体，是解决 OI 问题的工具
  > 在 OI 中，最常用的编程语言是 C++
  > 学习编程是学习 OI 最基础的部分

- [C++ 在线编辑器](https://www.runoob.com/try/runcode.php?filename=helloworld&type=cpp)
  > 在线练习 C++ 代码

### 有一定基础人群

推荐以[洛谷题单广场](https://www.luogu.com.cn/training/list)的顺序开始练习，题单难度不小，但可以依照此学习顺序。

### 其他资源

- [C语言中文网](http://c.biancheng.net/)
- [B站黑马程序员C++教程](https://www.bilibili.com/video/BV1et411b73Z)
- [LeetCode 中国](https://leetcode.cn/) - 算法练习平台
- [牛客网](https://www.nowcoder.com/) - 笔试面试准备

加油！C/C++ 会让你对计算机有更深刻的理解！💪
