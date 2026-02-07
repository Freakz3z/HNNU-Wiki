Conda 是一个流行的包管理和环境管理工具，特别适用于 Python 和 R 的数据科学和科学计算。

## 1. **环境管理**

- **创建新环境**：
  ```bash
  conda create --name myenv
  ```
  创建一个名为 `myenv` 的新环境。

- **创建新环境并指定 Python 版本**：
  ```bash
  conda create --name myenv python=3.8
  ```
  创建一个名为 `myenv` 的新环境，并指定 Python 版本为 3.8。

- **激活环境**：
  ```bash
  conda activate myenv
  ```
  激活名为 `myenv` 的环境。

- **停用当前环境**：
  ```bash
  conda deactivate
  ```
  退出当前激活的环境。

- **列出所有环境**：
  ```bash
  conda env list
  ```
  显示系统中所有的 Conda 环境。

- **删除环境**：
  ```bash
  conda remove --name myenv --all
  ```
  删除名为 `myenv` 的环境及其所有包。

## 2. **包管理**

- **安装包**：
  ```bash
  conda install package_name
  ```
  安装指定名称的包。例如：
  ```bash
  conda install numpy
  ```

- **安装特定版本的包**：
  ```bash
  conda install package_name=1.0.0
  ```
  安装指定版本的包，例如 `numpy` 版本 1.18.1。

- **更新包**：
  ```bash
  conda update package_name
  ```
  更新指定的包到最新版本。

- **更新所有包**：
  ```bash
  conda update --all
  ```
  更新当前环境中的所有包。

- **卸载包**：
  ```bash
  conda remove package_name
  ```
  卸载指定的包。

- **查看已安装的包**：
  ```bash
  conda list
  ```
  列出当前环境中安装的所有包。

## 3. **环境导出和恢复**

- **导出环境**：
  ```bash
  conda env export > environment.yml
  ```
  将当前环境导出到 `environment.yml` 文件中。

- **从环境文件创建环境**：
  ```bash
  conda env create -f environment.yml
  ```
  根据 `environment.yml` 文件创建一个新环境。

## 4. **搜索和信息**

- **搜索包**：
  ```bash
  conda search package_name
  ```
  在 Conda 仓库中搜索指定的包。

- **显示包信息**：
  ```bash
  conda info package_name
  ```
  显示指定包的详细信息。

## 5. **其他常用命令**

- **清理未使用的包和缓存**：
  ```bash
  conda clean --all
  ```
  清理未使用的包、缓存和其他临时文件。

- **帮助手册**：
  ```bash
  conda --help
  ```
  显示 Conda 的帮助信息。
