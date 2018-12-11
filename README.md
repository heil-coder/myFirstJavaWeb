# myFirstJavaWeb

# JavaWeb快速入门实例 手工搭建web项目
[简单粗暴，详细得不要不要的 JavaWeb快速入门实例（1）](https://www.cnblogs.com/lrzy/articles/8258470.html "简单粗暴，详细得不要不要的 JavaWeb快速入门实例（1）")

## 服务器
服务器就是一台电脑，而tomcat是一个容器，专门存放web项目的容器。  
  
以下我都将tomcat称为tomcat容器。  
  
我们看到在tomcat容器根目录下，有一个webapps文件夹  
```
 ├─docs	          
 ├─examples		
 ├─host-manager      
 ├─manager    
 ├─ROOT	
 └─ ...
```

### 服务器启动
在tomcat目录下有一个bin目录。一般来说，可执行的文件都放在bin目录下。  
打开bin，找到一个startup.bat文件。这就是启动tomcat的东西，双击它，tomcat就被启动了。  
打开浏览器，通过地址：http://localhost:8080/yourDir访问tomcat里面的项目。


## 手工搭建web项目
> 首先，在webapps目录下新建一个文件夹，是的，就是文件夹，不管你项目是什么，肯定还是放在文件夹里面的。
```
 ├─docs 
 ├─examples	
 ├─host-manager	
 ├─manager 
 ├─manager
 ├─myapp
 ├─ROOT	
 └─ ... 
```

> 项目名称就叫做webapp。  

打开webapp，根据web项目的规范，我们需要有一个WEB-INF文件夹。  
```
├─myapp				 项目目录
│  ├─WEB-INF
│  └─ ... 
```

> 然后，在WEB-INF文件夹里面，必须要有一个web.xml文件。
```
├─myapp				 项目目录
│  ├─WEB-INF
│  |  ├─web.xml
│  |  └─ ... 
│  └─ ... 
```

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

> 接下来，我们是不是要给他一个欢迎页啊。嗯，我们在webapp目录下添加一个简单的欢迎页，里面就打印一个HelloWorld。  

```
├─myapp				 项目目录
│  ├─WEB-INF
│  |  ├─web.xml
│  |  └─ ... 
│  ├─index.jsp		 欢迎页
│  └─ ... 
```

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
    <h1>Hello World!</h1>
</body>
</html>
```

```
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%>
```
这是一条JSP的page指令，如果你用面向对象的思维来看待这个玩意，就是new了一个page对象，并且给它里面的language，contentType，charset，pageEncoding属性分别赋了值。  

language表示JSP页面所用的语言，默认是java，其实你写不写都没有关系，因为目前来说JSP它只支持Java。  

我们来试一下，现在我们把language属性去掉。就变成了这样：  
```
<%@ page contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
```

contentType="text/html; charset=UTF-8"：设置页面的内容是文本或者html页面，字符设置为UTT-8。  
pageEncoding="UTF-8"：页面编码设置为UTF-8。  
好的，现在我们在bin目录，双击运行startup.bat
启动完毕。

打开浏览器，在地址栏输入http://localhost:8080/myapp/

回车

```
Hello World!
```

是不是出来了。

这就是手工搭建一个web项目的过程。

只要你符合web项目的规范，包括文件夹的名字，文件的名字，就会被tomcat容器识别为一个web项目。
