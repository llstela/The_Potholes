# 服务器常见问题排查
  1. **Q**: 已经在VSCode中下载了Python插件，但是打开python代码依然没有辅助拼写功能。
     
     **A**：可能是当前工作目录下的文件太多，导致插件失灵。[visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc](https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc)
 
  2. **Q**: 为什么没有办法打开Docker？
     
     **A**：可能是当前服务器的存储空间已满，使用如下命令查看服务器的存储余量。
     
          df -h
          
  3. **Q**: VSCODE无法连接服务器？ 

     **A**: 根据个人经验，可能的网络原因如下：① 连接了手机热点。② 一些非正式的WiFi（如 xxx-Guest）。③ 信号差的WiFi。④服务器存储空间已满，无法存放运行vscode额外所需空间。
