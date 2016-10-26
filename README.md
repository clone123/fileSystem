# fileSystem —— 第一个 Node.js 项目
文件服务：分片上传，合并，入库，查询，搜索，修改，下载，预览，删除

具体需用到的技术及重点大概如下：

####1：FileReader，前端文件读取，读取格式可选，二进制，Data Url等，适合做图片预览。

####2：FormDate，slice， Html5新出来的API，对文件的一些处理，切片，传输。

####3：vue-resource , 基于Vue的一个Http请求库，可直接注册到Vue原型上，也可自用ajax发送请求数据，具体看API文档。

####4：multiparty,formidable 对文件处理的npm包，后续对文件分片接受处理,API文档需细细研究，尤其分片接受那块。

####5：Nodejs FS模块，对分片上传上来的文件处理,后面涉及到一系列对文件的操作：

a：文件存盘路径策略

b：提前校验文件的状态，识别，md5(前端Spark-md5，后端node-md5)处理

c：临时文件的读取，重命名标示，为后续的文件合并做好铺垫
   
####6：最关键的一步，文件的合并，合并策略：

a：前端同步或异步分片上传，后端异步合并————此方法坑颇多，在分片总数较多情况下，异步合并后的文件可能不完整(与源文件内容顺序不一样)，导致压缩文件无法解压，视频播放中出现异常情况。

b：前端同步或异步分片上传，后端同步合并————此方法可行，读取文件的方式可以异步，或文件流的形式来读取，同步合并文件数据就OK，对后续的断点续传，秒传，也比较好的支持。

####7：入库前，目前基于Mysql, 通过 Sequelize 的 Model层对表的映射，从而来对表数据库的增删改查操作。

####8：入库，关于图片，音视频的存储入库策略：

a：直接fileReader获取文件二进制，存储到数据库，缺点是数据量过大，对数据库性能影响很大，Http请数据受限。

b：数据库存只放文件路径，利用 Express 托管静态文件即可(文件挂载)，后续删除数据库数据时候，对应文件也需要单独处理删除操作
   
####9：前端数据展示，less,es6,webpack,vue/vuex,组件化，过滤器，需注意的是当组件里面嵌套一个动态组件（三级嵌套），想通过动态组件的事件派发来传递数据，子组件无法监听到，改用props可行。


PS ：今天抽时间来记录下整个开发过程中大概需要注意的几个点，具体细节太多就不一一细说，碰到的问题也很多，过程很辛苦，结果还是挺让你欣慰的，收获挺大，真是应了那句话，压力大，动力大，永远不要小看自己！共勉！

