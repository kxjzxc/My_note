tags:: #教程

- 安装docker插件和remote-container
-
- 无法连接docker
  普通用户增加到docker组中
  ```bash
  sudo groupadd docker          
  sudo gpasswd -a $USER docker  
  newgrp docker                 
  ```