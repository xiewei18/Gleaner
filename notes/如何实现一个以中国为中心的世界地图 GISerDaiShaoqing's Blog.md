# 如何实现一个以中国为中心的世界地图 | GISerDaiShaoqing's Blog
save from: [如何实现一个以中国为中心的世界地图 | GISerDaiShaoqing's Blog](https://gisersqdai.top/2017/11/14/%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E4%BB%A5%E4%B8%AD%E5%9B%BD%E4%B8%BA%E4%B8%AD%E5%BF%83%E7%9A%84%E4%B8%96%E7%95%8C%E5%9C%B0%E5%9B%BE/) 

## Content 

最近屡屡有小伙伴为各种目的在询问有没有中国位于中心的世界地图。在某位同学的强烈要求下，我决定稍微记录下这个以我大中华为中心的世界地图的做法。效果图：

[![](http://blog.gisersqdai.top/15855136767897p7w4zvv.png)
](http://blog.gisersqdai.top/15855136767897p7w4zvv.png)

原始数据。

[![](http://blog.gisersqdai.top/15855132181209g9wzv8p.png)
](http://blog.gisersqdai.top/15855132181209g9wzv8p.png)

第一种就简单介绍下ArcGIS平台上如何操作吧。

首先在ArcGIS软件中，右击Layers（图层）→Properties（属性）→Coordinate System（坐标系）

[![](http://blog.gisersqdai.top/1585513343894xbqxtw7z.png)
](http://blog.gisersqdai.top/1585513343894xbqxtw7z.png)

然后如图所示点击生成一个新的Projected Coordinate System（投影坐标系）。

[![](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113200921.jpg)
](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113200921.jpg)

按照如图所示设置。

[![](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113200949.jpg)
](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113200949.jpg)

并用Save As，导出一个.prj的投影文件。

接着用Arctoolbox的投影工具进行投影变换（我本身数据是WGS1984的地理坐标系）。

[![](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113201327.jpg)
](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113201327.jpg)

[![](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113202047.jpg)
](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113202047.jpg)

选择投影的时候可以直接import。

[![](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113202036.jpg)
](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171113202036.jpg)

等待运行。

结果图。

[![](http://blog.gisersqdai.top/158551370322534i9tc4k.png)
](http://blog.gisersqdai.top/158551370322534i9tc4k.png)

如上，其实过程不复杂。最关键的这个使得中国能居于中间的原因是投影参数里面的第三个参数——Central Meridian，也就是中央经线。有兴趣还可以自行调整，我这里设150结果如上，也可以自行设定，只需要双击投影文件修改属性即可。

第二种介绍下R语言的方法。R语言做空间数据的这些处理最主要的两个包就是sp和rgdal。所以在处理前请先安装这两个包。

接下来直接进入正题。

我们需要先读入空间数据，然后对空间数据进行投影变换。

如何读空间数据就请点击前面我写过的文章，[戳](https://gisersqdai.top/2017/04/24/R%E8%AF%AD%E8%A8%80%E8%AF%BB%E5%8F%96%E7%A9%BA%E9%97%B4%E6%95%B0%E6%8D%AE%E4%BB%A5%E5%8F%8AArcGIS%E4%B8%ADOLS%E5%B7%A5%E5%85%B7%E5%9B%9E%E5%BD%92%E7%BB%93%E6%9E%9C%E5%8F%AF%E8%A7%86%E5%8C%96R%E8%AF%AD%E8%A8%80%E7%89%88/)

其实关键步骤就是用prj4字符串构造出我们需要的投影坐标系。关于这一点，推荐看下面的这篇博客学习。

[坐标详解与PROJ.4使用说明](http://blog.csdn.net/sf2gis2/article/details/50686811)

此外推荐几个网站用来查询相关坐标系信息。

[epsg开源查询网站，托管在github上](http://epsg.io/)

[空间参考官网网站](http://spatialreference.org/)

[OGR驱动中的矢量格式、读写情况以及代码](http://www.gdal.org/ogr_formats.html)

这里直接给出对应的prj4字符串。”+proj=eqc +lat\_ts=30 +lat\_0=0 +lon\_0=150 +ellps=WGS84 +datum=WGS84 +units=m +no\_defs”

用sptransform转换投影坐标系，结果如图。

[![](http://blog.gisersqdai.top/1585516735699zifcon47.png)
](http://blog.gisersqdai.top/1585516735699zifcon47.png)

打完收工。

贴个R语言源码图。

[![](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171114100936.jpg)
](http://blog.gisersqdai.top/QQ%E6%88%AA%E5%9B%BE20171114100936.jpg)

## Note