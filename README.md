# myFirstJavaWeb

# JavaWeb快速入门实例 手工搭建web项目
参考：[简单粗暴，详细得不要不要的 JavaWeb快速入门实例（1）](https://www.cnblogs.com/lrzy/articles/8258470.html "简单粗暴，详细得不要不要的 JavaWeb快速入门实例（1）")

## 服务器
服务器就是一台电脑，而tomcat是一个容器，专门存放web项目的容器。  

以下我都将tomcat称为tomcat容器。  

我们看到在tomcat容器根目录下，有一个webapps文件夹  
```
├─yourTomcatDir			你的tomcat目录
│  ├─backup
│  ├─bin
│  |  ├─ ...			
│  |  ├─servlet-api.jar
│  |  └─ ...
│  ├─conf
│  |  ├─ ...			
│  |  ├─tomcata-users.xml     tomcat用户角色配置
│  |  ├─server.xml            tomat主机配置
│  |  └─ ...
│  ├─lib
│  ├─logs
│  ├─temp
│  ├─webapp
│  ├─webapps
|  |  ├─docs	          
|  |  ├─examples		
|  |  ├─host-manager          主机管理
|  |  ├─manager               管理其他发布的项目，如examples
|  |  ├─ROOT                  访问http://localhost:8080页面对应的目录
|  |  └─ ...
│  ├─worker
│  └─ ...			          更多省略
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
 ├─host-manager          主机管理
 ├─manager               管理其他发布的项目，如examples
 ├─ROOT                  访问http://localhost:8080页面对应的目录
 ├─myapp
 ├─ROOT
 └─ ...
```

> 项目名称就叫做myapp。  

打开myapp目录，根据web项目的规范，我们需要有一个WEB-INF文件夹。  
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


> 写服务器代码

在WEB-INF下面新建一个文件夹，名字叫做classes，这个也是规范，就叫这个名字，否则tomcat容器识别不了。  
```
├─myapp				 项目目录
│  ├─WEB-INF
│  |  ├─classes			服务器代码目录
│  |  ├─web.xml
│  |  └─ ...
│  ├─index.jsp		 欢迎页
│  └─ ...
```

里面在创建一个java文件，名字就叫Hello吧

```
├─myapp				 项目目录
│  ├─WEB-INF
│  |  ├─classes			服务器代码目录
|  │  |  ├─Hello.java   java文件
|  │  |  └─ ...
│  |  ├─web.xml
│  |  └─ ...
│  ├─index.jsp		 欢迎页
│  └─ ...
```

用编辑器打开，将下面的代码拷贝进去。

```
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class Hello extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request,response);
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("已经进入服务器...");
    }

}
```

这是一个比较简单的HttpServlet 程序，说到servlet，他的意思就是服务器小程序。  

原来，在英文中，但凡是let结尾的单词，都有微小的意思。比如servlet，server是服务器，let结尾，那么就是服务器小程序。  

servlet是Server Applet的缩写，我们再来看Applet，app是应用程序，又是let结尾，所以应该就是小的应用程序。  


> 我们用命令行的方式将java文件编译成class文件。

在编译之前，我们先去tomcat容器的lib目录找一个jar：
```
├─yourTomcatDir			你的tomcat目录
│  ├─backup
│  ├─bin
│  |  ├─ ...			
│  |  ├─servlet-api.jar
│  |  └─ ...
│  ├─conf
│  ├─lib
│  ├─logs
│  ├─temp
│  ├─webapp
│  ├─webapps
│  ├─worker
│  └─ ...			更多省略
```

找到servlet-api.jar,复制一份，拷贝到classes目录下。  

```
├─myapp				 项目目录
│  ├─WEB-INF
│  |  ├─classes			服务器代码目录
|  │  |  ├─Hello.java   java文件
|  │  |  ├─servlet-api.jar			
|  │  |  └─ ...
│  |  ├─web.xml
│  |  └─ ...
│  ├─index.jsp		 欢迎页
│  └─ ...
```

然后，我们在该classes目录下，按住shift，鼠标右键，选择在此处打开命令行窗口（windows下的操作方式，如果linux，请直接在命令行中操作）。  

输入：  
```
javac -classpath servlet-api.jar Hello.java
```
如果Hello.java编译时提示编码错误，请加入编码参数：

```
javac -encoding utf-8 -classpath servlet-api.jar Hello.java
```

class文件就出来了
```
├─myapp				 项目目录
│  ├─WEB-INF
│  |  ├─classes			服务器代码目录
|  │  |  ├─Hello.class   class文件
|  │  |  ├─Hello.java   java文件
|  │  |  ├─servlet-api.jar			
|  │  |  └─ ...
│  |  ├─web.xml
│  |  └─ ...
│  ├─index.jsp		 欢迎页
│  └─ ...
```


> 再次打开web.xml，我们还需要把这个servlet配上去，让tomcat知道这个servlet需要加入我们的web项目   

web.xml  

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

  <servlet>
    <servlet-name>Hello</servlet-name>
    <servlet-class>Hello</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>Hello</servlet-name>
    <url-pattern>/hello</url-pattern>
  </servlet-mapping>
</web-app>
```

> 测试运行
如果tomcat未启动则双击startup.bat，启动tomcat容器  

然后，在浏览器的地址栏输入http://localhost:8080/myapp/hello  

发现网页上一片空白，回顾我们的servlet程序(startup.bat的运行界面)，按理说控制台会打印一句话的  


## 绑定域名
> 编辑tomcat目录/conf/server.xml增加站点配置。
```
├─yourTomcatDir			你的tomcat目录
│  ├─conf
│  |  ├─ ...			
│  |  ├─server.xml            tomat主机配置
│  |  └─ ...
│  └─ ...			          更多省略
```

servlet.xml
```
...
      <Host name="tomcat.YourDomain.com"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">

        <!-- SingleSignOn valve, share authentication between web applications
             Documentation at: /docs/config/valve.html -->
        <!--
        <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
        -->

        <!-- Access log processes all example.
             Documentation at: /docs/config/valve.html
             Note: The pattern used is equivalent to using pattern="common" -->
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

      </Host>


      <Host name="YourDomain.com" appBase="/YourAppDir/demo"
        unpackWARs="true" autoDeploy="true">

        <Context path="YourPath" docBase="root" workDir="/YourAppDir/demo/temp"  />

        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />
      </Host>

...

```
元素属性说明

|元素名|属性|说明|  
|---|---|---|
|Host||表示一个虚拟主机|  
|Host|name|指定主机域名|
|Host|appBase|应用程序基本目录，即存放应用程序的目录|
|Host|unpackWARs|如果为true，则tomcat会自动将WAR文件解压，否则不解压，直接从WAR文件中运行应用程序|
|Host|autoDeploy|热部署开关，如果为true,增加新的目录、war文件、修改WEB-INF/web.xml，会新建或重新部署应用，该选项方便部署，打开后会比较占用系统资源，不建议开启|
|Context||表示一个web应用程序，通常为WAR文件，关于WAR的具体信息见servlet规范|
|Context|docBase|应用程序的路径或者是WAR文件存放的路径,如果docBase为war路径可不加文件扩展名（.war），且无需手动建立war文件的解压目录以避免目录权限等原因导至war文件无法解压|
|Context|path|表示此web应用程序的url的前缀，这样请求的url为 http://YourDomain.com:8080/path/**** ,path为空时war解压应用程序路径为ROOT否则为path值对应的路径|
|Context|reloadable|这个属性非常重要，如果为true，则tomcat会自动检测应用程序的/WEB-INF/lib 和/WEB-INF/classes目录的变化，自动装载新的应用程序，我们可以在不重起tomcat的情况下改变应用程序，打开后会比较占用系统资源，不建议开启|
|Context|workdir|表示缓存文件的放置地址|
