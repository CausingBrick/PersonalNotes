# Ubuntu自启动脚本&锐捷网络自动连接

## 问题描述

**锐捷网络linux版本每次开机得手动去命令行输入命令连接, 过于麻烦,所以添加自启动脚本.**

## 解决过程

+ 编写启动脚本rjAutostart.sh:
  
    ```
    #! /bin/bash
    sudo /home/causingbrick/Desktop/rjsupplicant/rjsupplicant.sh -d 1  -u xi0350101 -p xi0350101
    ```

* 将其设置为可执行脚本

  >chmod +x rjAutostart.sh

+ 难点在于如何自启动命令中带有sudo命令的脚本,下列给出解决方案:  
 *编辑/etc/sudoers这个文件, 在文件背后加上一行代码*
  >causingbrick ALL = NOPASSWD: /home/causingbrick/rjsupplicant/rjsupplicant.sh

    编辑以后执行该脚本就不用输入sudo即可执行.

 + 添加脚本到自启动项:

   >sudo cp '/home/causingbrick/Desktop/rjsupplicant/rjAutostart.sh'  /etc/init.d

+ 进入启动目录

  >cd /etc/init.d

+ 将启动顺序设置为90,数值越高优先级越低

  >sudo update-rc.d rjAutostart.sh defaults 90

+ 移除脚本

  >sudo update-rc.d -f jAutostart.sh remove
