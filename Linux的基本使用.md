[TOC]



# linux的基本使用

[Linux 命令大全 | 菜鸟教程](https://www.runoob.com/linux/linux-command-manual.html)



### 1. 文件与目录管理

这些命令用于在你的项目文件夹中导航、查看和操作文件。

- **`ls`**：**列出目录内容**。

  - `ls`：显示当前目录下的文件和文件夹。

  - `ls -l`：显示详细列表，包括权限、所有者、大小、修改日期等。

  - `ls -a`：显示所有文件，包括隐藏文件（以 `.` 开头的文件）。

  - `ls -F`：在目录名后添加 `/`，在可执行文件后添加 `*`，方便识别。

  - `ls -lh`：以人类可读的格式显示文件大小（例如 1K, 234M, 2G）。

  - **示例**:

    Bash

    ```
    ls -lh
    # 会显示类似：
    # total 16K
    # drwxr-xr-x 2 user user 4.0K Jul 20 10:00 dataset/
    # -rw-r--r-- 1 user user 2.5K Jul 20 10:30 train.py
    # drwxr-xr-x 2 user user 4.0K Jul 20 10:00 model/
    ```

- **`cd`**：**改变目录**（Change Directory）。

  - `cd your_directory_name`：进入指定目录。

  - `cd ..`：返回上一级目录。

  - `cd` 或 `cd ~`：回到你的主目录。

  - `cd -`：回到上一个工作目录。

  - **示例**:

    Bash

    ```
    cd dataset/train
    # 进入到你项目的训练数据集目录
    ```

- **`pwd`**：**打印当前工作目录**（Print Working Directory）。

  - `pwd`：显示你当前所在的完整路径。

  - **示例**:

    Bash

    ```
    pwd
    # /home/your_username/your_pytorch_project/dataset/train
    ```

- **`mkdir`**：**创建目录**（Make Directory）。

  - `mkdir new_folder`：创建一个新文件夹。

  - `mkdir -p path/to/new/deep/folder`：递归创建多级目录，即使中间的目录不存在也会一并创建。

  - **示例**:

    Bash

    ```
    mkdir new_experiments
    mkdir -p results/epoch_1
    ```

- **`rm`**：**删除文件或目录**（Remove）。

  - `rm file.txt`：删除文件。
  - `rm -r folder_name`：递归删除目录及其所有内容（**请谨慎使用，删除后通常无法恢复！**）。
  - `rm -rf folder_name`：强制递归删除目录及其所有内容（`f` 是 force，**极其危险，千万小心！**）。

- **`cp`**：**复制文件或目录**（Copy）。

  - `cp source_file destination_file`：复制文件。

  - `cp -r source_folder destination_folder`：递归复制目录及其所有内容。

  - **示例**:

    Bash

    ```
    cp config.yaml config_backup.yaml
    cp -r dataset_small dataset_full
    ```

- **`mv`**：**移动或重命名文件/目录**（Move）。

  - `mv old_name new_name`：重命名文件或目录。

  - `mv file.txt /path/to/new_location/`：移动文件到新位置。

  - **示例**:

    Bash

    ```
    mv resnet18_catdog.pth final_model.pth
    mv my_script.py scripts/
    ```

- **`cat`**：**查看文件内容**（Concatenate and Print）。

  - `cat file.txt`：将文件内容输出到终端。

  - **示例**:

    Bash

    ```
    cat train.py
    # 会在终端显示 train.py 的代码内容
    ```

- **`head` / `tail`**：**查看文件开头/结尾**。

  - `head -n 10 file.txt`：显示文件的前 10 行。

  - `tail -n 10 file.txt`：显示文件的最后 10 行。

  - `tail -f log_file.log`：实时跟踪文件末尾的追加内容（**非常适合查看模型训练日志！**）。按 `Ctrl+C` 退出。

  - **示例**:

    Bash

    ```
    tail -f training_log.txt
    ```

- **`find`**：**查找文件或目录**。

  - `find . -name "*.py"`：在当前目录（`.`）及其子目录中查找所有 `.py` 文件。

  - `find /home/user/my_project -type d -name "model*"`：在指定路径下查找所有名字以 "model" 开头的目录（`d` 代表 directory）。

  - **示例**:

    Bash

    ```
    find . -name "cat_image_*.jpg"
    ```

------



### 2. 环境与包管理

如果你使用 **Conda**（推荐用于 PyTorch），以下命令是必须的：

- **`conda env list`**：**列出所有 Conda 环境**。

  - `conda env list`：显示所有已创建的 Conda 环境及其路径。你的 PyTorch 项目通常会运行在一个独立的 Conda 环境中。

  - **示例**:

    Bash

    ```
    conda env list
    # # conda environments:
    # #
    # base                     /opt/conda
    # pytorch_env           * /opt/conda/envs/pytorch_env
    ```

- **`conda activate your_env_name`**：**激活 Conda 环境**。

  - `conda activate pytorch_env`：进入名为 `pytorch_env` 的 Conda 环境。激活环境后，你在终端安装的包都会安装到这个环境里，且当你运行 Python 脚本时，会使用这个环境中的 Python 解释器和库。

  - **示例**:

    Bash

    ```
    conda activate pytorch_env
    (pytorch_env) $ python train.py # 括号表示环境已激活
    ```

- **`conda deactivate`**：**退出当前 Conda 环境**。

  - **示例**:

    Bash

    ```
    (pytorch_env) $ conda deactivate
    $ # 退出环境后，括号消失
    ```

- **`conda install package_name`**：**安装包**。

  - `conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia`：这是安装 PyTorch 和 TorchVision 的典型命令（根据 CUDA 版本调整）。
  - `conda install numpy matplotlib`：安装其他 Python 库。

- **`pip install package_name`**：**使用 pip 安装包**。

  - `pip` 是 Python 自己的包管理器，通常在 Conda 环境中也可用。如果 Conda 没有某个包，或者 PyTorch 官方建议用 pip 安装特定版本，就会用到它。
  - `pip install -r requirements.txt`：安装 `requirements.txt` 文件中列出的所有依赖包。

------



### 3. 资源监控

在训练深度学习模型时，监控 GPU 和 CPU 使用情况至关重要。

- **`nvidia-smi`**：**监控 NVIDIA GPU 使用情况**。

  - `nvidia-smi`：显示 GPU 的使用率、显存占用、温度等信息。

  - `watch -n 1 nvidia-smi`：每 1 秒刷新一次 `nvidia-smi` 的输出，**非常有用，可以实时监控 GPU 状态**。按 `Ctrl+C` 退出。

  - **示例**:

    Bash

    ```
    watch -n 1 nvidia-smi
    # 会显示类似：
    # +-----------------------------------------------------------------------------+
    # | NVIDIA-SMI 535.104.05   Driver Version: 535.104.05   CUDA Version: 12.2     |
    # |-------------------------------+----------------------+----------------------+
    # | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
    # | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
    # |                               |                      |               MIG M. |
    # |===============================+======================+======================|
    # |   0  NVIDIA A100... Off      | 00000000:01:00.0 Off |                    0 |
    # | 30%   45C    P2    60W / 300W |  15360MiB / 40960MiB |     95%      Default |
    # +-------------------------------+----------------------+----------------------+
    ```

- **`nvcc -V`/`nvcc --version`：** **显示已安装的 CUDA 编译器的版本信息**

  * - **示例**:

      Bash

      ```
      nvcc -V
      nvcc: NVIDIA (R) Cuda compiler driver
      Copyright (c) 2005-2023 NVIDIA Corporation
      Built on Mon_Apr__3_17:16:06_PDT_2023
      Cuda compilation tools, release 12.1, V12.1.105
      Build cuda_12.1.r12.1/compiler.32688072_0
      ```

- **`htop` / `top`**：**监控 CPU、内存和进程**。

  - `top`：Linux 自带的进程监控工具，显示 CPU 和内存使用率以及运行的进程。

  - `htop`：`top` 的增强版，界面更友好，功能更强大，通常需要额外安装 (`sudo apt install htop` 或 `sudo yum install htop`)。

  - **示例**:

    Bash

    ```
    htop
    # 会显示一个交互式界面，显示CPU核心使用率、内存使用情况以及进程列表。
    ```

- **`df -h`**：**查看磁盘空间使用情况**。

  - `df -h`：显示文件系统的磁盘空间使用情况（以人类可读格式）。

  - **示例**:

    Bash

    ```
    df -h
    # Filesystem      Size  Used Avail Use% Mounted on
    # /dev/sda1       200G   50G  140G  27% /
    ```

------



### 4. 文本编辑

你可能需要在终端直接编辑配置文件或脚本。

- **`nano` / `vim`**：**终端文本编辑器**。

  - `nano filename.txt`：一个简单易用的文本编辑器，适合初学者。

  - `vim filename.txt`：一个功能强大的文本编辑器，学习曲线较陡峭，但效率极高。

  - **示例**:

    Bash

    ```
    nano requirements.txt
    ```



### 5. 进程管理与后台任务

在训练深度学习模型时，训练过程通常很长，你不能一直开着终端。这时，进程管理就显得至关重要。

- **ps**：**查看当前用户的进程 (Process Status)**。

  - ps aux: 显示系统中所有用户的详细进程信息。这在你需要查找特定 Python 训练脚本的进程 ID (PID) 时非常有用。
  - ps -ef | grep python: 筛选出所有与 python 相关的进程，这是快速定位你的训练任务的常用方法。
  - **PyTorch 场景**: 当你的训练意外卡住，或者你忘记了哪个终端在运行哪个模型时，可以用 ps 来查找进程 PID。

- **kill**：**终止进程**。

  - kill <PID>: 向指定进程发送一个终止信号，尝试正常关闭它。
  - kill -9 <PID>: 强制终止一个进程。当一个进程无响应时（例如，GPU 显存泄漏导致程序卡死），这个命令是你的最后手段。
  - **PyTorch 场景**: 你的训练脚本失控，占用了所有 GPU 资源且无法通过 Ctrl+C 停止，这时你需要 ps 找到它的 PID，然后用 kill -9 来强制结束它，释放 GPU。

- **nohup**：**让命令在后台持续运行 (No Hang Up)**。

  - nohup python train.py &: 在后台运行你的训练脚本。即使你关闭了终端窗口，训练任务依然会继续运行。& 符号表示“在后台运行”。

  - 默认情况下，nohup 会将所有的标准输出（例如 print 语句）重定向到当前目录下一个名为 nohup.out 的文件里。

  - **PyTorch 场景**: 这是在远程服务器上进行长时间训练的基础命令。例如：

    ```
    nohup python train.py --epochs 100 > training_log.log 2>&1 &
    ```

    - \> training_log.log: 将标准输出重定向到 training_log.log 文件。
    - 2>&1: 将标准错误输出也重定向到标准输出（即，也写入 training_log.log 文件）。
    - 使用tmux就不需要使用`nohup`了

- **jobs / fg / bg**：**管理后台任务**。

  - jobs: 查看当前终端会话中，有哪些在后台运行的任务。
  - bg: 将一个暂停的任务转到后台继续运行。
  - fg %<job_number>: 将一个后台任务调回到前台运行。
  - **PyTorch 场景**: 你用 Ctrl+Z 暂停了一个训练任务，可以用 bg 让它在后台继续跑，或者用 fg 把它调回前台查看实时输出。

### 6. 远程操作与会话管理

当你使用远程服务器（如公司内网服务器、云服务器 AWS/GCP/Azure）进行训练时，这些命令是必不可少的。

- **ssh**：**安全登录远程主机 (Secure Shell)**。
  - ssh username@remote_host_ip: 连接到远程服务器。
  - **PyTorch 场景**: 这是你登录远程 GPU 服务器的第一步。
- **scp**：**安全地在本地和远程主机间复制文件 (Secure Copy)**。
  - scp local_file.py username@remote_host:/path/to/destination: 将本地文件上传到服务器。
  - scp username@remote_host:/path/to/model.pth .: 将服务器上的模型权重下载到本地（. 表示当前目录）。
  - **PyTorch 场景**: 上传你的代码、下载训练好的模型权重和日志文件。
- **tmux / screen**：**终端复用器 (Terminal Multiplexer)**。
  - **强烈推荐！** tmux 和 screen 允许你创建一个持久的终端会话。即使你的 SSH 连接因为网络问题断开，这个会话和里面运行的程序（如你的训练脚本）依然会在服务器上保持运行。当你重新连接后，可以再次“附加” (attach) 到这个会话。
  - **基本流程**:
    1. tmux new -s my_training_session: 创建一个名为 my_training_session 的新会话。
    2. 在这个会话里，像往常一样运行你的 python train.py。
    3. 直接关闭你的本地终端（或者按 Ctrl+b 然后按 d 来分离会话）。
    4. 重新 SSH 登录服务器后，输入 tmux attach -t my_training_session 即可回到之前的会话。
  - **PyTorch 场景**: 这是比 nohup 更强大、更灵活的长时间任务管理工具。你可以在一个 tmux 会话中开多个窗口，一个跑训练，一个用 nvidia-smi 监控，一个用 htop 监控 CPU，非常方便。

### 7. 数据处理与传输

深度学习项目通常涉及巨大的数据集，高效地处理和传输它们非常重要。

- **tar / zip**：**打包与压缩**。
  - tar -czvf dataset.tar.gz /path/to/dataset/: 将 dataset 目录打包并用 gzip 压缩成 dataset.tar.gz。
  - tar -xzvf dataset.tar.gz: 解压文件。
  - **PyTorch 场景**: 当你需要上传或下载整个数据集时，先打包压缩成一个文件会比传输成千上万个小文件快得多。
- **rsync**：**远程文件同步**。
  - rsync -avz /local/path/to/dataset/ username@remote_host:/remote/path/: 高效地将本地数据集同步到远程服务器。
  - rsync 是增量同步的，它只会传输有变化的文件，因此比 scp 更快、更智能，尤其适合同步大型或频繁更新的目录。
  - **PyTorch 场景**: 同步你的代码库或者巨大的数据集目录，中断后还可以续传。
- **du**：**查看目录或文件的磁盘使用情况 (Disk Usage)**。
  - du -sh /path/to/folder: 估算指定目录的总大小 (s for summary, h for human-readable)。
  - **PyTorch 场景**: 检查你的数据集、模型权重或实验结果占用了多少磁盘空间。

### 8. 脚本与自动化

- **alias**：**设置命令别名**。
  - alias watch-gpu='watch -n 1 nvidia-smi': 创建一个名为 watch-gpu 的新命令，以后你只需要输入 watch-gpu 就能实时监控 GPU。
  - 你可以将常用的 alias 添加到你的 ~/.bashrc 或 ~/.zshrc 文件中，使其永久生效。
  - **PyTorch 场景**: 为常用的长命令（如激活 Conda 环境、SSH 登录等）创建简短的别名，提高效率。
- **Bash 脚本**：
  - 学习编写简单的 Shell 脚本（.sh 文件）来自动化你的工作流。
  - **PyTorch 场景**:
    - 
    - 编写一个 train.sh 脚本，在里面设置好所有参数，然后一键启动训练：bash train.sh。
    - 编写一个脚本来自动下载数据、解压、然后启动训练。
    - 编写一个脚本来对多个超参数组合进行循环，依次启动训练任务。





### 文本编辑与输出

##### **vim**-文本编辑器

* 打开文件

```
vim hello.py
```

<img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250708191140011.png" alt="image-20250708191140011" style="zoom: 67%;" />

* 命令模式下常规命令

  - **i** -- 切换到输入模式，在光标当前位置开始输入文本。

  - **x** -- 删除当前光标所在处的字符。

  - **:** -- 切换到底线命令模式，以在最底一行输入命令。

  - **a** -- 进入插入模式，在光标下一个位置开始输入文本。

  - **o**：在当前行的下方插入一个新行，并进入插入模式。

  - **O** -- 在当前行的上方插入一个新行，并进入插入模式。

  - **dd** -- 剪切当前行。

  - **yy** -- 复制当前行。

  - **p**（小写） -- 粘贴剪贴板内容到光标下方。

  - **P**（大写）-- 粘贴剪贴板内容到光标上方。

  - **u** -- 撤销上一次操作。

  - **Ctrl + r** -- 重做上一次撤销的操作。

  - **ESC** -- 退出输入模式

  - **:w** -- 保存文件。

  - **:q** -- 退出 Vim 编辑器。
  - **:wq** -- 保存并退出

  - **:q!** -- 强制退出Vim 编辑器，不保存修改。



##### **echo**-用于在标准输出（通常是终端）显示一行文本或变量的值

* 输出文本

```
echo "Hello, World!"
```

* 输出变量

```
name="Linux User"
echo "Welcome, $name!"
```

* 查看特定环境变量

```
echo $HOME
```

* 重定向将输出保存到文件(>)

```
echo "This will be saved to file" > output.txt
```

​	追加内容到文件(>>)：

```
echo "Additional line" >> output.txt
```

![image-20250708184634189](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250708184634189.png)



##### **cat**-查看和连接文件

* 查看文件内容

```
cat hello.py
```

![image-20250708190804695](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250708190804695.png)

* 合并file1和file2到file3

```
cat file1 file2 > file3
```

* 创建文件功能与追加内容功能同echo



### 查找与搜索

##### **find**-查找文件

##### **grep**-搜索内容

##### **which**-查找命令路径

##### **locate**-快速查找文件



### 系统资源与进程

##### **top**-实时查看系统资源占用（含 CPU、内存、进程）

* 按 `q` 退出

* 按 `P` 按 CPU 占用排序

* 按 `M` 按内存使用排序

##### **free**-查看内存使用情况

`-h`：以人类友好的单位（如 MB、GB）显示

```
free -h
```



