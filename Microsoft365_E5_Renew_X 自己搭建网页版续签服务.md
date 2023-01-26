# Microsoft365_E5_Renew_X 自己搭建网页版续签服务
Save From : [Microsoft365_E5_Renew_X 自己搭建网页版续签服务](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html) 

## Content
### Microsoft365\_E5\_Renew_X 自己搭建网页版续签服务

*   获取链接
*   Facebook
*   Twitter
*   Pinterest
*   电子邮件
*   其他应用

\-  [  一月 18, 2023  ](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html "permanent link") 

[![](https://blogger.googleusercontent.com/img/a/AVvXsEhLD84GT0Rfz1M7X5rjUE_2BtaPmSKh09oMqQjlDzQYkoC81ISecEz2Lwa1zckcXxej-zefuvFcGNhi3uyZv51yF1FXzciC2q40RLApauuVAQJ_Xkg5XUOejT9_9SiSkTGHEBpa0sVHM7vzRxAGgjbudNkFKNQ5-rAXMQTVzEgC3k63kLHKYM0kMCW3=w640-h314)
](https://blogger.googleusercontent.com/img/a/AVvXsEhLD84GT0Rfz1M7X5rjUE_2BtaPmSKh09oMqQjlDzQYkoC81ISecEz2Lwa1zckcXxej-zefuvFcGNhi3uyZv51yF1FXzciC2q40RLApauuVAQJ_Xkg5XUOejT9_9SiSkTGHEBpa0sVHM7vzRxAGgjbudNkFKNQ5-rAXMQTVzEgC3k63kLHKYM0kMCW3)

  
  

E5 账号大家都白嫖上了吧！

续签服务搭建在自己服务器上或许会安全点。我找了一个 GitHub 上的 docker 搭建方法，结合我自己经验。应该可行，比较简单。

  

  

**买台 VPS**

RN VPS 使用教学（推荐视频）

[https://youtu.be/Eru03pm-_GA](https://youtu.be/Eru03pm-_GA)

科技 lion 推荐的热门 VPS 购买

[https://kejilion.pro/index.php/topVPS/](https://kejilion.pro/index.php/topVPS/)

  

  

**连接 VPS**

买好 VPS 后获取 VPS 的公网 IP 地址

端口默认 22

SSH 连接你的 VPS

  

  

**更新环境**

apt update -y && apt install -y curl && apt install -y socat && apt install wget -y

  

**安装 sudo**

apt-get install sudo

  

**安装 Docker**

sudo apt install docker.io -y && sudo apt install docker-compose

  

**自启动 docker**

sudo systemctl enable --now docker

  

**下载镜像**

docker pull hanhongyong/ms365-e5-renew-x:latest

  

**部署容器**

docker run -d -p 1066:1066 -e TZ=Asia/Shanghai --name ms365  hanhongyong/ms365-e5-renew-x:latest

  

**初始密码**

123456

  

**修改密码**

docker exec -it ms365 /bin/bash

cd Deploy

vim Config.xml

  

输入 i 启动编辑模式

修改密码

输入 esc 退出编辑

:wq! 回车 退出

重启密码才会生效

  

**重启续签服务**

重启服务器后 E5 续签网页不会跟随重启

需要以下命令

docker start ms365

  

**更多 docker 常用命令**

docker ps -a 查看已经创建的容器

docker ps -s 查看已经启动的容器

docker start con\_name 启动容器名为 con\_name 的容器

docker stop con\_name 停止容器名为 con\_name 的容器

docker rm con\_name 删除容器名为 con\_name 的容器

  

**原作者 GitHub 地址**

[https://github.com/hongyonghan/Docker\_Microsoft365\_E5\_Renew\_X](https://github.com/hongyonghan/Docker_Microsoft365_E5_Renew_X)

  

  

  

  

  

  

  

  

*   获取链接
*   Facebook
*   Twitter
*   Pinterest
*   电子邮件
*   其他应用

### 评论

1.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/19/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674106879413#c914335780925860148)
    
    密码呢
    
    [回复](javascript:;)[删除](https://www.blogger.com/delete-comment.g?blogID=8943566632081215369&postID=914335780925860148)
    
    [回复](javascript:;)
    
    [回复](javascript:;)
    
2.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/19/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674107429234#c1119778151782837724)
    
    好像用群晖更简单
    
    [回复](javascript:;)[删除](https://www.blogger.com/delete-comment.g?blogID=8943566632081215369&postID=1119778151782837724)
    
    [回复](javascript:;)
    
    [回复](javascript:;)
    
3.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/22/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674376538040#c1374173635169996971)
    
    能否出一期详细视频啊。。。
    
    [回复](javascript:;)[删除](https://www.blogger.com/delete-comment.g?blogID=8943566632081215369&postID=1374173635169996971)
    
    [回复](javascript:;)
    
    [回复](javascript:;)
    
4.  ![](https://resources.blogblog.com/img/blank.gif)
    
    匿名 [1/22/2023](https://kejilion.blogspot.com/2023/01/microsoft365e5renewx.html?showComment=1674393971966#c2572450637340079980)
    
    感谢分享，不过个人觉得镜像作者的 Github readme 要写得清楚一些
## Note
