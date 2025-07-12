# 小结(关于VPN+连远程服务器)，主要在VScode中操作

* 已生成了公钥和私钥，并且公钥已上传服务器

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```



* 挂VPN好连机子（校内就不需要了，VPN看情况需要更改）

* 下载zerotier，ZeroTier 默认是开机自动启动的，然后根据 xubiaolin/docker-zerotier-planet: 一分钟私有部署zerotier-planet服务](https://github.com/xubiaolin/docker-zerotier-planet) 操作；（以下操作对应Windows系统， Linux和MacOS见网址）

  * 加入网络

    ```
    PS C:\Windows\system32> zerotier-cli.bat join 网络id
    200 join OK
    ```

  * 验证链接，看到有一个 `PLANET` 和 `LEAF` 角色，连接方式均为 `DIRECT`（直连），就加入网络成功了！

    ```
    PS C:\Windows\system32> zerotier-cli.bat peers
    200 peers
    <ztaddr>   <ver>  <role> <lat> <link> <lastTX> <lastRX> <path>
    fcbaeb9b6c 1.8.7  PLANET    52 DIRECT 16       8994     1.1.1.1/9993
    fe92971aad 1.8.7  LEAF      14 DIRECT -1       4150     2.2.2.2/9993
    ```

  * ping 服务器IP查看是否成功连上网络

    ```
    C:\WINDOWS\System32>ping 10.177.60.157
    
    正在 Ping 10.177.60.157 具有 32 字节的数据:
    来自 10.177.60.157 的回复: 字节=32 时间=222ms TTL=64
    来自 10.177.60.157 的回复: 字节=32 时间=56ms TTL=64
    来自 10.177.60.157 的回复: 字节=32 时间=57ms TTL=64
    来自 10.177.60.157 的回复: 字节=32 时间=61ms TTL=64
    
    10.177.60.157 的 Ping 统计信息:
        数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
    往返行程的估计时间(以毫秒为单位):
        最短 = 56ms，最长 = 222ms，平均 = 99ms
    ```

  * ssh超时时也可以尝试ping一下

    <img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250707210420030.png" alt="image-20250707210420030" style="zoom:67%;" />

  * 查看网络给主机分配的虚拟地址

    ```
    C:\WINDOWS\System32>zerotier-cli.bat listnetworks
    200 listnetworks <nwid> <name> <mac> <status> <type> <dev> <ZT assigned ips>
    200 listnetworks a48c5976d1f21fc6 xyy_net c6:23:09:c8:ff:f3 OK PUBLIC ethernet_32777 192.168.101.247/24
    ```

  * 查看clash是否影响zerotier，ping一下主机 （方便使用GPT，若未通过本地回环测试，建议百度一下）

    ```
    C:\WINDOWS\System32>ping 192.168.101.247
    
    正在 Ping 192.168.101.247 具有 32 字节的数据:
    来自 192.168.101.247 的回复: 字节=32 时间<1ms TTL=128
    来自 192.168.101.247 的回复: 字节=32 时间<1ms TTL=128
    来自 192.168.101.247 的回复: 字节=32 时间<1ms TTL=128
    来自 192.168.101.247 的回复: 字节=32 时间<1ms TTL=128
    
    192.168.101.247 的 Ping 统计信息:
        数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
    往返行程的估计时间(以毫秒为单位):
        最短 = 0ms，最长 = 0ms，平均 = 0ms
    ```

* 连接成功后可以在自己电脑的~/.ssh文件夹里配置一下config，（VScode上实现）

  ```
  #配置名，fdu-fvl-远程服务器
  Host my-server
      HostName 10.176.42.8
      Port 20052
      User root
      IdentityFile C:\Users\SHI\.ssh\id_rsa
  ```

* 然后就可以连接远程主机了（由于配置了config文件，可以直接ssh config中的远程主机别名）

```
PS C:\Users\SHI\.ssh> ssh -i C:\Users\SHI\.ssh\id_rsa -p 20052 root@10.176.42.8
PS C:\Users\SHI\.ssh> ssh my-server
```

<img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250707211746287.png" alt="image-20250707211746287" style="zoom:67%;" />

* (base)表示已经安装了conda
* 在VScode中下载插件Remote-SSH可以打开远程服务器页面（感觉有点慢，可能是VPN的原因）

<img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250707212348824.png" alt="image-20250707212348824" style="zoom:67%;" />

* 一般拿到一台机器，先看看这个机器的配置, 之后去公司或者是读研读博期间拿到其他机器同理

  * 是看什么卡 (或者是pip install 了 gpustat, 可以直接执行gpustat)

    ```
    (base) root@d0b8c8082bbd:~# nvidia-smi
    ```

    <img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250707214337305.png" alt="image-20250707214337305" style="zoom:67%;" />

    - 当前在 **容器内** 运行（根据GPU利用率等信息推出，不准确）

    - 容器能访问GPU资源：8 张 RTX 3090，每张 24GB

    - GPU 状态一切正常，处于**空闲状态（无进程使用）**。

    - 每张卡只有 `1MiB` 被系统初始化使用，没有训练任务占用。
    - 说明重点字段：

  | 字段               | 含义                                                         |
  | ------------------ | ------------------------------------------------------------ |
  | **GPU Name**       | 显示你每张卡的型号，如 `NVIDIA GeForce RTX 3090`             |
  | **Memory-Usage**   | 每张 GPU 使用显存的情况，当前为 1MiB/24576MiB，表示未运行任何深度学习任务 |
  | **GPU-Util**       | GPU 的当前利用率，都是 0% 表示空闲                           |
  | **Driver Version** | 当前驱动版本为 `555.42.02`                                   |
  | **CUDA Version**   | 支持的 CUDA 版本是 `12.5`，用于加速 PyTorch / TensorFlow 等计算 |
  | **Processes**      | 没有任何正在使用 GPU 的进程（No running processes found）    |

  * 这个机器是裸金属机还是容器(意味着你搞坏的后果，裸金属机就是类似你搞坏了这个机器真正的系统也坏了，容器/虚拟机就是你懂得, 大部分东西都是可以乱搞的 (感觉用多了可以经验判断)

    * 判断容器或金属机: ` cat /proc/1/cgroup`

      容器内会出现关键词：`docker`、`containerd`、`lxc`、`kubepods`

      裸金属机或普通虚拟：只会显示 `/`

      <img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250707215051094.png" alt="image-20250707215051094" style="zoom:67%;" />

    * 判断容器: `ls /.dockerenv` 

      有结果 → 在 Docker 容器中；	无结果 → 通常不是容器（但不是 100% 准确）。

    <img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250707215150324.png" alt="image-20250707215150324" style="zoom:80%;" />

    * 判断容器: 主机名是一长串十六进制字符，很可能是 Docker 容器自动生成的名字

    * 判断裸金属机: `systemd-detect-virt`

      输出 `none` → 通常是裸金属机（也可能是没有启用虚拟化信息的虚拟机）

      输出 `docker` / `lxc` / `containerd` → 容器

      输出 `kvm` / `vmware` / `hyperv` → 虚拟机

      <img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250707215635797.png" alt="image-20250707215635797" style="zoom:80%;" />

  * 确认东西能放哪，这个要问人

* 然后就可以按照需要使用这个机子啦！

