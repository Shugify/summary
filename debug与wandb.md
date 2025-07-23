[TOC]





xyy:

1. 你问gpt了解一下vscode在远程服务器上debug的原理. 注意, 这里你去看什么csdn或者知乎那些vscode的python debug教程可能不完全适用. 因为你是在用vscode去远程coding, 实际上就是服务器上装了一个vscode(你第一次用vscode  连接服务器的时候就会说在安装vscode-server), 而你电脑上的vscode只是起到一个前端页面的作用 -> 因此你相当于就是在直接操控服务器上的vscode, 因此要给vscode配置的是服务器的python解释器路径. 

然后你目前要做的就是问一下gpt这个流程是什么, 了解vscode debug的时候的launch.json是干什么用的? (你本科的时候可能用过但是没深入了解过), 然后配置好的conda环境的解释器(而不是系统默认python的或其他的, 你可以用很多命令来看, 包括之前你学会的echo $PATH, 可以具体问一下GPT)
然后创建一个type是debugpy的调试, 开始调试你目前的代码, 实现能断点的功能.

xyy:
lanch.json的说明参考: https://code.visualstudio.com/docs/debugtest/debugging-configuration

xyy:
快速读英文文档的话, 你可以chrome装一个沉浸式浏览的插件, 然后进去设置配置一下openai格式的api, 这里api就是按我上次给你的那种

xyy:
例如: yunwu.ai
充几块钱试试

xyy:
效果:

xyy:
[图片]

xyy:
2. 看wandb官方文档, 学会怎么用wandb:
https://wandb.ai/site/

然后实现把训练过程的loss, 还有训练中的训练图片(部分就行)保存到wandb



## vscode在远程服务器上debug

### **解释器与调试器(debug)**

- 解释器是一种计算机程序，用于将源代码逐行解释成计算机可执行的指令
- **解释器是执行者**：它始终是最终负责运行代码的那个核心程序。
- **调试器是控制者**：它本身不运行代码，而是像一个“提线木偶”的操作者，通过向解释器发送指令（暂停、继续、查询状态等）来控制代码的执行流程。当你启动调试时，实际上是调试器启动并接管了解释器。




### **launch.json 的作用：调试的“启动说明书”**

launch.json 文件是VS Code调试功能的核心配置文件。它位于项目工作区的 .vscode 文件夹下。

它的作用是**告诉VS Code的调试器（Debugger）如何准备和启动一个调试会话（Debug Session）**。它写明了：

- 要调试的主程序文件是哪一个，例如 ${workspaceFolder}/main.py。 ${workspaceFolder} 是一个非常有用的变量，它代表你当前在VS Code中打开的项目根目录。
- 使用哪种类型的调试器。对于Python，我们现在使用的标准调试器是 **debugpy**。
- 两种主要模式：
  - launch：这是最常用的模式。VS Code会为你**启动**指定的程序，并自动附加调试器。
  - attach：用于附加到一个**已经运行**的进程上。比如你有一个已经启动的Web服务器，你想中途接入进去进行调试。
- **其他配置（configurations）**：launch.json 文件可以包含一个或多个调试配置，它们都放在一个名为 configurations 的数组里。这允许你为一个项目设置多种调试场景（比如，一个用于调试主文件，一个用于调试单元测试）。
  - name：给这个调试配置起一个人类可读的名字，它会显示在调试面板的下拉菜单里。
  - console：指定调试时代码的输出位置，例如 integratedTerminal 表示使用VS Code的集成终端。
  - python：可以显式指定用于本次调试的Python解释器路径。**虽然可以设置，但最佳实践是使用VS Code的“选择解释器”功能，让其自动应用**。





### **实战流程：在远程服务器上配置并启动Debug**

以下是在远程服务器上，针对特定的Conda环境，创建并启动调试会话的完整步骤。

#### **第1步：确保已连接到服务器并打开项目文件夹**

通过VS Code的 "Remote-SSH" 插件连接到你的服务器，并打开你的项目代码所在的文件夹。

#### **第2步：为VS Code选择正确的Conda环境解释器**

这是最关键的一步，目的是让 vscode-server 知道应该用哪个Python来运行和调试你的代码。

1. **打开命令面板**：使用快捷键 Ctrl+Shift+P (或者 Cmd+Shift+P on Mac)。
2. **选择解释器**：输入 Python: Select Interpreter 并回车。
3. **选择你的Conda环境**：VS Code通常会自动检测到服务器上的Conda环境。你应该能从列表中看到类似 ('my-conda-env':conda) 的选项。直接选择它。

**如果VS Code没有自动找到你的环境，你需要手动提供解释器路径：**

1. **在服务器终端中找到路径**：
   - 首先，激活你的Conda环境：conda activate your_env_name
   - 然后，找出该环境下python可执行文件的确切位置：which python
   - 这会输出一个绝对路径，例如：/home/your_username/miniconda3/envs/your_env_name/bin/python。**这个路径就是我们需要的。**
   - *关于 echo $PATH*：这个命令会显示当前shell环境下所有可执行文件的搜索路径。当你激活Conda环境后，你会看到Conda环境的 bin 目录被添加到了 $PATH 的最前面，这就是为什么你可以直接输入 python 就能启动正确解释器的原因。which python 正是利用了这个$PATH来帮你找到第一个匹配到的python可执行文件。
2. **在VS Code中输入路径**：回到 "Select Interpreter" 列表，选择 "Enter interpreter path..."，然后将刚刚复制的完整路径粘贴进去。

完成这一步后，VS Code右下角状态栏会显示你已选定的Conda环境。之后的所有终端创建、代码运行和调试都会默认使用这个解释器。

#### **第3步：创建launch.json并配置debugpy**

1. **切换到“运行和调试”视图**：点击VS Code左侧活动栏的“播放带虫子”图标。
2. **创建配置文件**：如果项目里没有 launch.json，你会看到一个 "create a launch.json file" 的链接。点击它。
3. **选择调试器**：在弹出的选择框中，选择 **"Python"**。
4. **选择配置模板**：在下一个选择框中，选择 **"Python File"**。

VS Code会自动在 .vscode/launch.json 中为你生成一个默认配置，如下所示：

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: 当前文件", // 这个名字会显示在调试下拉菜单中
            "type": "debugpy",          // 指定使用debugpy调试器
            "request": "launch",        // 采用“启动”模式
            "program": "${file}",       // 关键：${file}变量表示当前你激活的那个编辑器窗口里的文件
            "console": "integratedTerminal" // 在集成终端中显示输出
        }
    ]
}```

**这个默认配置对于调试单个文件非常方便。** 如果你想调试一个固定的入口文件（比如`main.py`），可以把 `"program": "${file}"` 修改为 `"program": "${workspaceFolder}/main.py"`。
```

`"type"` 是 launch.json 文件中**最核心、最基本**的字段。它告诉 VS Code 你想要调试的是哪种类型的程序，以及应该调用哪个**调试扩展**来完成这项工作。

`"type": "debugpy"`：用于调试 Python 代码的标准类型



#### **第4步：设置断点并开始调试**

1.  **设置断点**：在你的Python代码文件中，在你想要暂停执行的行号左侧单击，会出现一个红点，这就是断点。
2.  **启动调试**：
    *   确保顶部的调试配置下拉菜单选择了你想要的配置（例如 "Python: 当前文件"）。
    *   按下 `F5` 键，或者点击配置旁边的绿色播放按钮。

现在，`vscode-server` 会在服务器上使用你选定的Conda环境的Python解释器来运行你的脚本。当代码执行到你设置的断点时，程序会暂停。此时，你本地的VS Code界面会同步显示暂停状态，你可以在左侧的调试面板中查看变量、调用堆栈，并使用调试工具栏（继续、单步跳过、单步进入等）来控制程序的执行。



## Wandb的使用

[W&B 快速入门 |权重和偏差文档](https://docs.wandb.ai/quickstart/)

#### 1. 安装 wandb

首先，确保已经安装了 wandb 库。

注意激活conda环境后安装，wandb可被conda虚拟环境隔离

```
pip install wandb
```



#### 2. 登录 wandb

在终端或中运行以下命令。会提示登录自己的 wandb 账户。如果还没有账户，可以去官网免费注册一个，并输入密钥。

```
wandb login
```



#### 3. (可选)通过环境变量进行身份验证

1. **获取密钥**：
   前往 [https://wandb.ai/authorize](https://www.google.com/url?sa=E&q=https%3A%2F%2Fwandb.ai%2Fauthorize) 页面，复制 API 密钥。假设它长这个样子：abcdef1234567890abcdef1234567890abcdef12。

2. **在终端中设置**：
   在终端（例如，正在使用的 (sjjenv) root@... 提示符下）输入以下命令，然后按 Enter。

   ```
   # 推荐将密钥用引号括起来，以避免特殊字符引起的问题
   export WANDB_API_KEY="abcdef1234567890abcdef1234567890abcdef12"
   ```

3. **验证（可选）**：
   您可以输入以下命令来检查环境变量是否设置成功：

   ```
   echo $WANDB_API_KEY
   ```

   如果它打印出了密钥，说明设置成功。

4. **运行您的脚本**：
   现在，您可以直接运行您的 Python 脚本，**无需事先运行 wandb login**。

   ```
   python train.py
   ```

   当脚本执行到 wandb.init() 时，它会自动检测到 WANDB_API_KEY 这个环境变量，并用它来完成登录和认证。

| 特性         | wandb login (交互式登录)                     | export WANDB_API_KEY (环境变量)                              |
| ------------ | -------------------------------------------- | ------------------------------------------------------------ |
| **操作方式** | 需要手动运行命令并粘贴密钥                   | 在运行脚本前设置一次，或写入配置文件`~/.bashrc`              |
| **适用场景** | 适合在您自己的本地开发机上进行一次性设置     | **极度适合自动化环境**：服务器、Docker容器、CI/CD流水线      |
| **安全性**   | 密钥保存在本地的 .netrc 文件中               | **更好**。密钥不会被硬编码在代码或笔记本中，只存在于环境中   |
| **便捷性**   | 每次换环境（如新的Docker容器）都需要重新登录 | 只需在启动环境时设置一次，所有脚本自动生效，**无需修改代码** |



#### 4. 修改 PyTorch 脚本

在代码中添加几行 wandb 相关的指令：

1. **import wandb**: 导入库。
2. **wandb.init()**: 在训练开始前初始化一个新的 wandb run。这里可以指定项目名称、run的名称以及所有希望记录的超参数。
3. **wandb.config**: 将重要的超参数（如学习率、batch size、模型架构等）保存到 wandb.config 对象中。
4. **wandb.log()**: 在训练循环中，使用此函数来记录需要的指标，例如 loss 和 accuracy。wandb.log 需要一个字典作为参数。
5. **wandb.Image()**: 为了记录图片，需要将 PyTorch 的 Tensor 转换为 wandb.Image 对象，然后通过 wandb.log() 上传。
6. **wandb.finish()**: (可选) 在脚本结束时，调用此函数来标记 run 已完成。通常脚本正常退出时 wandb 会自动处理。

### 修改后的完整代码

这是修改后的完整代码。请注意新增和修改的部分。

Generated python

```
import os
import torch
import torch.nn as nn
import torch.optim as optim
from torchvision import datasets, models, transforms
from torch.utils.data import DataLoader
import wandb # 导入wandb

# ---------- 路径配置 ----------
data_dir = 'dataset'
model_dir = 'model'
os.makedirs(model_dir, exist_ok=True)

# ---------- 使用GPU ----------
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
print("Using device:", device)

# ---------- 定义超参数 (方便wandb记录) ----------
config = {
    "learning_rate": 1e-4,
    "batch_size": 4,
    "num_epochs": 10,
    "architecture": "ResNet-18"
}

# ---------- wandb 初始化 ----------
# 1. 开始一个新的 wandb run 来跟踪这个实验
wandb.init(
    project="pytorch-catdog-classification", # 在wandb中显示的项目名称
    config=config # 传入超参数字典
)

# ---------- 数据预处理 ----------
# 注意：为了能正确显示图片，我们从[0.5, 0.5, 0.5]反归一化回[0, 1]
def denormalize(tensor):
    return tensor * 0.5 + 0.5

data_transforms = {
    'train': transforms.Compose([
        transforms.Resize((224, 224)),
        transforms.RandomHorizontalFlip(),
        transforms.ToTensor(),
        transforms.Normalize([0.5]*3, [0.5]*3)
    ]),
    'val': transforms.Compose([
        transforms.Resize((224, 224)),
        transforms.ToTensor(),
        transforms.Normalize([0.5]*3, [0.5]*3)
    ]),
}

# ---------- 加载数据 ----------
batch_size = wandb.config.batch_size # 从wandb.config中获取batch_size
image_datasets = {
    x: datasets.ImageFolder(os.path.join(data_dir, x), data_transforms[x])
    for x in ['train', 'val']
}
dataloaders = {
    x: DataLoader(image_datasets[x], batch_size=batch_size, shuffle=True)
    for x in ['train', 'val']
}
dataset_sizes = {x: len(image_datasets[x]) for x in ['train', 'val']}
class_names = image_datasets['train'].classes
print("Classes:", class_names)

# ---------- 构建模型 ----------
model = models.resnet18(pretrained=True)
model.fc = nn.Linear(model.fc.in_features, len(class_names))
model = model.to(device)

# ---------- 损失和优化器 ----------
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=wandb.config.learning_rate) # 从wandb.config获取学习率

# ---------- 训练函数 ----------
def train_model(model, criterion, optimizer, num_epochs=10):
    # 告诉wandb开始监控模型
    wandb.watch(model, criterion, log="all", log_freq=10)
    
    for epoch in range(num_epochs):
        print(f"\nEpoch {epoch+1}/{num_epochs}")
        print("-" * 30)

        for phase in ['train', 'val']:
            if phase == 'train':
                model.train()
            else:
                model.eval()

            running_loss, running_corrects = 0.0, 0

            for i, (inputs, labels) in enumerate(dataloaders[phase]):
                inputs, labels = inputs.to(device), labels.to(device)

                optimizer.zero_grad()
                with torch.set_grad_enabled(phase == 'train'):
                    outputs = model(inputs)
                    _, preds = torch.max(outputs, 1)
                    loss = criterion(outputs, labels)

                    if phase == 'train':
                        loss.backward()
                        optimizer.step()

                running_loss += loss.item() * inputs.size(0)
                running_corrects += (preds == labels).sum().item()

                # 在每个epoch的第一个batch记录训练图片
                if phase == 'train' and i == 0:
                    # 反归一化并转换为wandb.Image格式
                    log_images = [wandb.Image(denormalize(img.cpu()), caption=f"Pred: {class_names[pred]}, Truth: {class_names[truth]}")
                                  for img, pred, truth in zip(inputs, preds, labels)]
                    # 记录图片到wandb
                    wandb.log({"Training Images": log_images}, step=epoch)

            epoch_loss = running_loss / dataset_sizes[phase]
            epoch_acc = running_corrects / dataset_sizes[phase]
            print(f"{phase.capitalize()} Loss: {epoch_loss:.4f}  Acc: {epoch_acc:.4f}")

            # 使用 wandb.log() 记录 loss 和 accuracy
            # 我们将训练和验证指标分开记录，方便在图表中对比
            log_data = {
                f"{phase}_loss": epoch_loss,
                f"{phase}_accuracy": epoch_acc
            }
            # 使用epoch作为x轴
            wandb.log(log_data, step=epoch)

    return model

# ---------- 启动训练 ----------
model = train_model(model, criterion, optimizer, num_epochs=wandb.config.num_epochs)

# ---------- 保存模型 ----------
model_path = os.path.join(model_dir, "resnet18_catdog.pth")
torch.save(model.state_dict(), model_path)
print("Model saved to:", model_path)

# (可选) 标记run结束
wandb.finish()
```



### 如何运行和查看结果

1. **准备数据集**：确保您的 dataset 文件夹下有 train 和 val 子文件夹，并且每个子文件夹下都有按类别分的图片（例如 cat 和 dog 文件夹）。

2. **运行脚本**：直接运行修改后的 Python 脚本。

   ```
   python train.py
   ```

3. **查看结果**：脚本开始运行时，终端会输出一个 wandb 的链接。复制此链接到您的浏览器中打开，即可实时查看您的实验仪表盘。您会看到：

   - **Charts** 面板中自动生成的 train_loss, val_loss, train_accuracy, val_accuracy 随 epoch 变化的图表。
   - **Media** 面板中您上传的训练图片，以及它们的预测标签和真实标签。
   - **Config** 或 **Overview** 页面记录的超参数。



### wandb 文件夹

运行后出现的wandb 文件夹是 Weights & Biases 在您本地机器上创建的**工作目录和缓存区**

* **容错与鲁棒性 (Resilience)**：如果您的网络突然中断，或者 wandb.ai 服务器暂时无法访问，您的训练脚本**不会崩溃**。所有的数据（如 loss, accuracy）会先被安全地写入这个本地文件夹。wandb 的后台进程会稍后在网络恢复时，继续尝试上传数据，确保数据不丢失。
* **性能 (Performance)**：将数据写入本地磁盘远比通过网络发送要快得多。wandb 将记录数据的操作（写入本地文件）和上传数据的操作（发送到云端）分离，变成一个**异步过程**。这可以确保频繁调用 wandb.log() 不会因为网络延迟而拖慢您的训练主进程。
* **离线支持 (Offline Mode)**：您可以完全在没有网络的环境下运行训练（例如，在 wandb.init(mode="offline") 模式下）。所有实验数据都会被完整地保存在这个本地文件夹中。当您回到有网络的环境时，只需一条命令 (wandb sync) 就可以将所有离线实验上传到云端。

**它是缓存/生成数据**，应该将wandb文件夹添加到 **.gitignore** 文件中，不要将它提交到 Git 版本控制中

在项目根目录下创建 .gitignore文件，并添加wandb/

```
(sjjenv) (base) root@d0b8c8082bbd:~/sjj/test# vim .gitignore
#文件内容：
test/wandb/
```



