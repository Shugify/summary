[TOC]



# linux的基本使用

[Linux 命令大全 | 菜鸟教程](https://www.runoob.com/linux/linux-command-manual.html)

### 文件与目录操作

##### **mkdir**-创建新目录

```
mkdir test
```

##### **rmdir**-删除目录

```
rmdir test
```

##### **rm**-删除文件/目录

```
rm file.txt
rm -f folder
```

##### **cp**-拷贝文件/目录

```
cp a.txt b.txt
cp -r dir1 dir2
```

##### **mv**-移动或重命名文件

```
mv a.txt newname.txt
```



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



