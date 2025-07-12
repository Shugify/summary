[TOC]



# 环境配置(针对pytorch项目)



## 常规概念解释

### 环境变量

**环境变量**一般是指在操作系统中用来指定操作系统运行环境的一些参数，是操作系统为了满足不同的应用场景预先在系统内预先设置的一大批全局变量。

在Linux系统中，环境变量可以分为以下几类：

* 系统级环境变量：
  系统级环境变量对所有用户和进程都可见。它们通常在系统启动时被设置，并被所有用户和进程共享。一些常见的系统级环境变量包括PATH（用于指定可执行文件的搜索路径）、LANG（用于设置系统语言环境）等。

* 用户级环境变量：
  用户级环境变量是每个用户独立设置的，只对该用户及其相关进程可见。这些变量可以在登录时通过不同的配置文件（如.bashrc、.bash_profile、.profile等）设置。常见的用户级环境变量包括HOME（指定用户的主目录路径）、USER（当前用户名）等。

* 进程级环境变量：
  进程级环境变量是由特定进程设置的，并且仅对该进程及其子进程可见。这些变量可以通过编程语言（如C语言中的setenv函数）在程序中进行设置，或者通过终端命令行在特定的进程上下文中设置。

需要注意的是，系统级环境变量和用户级环境变量通常是通过配置文件进行设置和管理的。对于系统级环境变量，常见的配置文件包括/etc/profile和/etc/environment。对于用户级环境变量，常见的配置文件包括用户的个人配置文件（如.bashrc、.bash_profile、.profile等）。



**常见的Linux环境变量：**

* PATH：决定了系统在哪些目录中查找可执行文件。当你输入一个命令时，系统会在PATH中定义的目录中查找该命令的可执行文件。

* HOME：指定当前用户的主目录路径。

* USER：当前用户的用户名。

* SHELL：指定当前用户默认使用的shell。

* LANG：指定系统的默认语言。

* LD_LIBRARY_PATH：指定系统在哪些目录中查找共享库文件。

* TERM：指定当前终端的类型。

* PS1：定义命令行提示符的格式。

* PS2：定义多行命令的提示符的格式。
  

安装 Conda、Java、Python 等软件后要更新环境变量 `PATH`，系统通过 `PATH` 环境变量中的目录，来查找你输入的命令（如 `python`, `java`, `conda`）的可执行文件



### .bashrc

 `bash` 是 Linux 和类 Unix 系统中最常用的 **命令行解释器（shell）**

<img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709103931579.png" alt="image-20250709103931579" style="zoom: 80%;" />

**配置文件是用来定义或修改环境变量的文件**，它们会在你打开终端或登录系统时被自动执行，从而设置好你的环境变量。

`.bashrc`是 Linux 和类 Unix 系统中 **bash shell 的用户级配置文件**，一般位于 ~/.bashrc

在`.bashrc`中更新`PATH`方法：

* 打开./bashrc文件

```
vim ~/.bashrc
```

* 在文件尾添加新路径，保存并退出

```export PATH="新路径:$PATH"
export PATH="新路径:$PATH"
```

* 刷新./bashrc文件令其立刻生效

```
source ~/.bashrc
```

* 验证PATH是否有效(观察输出路径是否正确)

```
echo $PATH
```

`./bashrc`示例

```
# 设置 Conda 路径
export PATH="$HOME/anaconda3/bin:$PATH"

# 设置自定义 Python
export PATH="/opt/python3.11/bin:$PATH"

# 设置 Java 路径，可用变量JAVA_HOME
export JAVA_HOME="/usr/lib/jvm/java-11-openjdk"
export PATH="$JAVA_HOME/bin:$PATH"
```

目前的conda等会自动在bashrc文件中加入一段初始化脚本，这个脚本的作用是：

- 动态把 `conda` 命令加入当前 shell 环境
- 运行时修改 `PATH`，激活 conda base 环境
- 支持 `conda activate` 和 `conda deactivate`

**它是写在 `~/.bashrc` 文件里的**，但不会直接修改系统的全局 `PATH`，而是在你打开新终端或 `source ~/.bashrc` 时生效。



想用更直接的方式配置 `PATH`，或者安装器没有自动写入初始化代码（比如手动解压安装），或者想临时切换 conda 路径：

需要手动 `export PATH=...`





pytorch相关的重要环境变量的CUDA_VISIABLE_DEVICES





代理http_proxy, https_proxy





## 深度学习项目准备

* 环境准备流程图

```
① 安装 Python 和 Conda（Miniconda/Miniforge）
         ↓
② 创建虚拟环境（指定 Python 版本）
         ↓
③ 安装框架（如 PyTorch、TensorFlow）
         ↓
④ 安装其他依赖包（如 numpy、scikit-learn、matplotlib 等）
         ↓
⑤ 验证 GPU、代码是否能正常运行
```



### Python

* 查看当前已安装python版本

```
python --version
```

* 运行python文件

```
python file.py
```

<img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709113653116.png" alt="image-20250709113653116" style="zoom:80%;" />



### conda

conda是一个 **开源的包管理器 + 环境管理器**

* 包管理器，类似于 pip，但功能更强大。会自动安装依赖包，支持从多个镜像源（如 TUNA、清华、Anaconda Cloud）下载,例如：

```
conda install numpy
conda remove pandas
conda update scikit-learn
```

* 虚拟环境管理器，允许你为每个项目创建独立的 Python 环境，不同项目可使用不同的 Python 版本或依赖版本，例如：

```
conda create -n myenv python=3.12
conda activate myenv
python  # 进入 Python 交互环境，检查版本,临时试验、调试、学习（用的不多
exit    # 退出 Python
conda deactivate	#退出当前激活的环境，返回到 base 环境或系统默认环境
```

* 查看所有虚拟环境

```
conda env list
```

* 删除环境

```
conda remove -n myenv --all
```

* 更新conda本身(建议在base环境下进行)

```
conda activate base
conda update -n base -c conda-forge conda
```

* 验证环境是否正常

```
conda info --envs      # 查看所有环境
python --version       # 应该输出 Python 3.12.11
which python           # 应该指向 sjjenv 的 bin 目录
```

<img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250709113432537.png" alt="image-20250709113432537" style="zoom:80%;" />

* 导出当前环境为 `yml` 文件（方便复现）

```
conda env export > sjjenv.yml
```



### CUDA

Conda 环境隔离的是软件栈（Python + 包 + 依赖库），不隔离硬件驱动和操作系统资源，因此nvcc显示出结果一样，但每个conda环境需要单独安装python和pytorch

```
import torch
print(torch.__version__)
```

该命令显示的是表示 **PyTorch 是用哪个 CUDA 版本编译出来的**。

即安装pytorch时执行的

```
pip install torch==2.1.2+cu118 --index-url https://download.pytorch.org/whl/cu118
```







nvidia-smi与nvcc两者不同



| `nvcc --version` | 显示系统 CUDA Toolkit 编译器版本 | 系统级 CUDA |
| ---------------- | -------------------------------- | ----------- |
|                  |                                  |             |

| `torch.version.cuda` | 显示当前 PyTorch 使用的 CUDA 版本 |
| -------------------- | --------------------------------- |
|                      |                                   |



CUDA的组成



指定用于训练得到的GPU

CUDA_VISIBLE_DEVICES=1 python train.py



下载对应CUDA的pytorch



### cuDNN







## 第一个pytorch项目

project_root/   ← 鉴别猫狗项目
├── dataset/
│   ├── train/
│   │   ├── cat/   ← 10 张猫的图片（命名如 cat1.jpg, cat2.jpg...）
│   │   └── dog/   ← 10 张狗的图片（dog1.jpg, dog2.jpg...）
│   ├── val/
│   │   ├── cat/   ← 验证集可以复制训练集几张过来（或随机划分）
│   │   └── dog/
├── train.py         ← 主训练脚本
├── model/           ← 模型保存目录
├── outputs/         ← 日志输出/可视化预测
├── requirements.txt ← 环境依赖



`requirements.txt` 是一个用来记录 Python 项目的依赖库及其版本的**纯文本文件**，在 Python 项目中非常常见，特别是和 `pip` 搭配使用。

假设你的项目用到了三方库，写成requirements.txt后为

```
torch==2.1.0
torchvision==0.16.0
numpy>=1.21.0
matplotlib
```

运行

```
pip install -r requirements.txt
```

含义是：**读取 `requirements.txt` 中的每一行，并依次安装对应库及其版本**。



如果你已经在虚拟环境中安装了所需的库，想保存下来：

```
pip freeze > requirements.txt
```







