# StartUbuntu
    从这里快速开启你的Ubuntu之旅
    
## 镜像源
推荐使用 北京外国语大学 的镜像，无论是conda、ubuntu、pypi的镜像源都很可靠：
https://mirrors.bfsu.edu.cn/

## vim 中文乱码问题
    
    vim /etc/vim/vimrc
    
添加如下内容：

    set fileencodings=utf-8,gb2312,gbk,gb18030
    set termencoding=utf-8
    set encoding=prc
