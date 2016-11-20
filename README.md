# 使用 JAVA 操作 HDFS

  这里操作一个比较简单的读取 hdfs 数据的方法，通过java.net.URL打开一个流，不过在此之前要先调用 setURLStreamHandlerFactory 方法设置为 FsUrlStreamHandlerFactory。然后调用 IOUtils 类的 copyBytes 方法将 hdfs 数据流拷贝到标准输出流 System.out 中。

  操作：

1.使用eclipse 新建工程 -> 引进依赖                                         
 (这里先引入 hadoop-common-2.7.3.jar 类，后面在需要其他的时候再度引入)          
 ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/andExterl.PNG)

2.在eclipse 中写代码，读取文件(只读不能写)                                   
  新建包 ->新建类                                                            
 ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/AppOne.PNG)

3.在 Hadoop 中操作文件
  <br><b>
  # cd /root/Downloads 
  # ls 
  # vi hello (写入内容) 
  # hadoop fs -put hello / (上传文件)</b></br>
  
  显示拒绝连接，无法上传文件。分析了一下，应该是进程没有开启，在 hadoop 目录下运行 sbin/start-all.sh 启动
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/APP1.PNG)  

  启动之后，果然可以上传
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/APP2.PNG)  
  
  在浏览器中访问 jxyy:50070 可以看到刚刚写的文件
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/hello.PNG)
  
  但是出错运行，如图，应该是hadoop-2.7.3版本的源码与eclipse不兼容
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/xxxx.PNG)
  
  换成了hadoop-1.2.1的源码，运行出错，如图，是因为本地和虚拟机无法通信，再次配置虚拟机的ip
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/retry.PNG)
  
  能通信之后，运行还是有问题，如图，提示服务器的ipc和客户端的版本不能通信，因为ubuntu里配置的是hadoop-2.7.3版本
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/version.PNG)
  
  于是纠结一番之后，决定装个hadoop-1.2.1的版本，利用虚拟机自带的克隆操作，修改相关的配置文件，倒是很快安装了，但是启动不了datanode，start-all.sh没有报错，但是 jps 看不到Datanode进程。好不容易启动了，节点也会很快就死了<b>所以这里还是有问题啊</b>
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/jps.PNG)
  
  查看logs目录下的相关日志文件，意思是路径不存在。<b>呵呵</b>
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/error.PNG)
  
  在有 DataNode 节点启动的情况下，在eclipse运行程序，如图，<b>我不知道为啥啊</b>
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/empty.PNG)
  
  又想了一个方法：利用eclipse自带的 export 功能将java文件打包成 .jar 文件放进ubuntu系统中运行，如图，提示找不到类
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/noclass.PNG)
  
  看了报错的日志文件之后，意识到应该是引入的第三方 .jar 文件没有打包，但是eclipse 自带的 export功能无法完成。所以决定装一个 Fat Jar 的插件，具体的安装方法可以参考 http://blog.csdn.net/memray/article/details/17969443
  但是我下载安装的时候，eclipse没有反应，在线安装的时候，报错如图
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/jar.PNG)
  
  解决方法可以安装一个eclipse2.0的插件，1.安装Eclipse2.0版本的插件支持。具体操作：Help -> Install New Software... -> Work with-> 选择“The Eclipse Project Updates - http://download.eclipse.org/eclipse/updates/4.5”  （如果是4.4eclipse luna就选updates/4.4）-> 勾选"Eclipse Tests, Examples, and Extras" ,安装完再安装 Fat Jar ，安装完可以看到标志
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/Fat.PNG)
  
  安装之后打包java文件进行运行。还是不行哈<b>我还是不知道为啥啊</b>
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/reflect.PNG)
  
  专业挖坑，不想深说
  


