# Anaconda_Exp
  觉得自己很有必要记录一下自己经常踩的坑和常用到的资料。
# 常用命令：
    https://blog.csdn.net/ligous/article/details/124209700
# 镜像源的配置：
  **不建议使用清华源**，自己和周围人对清华源的体验都是说有很多坑.
  2022.10.10: 尝试使用BFSU的镜像源，目前体验良好。
  
    channels:
      - defaults
    show_channel_urls: true
    default_channels:
      - https://mirrors.bfsu.edu.cn/anaconda/pkgs/main
      - https://mirrors.bfsu.edu.cn/anaconda/pkgs/r
      - https://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
    custom_channels:
      conda-forge: https://mirrors.bfsu.edu.cn/anaconda/cloud
      msys2: https://mirrors.bfsu.edu.cn/anaconda/cloud
      bioconda: https://mirrors.bfsu.edu.cn/anaconda/cloud
      menpo: https://mirrors.bfsu.edu.cn/anaconda/cloud
      pytorch: https://mirrors.bfsu.edu.cn/anaconda/cloud
      pytorch-lts: https://mirrors.bfsu.edu.cn/anaconda/cloud
      simpleitk: https://mirrors.bfsu.edu.cn/anaconda/cloud
  如果无法使用，常常会报HTTPError，可以添加如下命令(但是这样做是否安全有待商榷)
# 关于使用conda install奇奇怪怪的报错
  一键重开(**真的救了我大命，不然真的要麻了...**)：
  
    conda install anaconda-clean
    anaconda-clean --yes
    conda update --all
    
   对于HTTPS的问题可以尝试：
   
    conda config --set ssl_verify false
# 使用时候的注意事项
  使用conda安装的时候一定要把VPN给关了，不然也会出现一堆错误。
  
  遇到问题，首先关闭VPN，再排查错误。
