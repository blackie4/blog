Nodejs链接mongodb简单介绍
===

本地安装mongodb数据库，项目npm install mongodb安装mongodb模块。

### 1. 启动mongodb

首先在您项目根目录下建立data文件夹，data下建立db文件；
运行cmd.exe 进入DOS命中界面，进入mongodb安装目录的bin文件目录 执行mongod -dbpath "your projecet\data\db"；
接着打开mongodb安装目录的bin文件目录下的mongo.exe文件，mongodb数据库已经启动成功

<!--more-->

### 2. 建立数据库和集合
mongo.exe界面下，输入 use blog 若存在blog库则转到blog库；不存在则会建立blog库并转到blog库下；
接着输入 db.content.insert({name: 'blog'}) 回车，若存在content集合则向其添加记录， 不存在则创建并添加记录
至此数据库方面的工作已准备完毕

### 3. 编写服务器代码

var mongodb = require('mongodb');
var server  = new mongodb.Server('localhost', 27017, {auto_reconnect:true});
var db = new mongodb.Db('blog', server, {safe:true});
db.open(function(err, db){
    if(!err){
        db.collection('contents', {safe:true}, function(err, collection){
            if(err){
                console.log(err);
            }else{
                collection.find().toArray(function(err,docs){ console.log(docs); });   // 查询数据
            }
        });
    }else{ console.log(err); }
});

