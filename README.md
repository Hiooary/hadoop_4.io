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
  <br>
  # cd /root/Downloads 
  # ls 
  # vi hello (写入内容) 
  # hadoop fs -put hello / (上传文件)</br>
  
  显示拒绝连接，无法上传文件。分析了一下，应该是进程没有开启，在 hadoop 目录下运行 sbin/start-all.sh 启动
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/APP1.PNG)  

  启动之后，果然可以上传
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/APP2.PNG)  
  
  在浏览器中访问 jxyy:50070 可以看到刚刚写的文件
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/hello.PNG)
  
  但是出错运行，如图，是hadoop-2.7.3版本的源码与eclipse不兼容
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/xxxx.PNG)
  
  换成了hadoop-1.2.1的源码，运行出错，如图，是因为本地和虚拟机无法通信，再次配置虚拟机的ip
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/try.PNG)
  
  能通信之后，运行还是有问题，如图，提示服务器的ipc和版本不能通信，因为ubuntu里配置的是hadoop-2.7.3版本
  ![图片](https://github.com/Hiooary/hadoop_4.io/blob/master/images/version.PNG)


