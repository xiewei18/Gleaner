# ArcGIS Pro（ArcMap 各版本）属性表中文乱码问题解决_AnywalkerGISer 的博客 - CSDN 博客_gis 属性表汉字显示问号
Save From : [ArcGIS Pro（ArcMap 各版本）属性表中文乱码问题解决_AnywalkerGISer 的博客 - CSDN 博客_gis 属性表汉字显示问号](https://blog.csdn.net/qq_24655701/article/details/84944046) 

## Content
在用 Pro 筛选图层字段时，发现属性表发生乱码，于是拿 ArcMap 10.6 一试，也是如此，到底为什么呢？  
![](https://img-blog.csdnimg.cn/20181210173327911.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI0NjU1NzAx,size_16,color_FFFFFF,t_70)
  
借鉴前辈们解决 ArcMap 低版本属性表乱码的问题解决方法，勇敢的尝试了一下 Pro 中的解决方法，其实道理都一样。  
**先来看看第一种方法**：  
打开 CMD，如果是 ArcMap，输入如下命令：

```
reg add HKEY_CURRENT_USER\Software\ESRI\Desktop10.6\Common\CodePage /v dbfDefault /t REG_SZ /d 936 /f

```

Desktop 后面跟的是 ArcGIS 的版本。

如果是 Pro，输入如下命令：

```
reg add HKEY_CURRENT_USER\Software\ESRI\ArcGISPro\Common\CodePage /v dbfDefault /t REG_SZ /d 936 /f

```

**再看看第二种方法**  
这是团队小伙伴找到的一种解决方法，高版本的 ArcMap 会先读取.cpg 文件来判断文件的编码，所以在 shapefile 文件目录下添加 “.cpg” 文件，文本内容为 **oem 或 936**。  
![](https://img-blog.csdnimg.cn/20181210175123123.jpg)
  
_这种方法有个缺点就是对每个 shapefile 都需要添加.cpg 文件。_

**最后看看这两种解决方法的效果**  
![](https://img-blog.csdnimg.cn/20181210180540427.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI0NjU1NzAx,size_16,color_FFFFFF,t_70)
## Note