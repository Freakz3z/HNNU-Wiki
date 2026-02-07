# 选择 IDE

在 [学习路线图](/快速开始/学习路线图.md) 中提到了以下内容：

* [C++在线编辑器](https://www.runoob.com/try/runcode.php?filename=helloworld\&type=cpp)
* [Dev-C++：适合初学者的IDE](https://sourceforge.net/projects/orwelldevcpp/)

在本文中，编程语言将不止限制于 C/C++，笔者也根据自己的使用体验和实际情况来聊一聊各种 IDE，希望你能选择到适合自己的 IDE。

## 对各种IDE的分析评价

### 1. [Visual Studio Code](https://code.visualstudio.com/)

* **适用语言**：JavaScript, TypeScript, Python, C++, Java, Go, PHP, Ruby 等
* **优势**：
  * 免费且开源，跨平台（Windows, macOS, Linux）。
  * 丰富的插件生态系统，几乎支持所有语言和框架。
  * 内置 Git 支持，强大的调试功能。
  * 轻量级，启动速度快。
* **用户群体**：前端开发者、全栈开发者、数据科学家

> 值得一提的是，笔者编写这本手册使用的就是 VSCode，包括项目的开发也是。VSCode 是目前为止笔者使用的最舒服的 IDE 而没有之一。几乎支持所有的语言和框架，这点在笔者看来对其他 IDE 有些降维打击了，大力推崇。~~但 VSCode 被某人评价为文本编辑器。~~

### 2. [IntelliJ IDEA](https://www.jetbrains.com/idea/)

* **适用语言**：Java, Kotlin, Groovy, Scala, JavaScript, SQL 等
* **优势**：
  * 强大的代码智能提示和重构功能。
  * 集成的版本控制系统支持（如 Git）。
  * 完善的插件生态，支持多种框架（如 Spring, Hibernate）。
  * 优秀的性能，适合大型项目。
* **用户群体**：Java 开发者、企业级应用开发者

> Java 开发的首选，个人认为使用体验跟 VSCode 类似。

### 3. [PyCharm](https://www.jetbrains.com/pycharm/)

* **适用语言**：Python
* **优势**：
  * 专为 Python 开发设计，功能强大。
  * 代码分析和调试工具非常完善。
  * 集成 Django 和 Flask 等框架的支持。
  * 版本控制系统集成。
* **用户群体**：Python 开发者、数据科学家、Web 开发者

> 虽然但是，笔者也没有使用过 PyCharm，所以不好对其进行更多的评价。但集成 Django 和 Flask 的支持确实是很诱人的。

### 4. [Visual Studio](https://visualstudio.microsoft.com/vs/)

* **适用语言**：C#, C++, Visual Basic, F#, JavaScript 等
* **优势**：
  * 功能强大，适合 Windows 应用和 Web 应用开发。
  * 支持 Azure 集成，适合云开发。
  * 强大的调试和测试工具。
  * 适合大型企业和团队开发。
* **用户群体**：C# 开发者、Windows 应用开发者、企业开发团队

> 对于笔者自己而言，VS 的使用体验是最差的，当然如果只是用来学习基本的 C/C++还尚且足够，好过 DEV-C++。由于笔者没有开发过关于 C/C++的项目，所以不好对其进行更多的评价。

### 5. [Atom](https://atom.io/) ⚠️ 已停止维护

> **重要提示**：Atom 已于 2022年12月15日停止维护，GitHub 推荐用户迁移到 [VS Code](https://code.visualstudio.com/) 或其他替代品。

* **适用语言**：HTML, CSS, JavaScript, Python, Ruby 等
* **历史优势**：
  * 曾经免费且开源，易于自定义。
  * 内置 Git 支持，适合团队协作。
  * 包含多种主题和插件，用户可以根据需求进行扩展。
* **替代方案**：[VS Code](https://code.visualstudio.com/)、[Sublime Text](https://www.sublimetext.com/)

### 5. [Sublime Text](https://www.sublimetext.com/)

* **适用语言**：几乎所有编程语言
* **优势**：
  * 极快的启动速度和响应速度。
  * 强大的多光标编辑功能。
  * 丰富的包生态系统。
  * 跨平台支持。
* **用户群体**：追求效率的开发者、文本编辑爱好者

> 轻量级但功能强大，适合不喜欢复杂IDE的用户。无限期免费试用（完整版需购买许可）。

### 6. [Android Studio](https://developer.android.com/studio)

* **适用语言**：Java, Kotlin
* **优势**：
  * 官方 Android 开发 IDE，支持所有 Android 相关开发。
  * 强大的布局编辑器和模拟器。
  * 集成 Gradle 构建系统，简化项目管理。
* **用户群体**：Android 应用开发者

> 安卓开发的首选，只是作为一个例子放在这里，貌似在日后很长的学习中都不会用到。

## 另外的一些话

有的同学可能会问，能不能一次性下载所有的IDE以备后面的学习和开发使用。答案当然是肯定的，但是不同的 IDE 间可能会出现一些问题，比如如果先下载了 VS 后再去 VSCode 中使用 C/C++就可能会出现一些问题，需要额外的花时间去解决。这当然不是什么非常大的事情，但是还是建议大家根据自己的需求来选择适合自己的 IDE。

## 更多代码编辑器及工具
[工具软件简介 - OI Wiki](https://oi-wiki.org/tools/)