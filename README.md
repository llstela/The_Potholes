# Anaconda_Exp
  觉得自己很有必要记录一下自己经常踩的坑和常用到的资料。
# 常用命令：
    https://blog.csdn.net/ligous/article/details/124209700
# 镜像源的配置：
  不建议使用清华源，同学说总是有很多bug
    https://mirror.tuna.tsinghua.edu.cn/help/anaconda/
  如果无法使用，常常会报HTTPError，可以添加如下命令(但是这样做是否安全有待商榷)
  
    conda config --set ssl_verify false
# 使用时候的注意事项
  使用conda安装的时候一定要把VPN给关了，不然也会出现一堆错误。
  
  遇到问题，首先关闭VPN，再排查错误。
