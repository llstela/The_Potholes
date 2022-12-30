# Docker_Potholes 
实验室内的Docker使用简记。


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
## 在Docker上使用Anaconda

下面介绍的方法是从CUDA开始安装Anaconda，搭完环境之后才发现 continuumio/anaconda3 就可以直接用torch+GPU（？有争议），不过该镜像是基于debian，而下面的方法可以获得基于ubuntu的anaconda
1. 使用NVIDIA官方镜像，里面已经帮我们装好了CUDA和cuDNN (选择版本：https://hub.docker.com/r/nvidia/cuda/)

        docker pull nvidia/cuda:11.3.1-cudnn8-runtime-ubuntu20.04

2. 使用乾坤师兄写好的模板docker-compose.yml，按照提示配置Docker相关参数。例如，需要挂载的volume的路径(包括workspace和/gdata)
   
   在服务器如下目录可以找到模板：
    
        /gdata/cold1/project_template/

3. docker-compose相关的操作命令在docker-compose.yml已经给出。

    例如，如下命令启动Docker容器：

        docker-compose up -d

4. 启动Docker容器，默认为root用户。启动Docker容器后，容器内操作和自己平时使用 linux 服务器一样，可以按照自己实验环境的需要安装依赖的库（建议创建一个普通用户，以防你做出不必要的误操作）

5. 在容器内下载Anaconda (Anaconda下载网址：https://repo.anaconda.com/archive/)

   使用wget命令在容器内下载：

       wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh

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
