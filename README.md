# The_Potholes
本文档建立之目的在于记录自己踩过的坑。往今后不再犯，或者在跳坑前先做观望。

## 关于Docker
请看这个文档：
[Docker_Potholes](https://github.com/llstela/The_Potholes/blob/main/Docker_Potholes.md)
## 关于Anaconda
请看这个文档：
[Anaconda_Potholes](https://github.com/llstela/The_Potholes/blob/main/Anaconda_Potholes.md)

## 各种官方文档
众里寻他千百度，不如看官方文档：
[Official Doc](https://github.com/llstela/The_Potholes/blob/main/OfficialDoc.md)

## tmux 常用指令
连接服务器常用：
[Tmux_CMD](https://github.com/llstela/The_Potholes/blob/main/tmux_cmd.md)

## 镜像源
推荐使用 北京外国语大学 的镜像，无论是conda、ubuntu、pypi的镜像源都很可靠：
https://mirrors.bfsu.edu.cn/

## vim 中文乱码问题
    
    vim /etc/vim/vimrc
    
添加如下内容：

    set fileencodings=utf-8,gb2312,gbk,gb18030
    set termencoding=utf-8
    set encoding=prc
