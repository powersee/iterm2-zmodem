# 项目介绍

在mac下，实现与服务器进行便捷的文件上传和下载操作


# 步骤

1.安装支持rz和sz命令的lrzsz：`brew install lrzsz`

> 等了挺长时间的。

补充：服务器安装（以 Ubuntu 为例）：`apt-get install lrzsz`



2.在本地/usr/local/bin/目录下保存iterm2-send-zmodem.sh 和iterm2-recv-zmodem.sh两个脚本

3.设置一下两个脚本的权限，给予可执行权限

```bash
chmod a+x /usr/local/bin/iterm2-*
```

4.设置Iterm2的Tirgger特性，profiles->default->editProfiles->Advanced中的Tirgger

添加两条trigger，分别设置 Regular expression，Action，Parameters，Instant如下：

```
1.第一条
        Regular expression: rz waiting to receive.\*\*B0100
        Action: Run Silent Coprocess
        Parameters: /usr/local/bin/iterm2-send-zmodem.sh
        Instant: checked
2.第二条
        Regular expression: \*\*B00000000000000
        Action: Run Silent Coprocess
        Parameters: /usr/local/bin/iterm2-recv-zmodem.sh
        Instant: checked
```

![如图](https://github.com/powersee/iterm2-zmodem/blob/master/imgs/01.png)

完成之后，用 ssh 连接服务器后，输入 `rz` 就会跳出一个窗口让我们选择文件传入到服务器里。
而想要把文件从服务器下载到电脑，可以用 `sz filename`

```
➜  ~ sz test.txt
**B00000000000000
➜  ~
➜  ~ # Sent -> /Users/name/Documents/
```
