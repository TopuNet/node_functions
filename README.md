# node.js类库 v1.1.1
###安装：npm install TopuNet-node-functions

文件结构：
-------------
        functions.js 放入项目文件夹handle中

更新日志：
-------------
v1.1.1

        1. 增加生成topu签名的同步方法

v1.0.5

        1. 通过jshint

v1.0.4

        1. CreateTopuSignature 的 处理ParamsJsonObj 代码块做了修改，之前写法不科学且有bug

v1.0.3

        1. 修改Request方法关于headers默认值的bug
        2. 增加全局变量subDomain_default // 默认二级域名，没找到主域名或无二级域名时使用
        3. CreateTopuSignature默认拼接params_filter和source

v1.0.2

        1. Request方法增加headers参数

v1.0.1

        1. 创建项目并发布到github
        2. 发布到npm：TopuNet-node-functions
