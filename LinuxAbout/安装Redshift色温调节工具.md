 


*以前一直使用f.lux色温调节工具，但是发现在Ubuntu台式机上安装f.lux后程序不能调节色温，查了很多资料都没有说怎么解决这个问题，随访期。。。但是长期看电脑还是应该要一个屏幕调节色温的工具，就找到了一个替代品——————Redshift——————能够与f.lux达到相同的效果。下面写一下安装配置步骤供参考：*



## 安装
> #只安装Redshift发现没有界面，所以安装了三个包  
$ sudo apt install gtk-redshift redshift   python-appindicator  
#执行  
$ gtk-redshift 


+ 也可以直接搜索应用redshift执行：   
执行后选择Autostart。

## 配置
1. 手动将经纬度设定在’39.92:116.46’（北京），并且调整白天色温为 5500K，夜晚 4500K:
>redshift-gtk -l 39.92:116.46 -t 5500:4500
生成配置文件
>sudo gedit ~/.config/redshift.conf

1. 在文件中加入以下内容，可以根据自己的需求更改相应的配置（其中经纬度北京）：

```
[redshift]
; 白天屏幕温度
temp-day=7000
; 夜晚屏幕温度
temp-night=3500
; 昼夜是否平滑过度(1/0)
transition=1

; 位置提供方式(redshift -l list)
location-provider=manual

[manual]
; 位置提供方式设置
; 经纬度(深圳)

lat=22.5410800000
lon=113.9394000000
```
