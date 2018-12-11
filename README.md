# myFirstJavaWeb

# JavaWeb快速入门实例 手工搭建web项目
[简单粗暴，详细得不要不要的 JavaWeb快速入门实例（1）](https://www.cnblogs.com/lrzy/articles/8258470.html "简单粗暴，详细得不要不要的 JavaWeb快速入门实例（1）")

## 服务器
服务器就是一台电脑，而tomcat是一个容器，专门存放web项目的容器。  
  
以下我都将tomcat称为tomcat容器。  
  
我们看到在tomcat容器根目录下，有一个webapps文件夹  
 ├─docs			          
 ├─examples				
 ├─host-manager	       
 ├─manager           
 ├─ROOT				
 └─ ... 


### 服务器启动
在tomcat目录下有一个bin目录。一般来说，可执行的文件都放在bin目录下。  
打开bin，找到一个startup.bat文件。这就是启动tomcat的东西，双击它，tomcat就被启动了。  
打开浏览器，通过地址：127.0.0.1:8080/yourDir访问tomcat里面的项目。


## 手工搭建web项目
> 首先，在webapps目录下新建一个文件夹，是的，就是文件夹，不管你项目是什么，肯定还是放在文件夹里面的。

 ├─docs  
 ├─examples	
 ├─host-manager	
 ├─manager 
 ├─manager
 ├─myapp
 ├─ROOT	
 └─ ... 

> 项目名称就叫做webapp。  

打开webapp，根据web项目的规范，我们需要有一个WEB-INF文件夹。  
├─myapp				 项目目录
│  ├─WEB-INF
│  └─ ... 


> 然后，在WEB-INF文件夹里面，必须要有一个web.xml文件。

xml文件，就是一个描述性的文件，参考资料作者观点如下：  

XML = JavaBean = Json = HashMap  

它无非就是描述一些东西，保存一些数据而已。  

好的，我们在里面新建一个web.xml。这个文件非常重要，正因为它的存在，tomcat容器才会知道这个文件夹里面竟然是一个web项目。  

否则，tomcat容器是不知道这个web项目的，它只会将myapp文件夹看做是一个文件夹而已。  

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app>
  <display-name>web</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
</web-app>
```

XML的一个作用就是配置文件，web.xml本身就是一个配置文件。在web项目中，我们应用xml最多的也就是配置一些参数。

配置参数，就是给属性赋值嘛，没什么神秘的。

包括我们学习JavaSE，归根到底，一直在做的一件事就是new对象，然后调用方法，调用方法的目的一方面是做一些事情，另一方面不还是给属性赋值嘛。

你可以把web.xml看做是一个java类，类名叫做 webApp。它里面有两个属性，分别是display-name和welcome-file-list。

display-name是发布名称，也就是项目的名字。
welcome-file-list 是欢迎页面，就是说，当你在浏览器直接访问这个myapp项目，默认跳转的页面。

想象一下，应该会变得非常好理解。

XML就是一个数据描述语言，我们通过web.xml描述这个项目的构成和配置。

