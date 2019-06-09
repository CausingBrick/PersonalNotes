# Ubuntu 打不开网易云音乐方法总结

## 方法一

*把版本固定在1.0.这样即可正常使用,后续补充降级方法.*

## 方法二

*点击网易云图标然后点击关机dashboard,停留两三秒即可打开,成功率极高.*

## 方法三

*在bash中输入以下命令即可打开.*
>sudo netease-cloud-music --no-sandbox %U

~~但是这样不方便,故在./.bashrc `or` ./.zshrc 中添加~~
>~~alias music="sudo netease-cloud-music --no-sandbox %U &~~"

~~但是不行,不知道为啥~~

## 方法四(测试无效)

*编辑/usr/share/applications/ netease-cloud-music.desktop文件,在其中把Exec = /the/path/to/netease-cloud-music 改为 Exec=/the/path/to/netease-cloud-music --no-sandbox %U即可.*
>sudo gedit usr/share/applications/ netease-cloud-music.desktop

但是没用

## 方法五 经测试有效!

*添加网易云sudo权限.*
>sudo gedit /etc/sudoers  
causingbrick ALL = NOPASSWD: /usr/bin/netease-cloud-music

*编辑/usr/share/applications/ netease-cloud-music.desktop文件.*
>sudo gedit usr/share/applications/ netease-cloud-music.desktop

 *修改其中的`Exec = /the/path/to/netease-cloud-music` 为 `Exec=sudo netease-cloud-music %U`*

  重启点击完美使用.

## 总结

道路千万条,折腾第一条  
资料不规范,系统两行泪  
除了方法一其他的都不完美;

现在方法五好使了.
