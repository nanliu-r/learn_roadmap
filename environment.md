# AI 开发环境搭建教程

> 适用系统：Windows / macOS / Linux  
> 目标：安装 VS Code + Python 3.10+ + Miniconda，创建虚拟环境 `ai-agent-env`，并安装 Jupyter 插件与 GitHub Copilot。

---

## 第一阶段：安装核心工具

### 步骤 1：安装 VS Code

1. 前往官网下载对应系统的安装包：  
   <https://code.visualstudio.com>

2. 按平台安装：
   - **macOS**：下载 `.dmg`，将 VS Code 拖入 `Applications` 文件夹。
   - **Windows**：下载 `.exe` 安装包，全程默认 Next，**务必勾选「Add to PATH」**。
   - **Linux**：下载 `.deb` / `.rpm` 包，或参考官网 snap 安装方式。

3. 验证安装（打开终端）：

   ```bash
   code --version
   ```

   输出版本号即表示安装成功。

---

### 步骤 2：安装 Python 3.10+

1. 前往官网下载：  
   <https://www.python.org/downloads>  
   选择 **3.10 或更高版本**。

2. 按平台安装：
   - **Windows**：运行安装包，**务必勾选「Add Python to PATH」**，否则终端无法识别 `python` 命令。
   - **macOS**：可使用安装包，或通过 Homebrew 安装：

     ```bash
     brew install python@3.11
     ```

3. 验证安装：

   ```bash
   python --version
   # 输出示例：Python 3.11.x
   ```

---

### 步骤 3：安装 Miniconda

Miniconda 是轻量版 Conda，用于管理虚拟环境和包依赖。

1. 前往官网下载（选择适合系统的版本）：  
   <https://docs.conda.io/en/latest/miniconda.html>

2. 按平台安装：
   - **Windows**：运行 `.exe` 安装包，选「Just Me」，建议勾选「Add Miniconda3 to PATH」（或后续使用 Anaconda Prompt）。
   - **macOS / Linux**：下载 `.sh` 脚本后运行：

     ```bash
     bash Miniconda3-latest-MacOSX-x86_64.sh
     ```

     按提示全程回车，出现 `yes/no` 时输入 `yes`。

3. 重启终端后，验证安装：

   ```bash
   conda --version
   # 输出示例：conda 23.x.x
   ```

---

## 第二阶段：创建虚拟环境

### 步骤 4：创建并配置 `ai-agent-env`

虚拟环境可隔离项目依赖，避免不同项目之间的版本冲突。

1. 创建环境（指定 Python 3.11）：

   ```bash
   conda create -n ai-agent-env python=3.11 -y
   ```

   > 如果此步骤下载太慢，可以进行以下改进：
   >
   > ```bash
   > # 1. 添加清华源的各个主频道
   > conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
   > conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
   > conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
   > # 2. 让 Conda 在下载时显示具体的包来自哪个源（方便排查）
   > conda config --set show_channel_urls yes
   > # 3. 使用 libmamba 加速器
   > conda config --set solver libmamba
   > ```

2. 激活环境：

   ```bash
   conda activate ai-agent-env
   ```

   激活成功后，终端提示符左侧会显示 `(ai-agent-env)`。

3. 安装 `ipykernel`，使 Jupyter 能够识别该环境：

   ```bash
   pip install ipykernel
   python -m ipykernel install --user --name=ai-agent-env
   ```

> **常用环境管理命令**
>
> | 操作 | 命令 |
> |------|------|
> | 查看所有环境 | `conda env list` |
> | 退出当前环境 | `conda deactivate` |
> | 删除环境 | `conda remove -n ai-agent-env --all` |
> | 导出环境配置 | `conda env export > environment.yml` |
> | 从配置还原环境 | `conda env create -f environment.yml` |

---

## 第三阶段：安装 VS Code 插件

在 VS Code 中按 `Ctrl+Shift+X`（macOS：`⌘+Shift+X`）打开插件面板。

### 步骤 5：安装 Jupyter 插件

搜索并安装以下两个插件（均由 Microsoft 发布）：

| 插件名 | 说明 |
|--------|------|
| **Python** | Python 语言基础支持，必装 |
| **Jupyter** | 支持 `.ipynb` 文件，含 Jupyter Keymap、Jupyter Cell Tags 等组件 |

安装完成后，打开任意 `.ipynb` 文件，点击右上角 **「Select Kernel」**，选择 `ai-agent-env` 即可使用刚创建的虚拟环境。

---

### 步骤 6：安装 GitHub Copilot

搜索并安装以下两个插件（均由 GitHub 发布）：

| 插件名 | 说明 |
|--------|------|
| **GitHub Copilot** | 行内代码补全 |
| **GitHub Copilot Chat** | 侧边栏对话，支持解释、重构、生成代码 |

> **前置条件**：需要 GitHub 账号并已订阅 Copilot。  
> - 个人版：$10 / 月  
> - 学生、开源维护者：免费申请（<https://education.github.com>）

安装后，VS Code 会提示登录 GitHub 授权，按指引完成即可。

---

## 步骤 7：验证整体环境

在 VS Code 中新建文件 `test.ipynb`，在第一个 Cell 输入以下代码，按 `Shift+Enter` 运行：

```python
import sys
print(sys.version)
print("环境搭建成功 ✓")
```

**预期输出：**

```
3.11.x (main, ...) [...]
环境搭建成功 ✓
```

确认右上角 Kernel 显示 `ai-agent-env`，说明 VS Code、Conda 虚拟环境与 Jupyter 已全部联通，环境搭建完成。
