---
title: 送给mac下的玩户外的小伙伴们
catalog: true
date: 2017-04-03 15:22:30
subtitle: 必应壁纸和8264每日一图for mac
header-img: http://wx4.sinaimg.cn/crop.0.0.800.449.1000/5754d828ly1fdisd5mk98j20m80gotsk.jpg
tags: mac wallpic
---
<div class="main_editor" node-type="articleContent">

<div class="WB_editor_iframe" node-type="contentBody" style="opacity: 1; zoom: 1; user-select: initial;">

一直都很喜欢8264每日一图的震撼，现在利用mac下的shell做了一个每日一图剽窃工具。

脚本运行在自己的机器上好久了，由于选择的两个图片源质量很高，每日看到都会有小小的兴奋。

现在分享给大家。 目前集成了壁纸资源 是8264的每日一图

[http://www.8264.com/list/842/](http://www.8264.com/list/842/)

和

[http://cn.bing.com/的每日壁纸](http://cn.bing.com/的每日壁纸)

## 1:bing脚本 wallpic.sh

#!/bin/sh

./etc/profile 

url=$(expr "$(curl 

[http://cn.bing.com/?mkt=zh-CN](http://cn.bing.com/?mkt=zh-CN)

 |grep hprichbg)" : ".

_g_img={url: \"(._

)\",id.*") 

#提取图片名称

filename=$(expr "${url%<i>*}" : ".*")

#本地图片地址-当前用户下缺省图片目录

localpath="$HOME/Pictures/$filename"

#下载图片至本地

curl -o $localpath $url

#调用Finder应用切换桌面壁纸

osascript -e "tell application \"Finder\" to set desktop picture to POSIX file \"$localpath\""`

## 2:8264脚本 wall8264.sh

#!/bin/sh

#提取壁纸图片URL

./etc/profile

url=$(expr "$(curl http://www.8264.com/list/842/ |grep http://bbs.8264.com/picture- |head -n 1)" : ".*<a href=\"\(.*\)\" target.*")

url=$(expr "$(curl $url |grep link-orimg |head -n 1)")

url=$(expr "${url%<i>*}" : ".*a href=\"\(.*\)\" class=.*")

#提取图片名称

filename=$(expr "$url" : ".*/\(.*\)")

#本地图片地址-当前用户下缺省图片目录

localpath="$HOME/Pictures/$filename"

#下载图片至本地

curl -o $localpath $url

#调用Finder应用切换桌面壁纸

osascript -e "tell application \"Finder\" to set desktop picture to POSIX file \"$localpath\""

## 3：crontab 任务脚本 wallservice.sh

15 10 * * * bash $HOME/归档/script/wallpic.sh

10 14 * * * bash $HOME/归档/script/wall8264.sh

说明：wallservice为任务描述文件，15 10 * * * 指的是每天上午10点15分。可根据需求进行调整。

使用方法： 1、从[https://github.com/happybang/wallpaper4mac下载代码或者是从上面自动创建脚本。](http://web_font.sina.com/zhangfengwan/file/script.zip下载代码或者是从上面自动创建脚本。)
2、修改walservice.sh中引用路径 
3、利用mac中的crontab命令来创建任务 
crontab wallservice.sh

4、可以先单独用bash调用wallpic和wall8264脚本可立即执行。​

原每天都有一个好心情。

必应的壁纸还是挺给力的，但是说实话 8264的每日一图也不输，不过并不是每日都更新。

原大家每日都有好心情。

注：脚本参考https://www.zhihu.com/question/25660659​

</div>

</div>
 