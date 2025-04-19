# 支持私有部署的笔记类应用

#### 思源笔记

[![支持私有部署的笔记类应用——个人向](https://am.zdmimg.com/202401/06/65993d24bdcc64689.png_e1080.jpg)](https://post.smzdm.com/p/ag5m98zm/pic_2/)

国人开发的一款非常棒的开源笔记，社区活跃，插件众多，颜值高而且国人开发使用起来没有语言障碍，一些插件比较贴合国内市场，也有挺多整活有趣的插件，其他功能特点可以看官网介绍。

为什么没有继续使用了？

* 同步问题 部署之后使用的NAS自身的webdav同步，不知怎么的安装几个挂件后同步巨慢，局域网下也巨慢，看了思源是把所有数据分成了小块进行同步的所以文件数据较多、体积小，同步时不能用满带宽，就跟平时复制文件夹时如果小文件太多复制起来会变慢一样。看官方也推荐使用S3同步，不过NAS不支持S3就没继续折腾了。
* 账号问题 部署后要使用同步功能必须要注册登录他们论坛的账号，对强制要求注册账号这种事比较抵触
* 收费问题 同步功能非免费，后面需要付费才能使用

#### Joplin

之前写过一篇文章记录[Joplin的部署](https://post.smzdm.com/p/an3r4p52/)，不过最近倒没有继续主力使用Joplin，目前用Joplin更多的是来收集网页内容，它的chrome插件配合本地客户端实在是太好用，直接一键把网页内容同步到本地笔记中。Joplin本身功能加上一些插件补充功能上还是满足使用的，就是界面有些简陋。

#### Trilium

[![支持私有部署的笔记类应用——个人向](https://am.zdmimg.com/202401/06/65993da36be4b6733.png_e1080.jpg)](https://post.smzdm.com/p/ag5m98zm/pic_3/)

这个有[汉化版](https://github.com/Nriver/trilium-translation)也有完整的使用[wiki文档](https://trilium.netlify.app/home)，支持双链导出markdown等。可以通过js、html、css实现各种插件比如字数统计、笔记统计等等非常容易扩展。另外一个比较好用的点是对画布excalidraw的支持很好。其他各种功能wiki都很详细，基本上看一遍wiki啥都清楚了。桌面客户端可以和服务器同步，也支持直接在web端访问。

#### blossom

[![支持私有部署的笔记类应用——个人向](https://am.zdmimg.com/202401/06/65993dbac54699746.png_e1080.jpg)](https://post.smzdm.com/p/ag5m98zm/pic_4/)

目前接触到界面最漂亮的一款笔记，github readme 有详细介绍可以直接在线试用，不过云笔记对服务器端要求比较高。

其他一些比较受流行的笔记Notion、Obsidian等没法私有部署就没一一体验了，就目前使用来Trilium已经完美满足需求了，就不想在折腾其他笔记了，毕竟部署笔记应用的初衷是为了记笔记。之前也一直想找款all in one的笔记最终折腾下来还是各种工具组合下来更舒服些。目前的话网页收集Joplin，笔记整理Trilium，一些项目类wiki使用[wiki.js](https://post.smzdm.com/p/ag5m98zm/#root/yhHvT5TpeHDZ/ApRaUVr1xIXq/N3tfJ6K73sYT)对draw.io的支持太棒了。

作者声明本文无利益相关，欢迎值友理性交流，和谐讨论～
