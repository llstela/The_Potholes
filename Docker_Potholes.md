# Docker_Potholes 
实验室内的Docker使用简记。

## OpenCV报错

1. 在Docker使用OpenCV (e.g. opencv-python==4.6.0.66)可能会遇到如下报错

            from .cv2 import *
            ImportError: libGL.so.1: cannot open shared object file: No such file or directory
   
   这是因为Docker缺少了OpenCV的依赖，运行如下命令：
   
               apt update && apt install libgl1
      
2. 另外一个错误：

                libgthread-2.0.so.0: cannot open shared object file
      
   运行如下命令：
 
               apt install libglib2.0-0

3. 组合处理上述命令：

               apt update && apt install libgl1 -y && apt install libglib2.0-0 -y
    
## 常用pytorch镜像选取

"pytorch/pytorch"镜像只是构建了PyTorch的环境，不构建CUDA。因此如果物理机上的CUDA版本与PyTorch不匹配。将不能正常运行代码。

"nvcr.io/nvidia/pytorch:xx.yy-py3"包括了CUDA的构建，可能可以跑一些古老的代码。

推荐使用2个常用的镜像。

Docker镜像网站上的pytorch/pytorch镜像，例如：

            pytorch/pytorch:1.13.1-cuda11.6-cudnn8-devel  # 尾缀有devel,runtime, 如果出现库装不上的情况，建议尝试devel
            
来自NVIDIA的nvcr.io/nvidia/pytorch镜像，例如：

            nvcr.io/nvidia/pytorch:23.04-py3  # 根据不同的环境需求，替换23.04为xx.xx
            
NVIDIA不同版本镜像对应的配置信息：

            https://docs.nvidia.com/deeplearning/frameworks/support-matrix/index.html#framework-matrix-2022
            
NVIDIA镜像使用教程：

            https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch
            
其他镜像，访问Docker官方镜像网站：
      
      https://hub.docker.com/
            
## 常用Docker命令

对镜像的操作：

      (不建议使用docker run，建议使用docker-compose up -d)
      docker run -p 10789:22  -it --name="sxh_conda_1131" --runtime=nvidia -v ~/coding_docker:/coding 3fb93e546a31 /bin/bash  # 实例化 --runtime=nvidia
      docker image rm
      docker images
      docker-compose up -d

对容器的操作：

      docker start sxh_conda_1131
      docker stop sxh_conda_1131
      docker attach sxh_conda_1131
      docker rm
      docker cp # 在容器和物理机之间搬运资源
      docker-compose exec ${容器名} bash
      
 查看Docker内部版本号：
            
      cat /etc/issue 
## 在Docker上搭建Code Server
      http://www2.scut.edu.cn/huanghan/2021/1021/c9791a448046/page.htm
## 从CUDA开始安装Anaconda

1. 使用CUDA镜像，里面已经帮我们装好了CUDA和cuDNN (选择版本：https://hub.docker.com/r/nvidia/cuda/ )。 
**组里服务器上已经有很多pytorch相关的镜像，这一步可以跳过。**

        docker pull nvidia/cuda:11.3.1-cudnn8-runtime-ubuntu20.04

2. 使用乾坤师兄写好的模板docker-compose.yml，按照提示配置Docker相关参数。例如，需要挂载的volume的路径(包括workspace和/gdata)
   
   在服务器如下目录可以找到模板：
    
        /gdata/cold1/project_template/

3. docker-compose相关的操作命令在docker-compose.yml已经给出。

    例如，如下命令启动Docker容器：

        docker-compose up -d

4. 启动Docker容器，默认为root用户。启动Docker容器后，容器内操作和自己平时使用 linux 服务器一样，可以按照自己实验环境的需要安装依赖的库（建议创建一个普通用户，以防你做出不必要的误操作）

5. 在容器内下载Anaconda (Anaconda下载网址：https://repo.anaconda.com/archive/)。
**如果你本来已经用的是pytorch的镜像，里面已经安装好了anaconda。**

   使用wget命令在容器内下载：

       wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
6. 如何在打开 终端terminal 的同时自动启动anaconda：

   在命令行输入：
   
            conda init

## 在物理机上对Docker容器挂载的文件夹内容做修改

在 Docker 容器中，/workplace 一般直接挂载了物理机上的某个目录(例如：coding_docker/)。这个时候会发现 coding_docker/ 的所属用户和所属用户组都变为了root。也就意味着我们在物理机上没有办法修改 coding_docker/ 中的文件。

我们可以进入Docker容器，使用Docker容器中的root账户修改 /workplace 的访问权限。

## 在个人电脑上，使用VSCode直接连接Docker容器

进入VSCode中的扩展商店，安装如下扩展插件

    Docker
    Remote Development

进入Docker或Remote的插件页面，选择对应容器，就可以用VSCode打开它。

## 参考资料：
1. Docker中安装Anaconda：

        https://www.cnblogs.com/xiaoli1996/p/15959469.html
        
2. Docker官方文档：

        https://docs.docker.com/
      
3. Docker中文文档：

        https://yeasy.gitbook.io/docker_practice/

4. 菜鸟编程文档：
            
        https://www.runoob.com/docker/docker-tutorial.html
