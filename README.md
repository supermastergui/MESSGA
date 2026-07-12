# MESSGA
Make EuroScope Sector Great Again | 使ES扇区再次强大

## 数据来源

EuroScope的扇区需要随着每期（28天）的导航数据更新而更新，感谢由 *[Navigraph](https://navigraph.com/)* 公司提供的导航数据，以下是扇区数据的来源：

- xplane12_native_****.zip : 提供丰富的、可口的导航数据，足够详细
- fsnav_****.zip : FSNavigator, FS-Navigator 4.x, ```cycle.json, AIRWAY.txt, ISEC.txt, cycle_info.txt```
- CSV : Secret QwQ（[supermastergui/rtecheck](https://github.com/supermastergui/rtecheck)）

那么，由聪明的小朋友就会问了：“啊~既然X-Plane 12的导航数据已经够丰富了，为什么我们还需要`FSNavigator`呢？”

因为，EuroScope通过读取这种数据，使得其内部的逻辑能够正常（例如：Flight Plan Box中航路的断点检查等你看不见的数据，都是由`FSNavigator`导航数据提供的）。

其次是，如果不添加，EuroScope将在载入扇区的时候报错。谁不想看一个底部没有报错的EuroScope扇区呢？

这些数据将被保存在`Navi/`文件夹内，这些文件应有开发者自行查找补全，仓库将过滤并不上传这些内容。

## 解析数据

以下内容参考：[https://developer.x-plane.com/article/navdata-in-x-plane-11/](https://developer.x-plane.com/article/navdata-in-x-plane-11/)

