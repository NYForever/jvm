# JVM

## 问题

1. IDEA启动main方法时，会自动进行javac编译吗？
>
> 是的，当你在IDEA中启动main方法时，如果代码没有编译过，IDEA会自动进行javac编译。这是因为IDEA内置了Java编译器，可以在后台自动编译代码。如果代码已经编译过，IDEA会检查是否有任何更改，并在必要时重新编译代码。

2. javac编译之后，java命令直接启动main方法？会自动生成jvm虚拟机？
>
> 是的，java命令会启动main方法，并且会自动生成JVM虚拟机。

3. JVM的类加载器主要分为以下几种：
> 
> 1.启动类加载器（Bootstrap ClassLoader）：负责加载JVM自身需要的类，如java.lang包中的类等。
> 
> 2.扩展类加载器（Extension ClassLoader）：负责加载Java平台扩展的一些类，如javax包中的类等。
> 
> 3.应用类加载器（Application ClassLoader）：负责加载应用程序中的类，即我们自己编写的类。
> 
> 启动类加载器加载的包包括：java.lang包中的类、java.util包中的类、java.io包中的类等。
> 
> 扩展类加载器加载的包包括：javax包中的类、sun包中的类等。
> 
> 应用类加载器加载的包包括：我们自己编写的类、第三方库中的类等。

4. 类加载器的执行顺序是怎么样的？双亲委派机制？
> 
> Java类加载器的执行顺序是按照双亲委派机制来执行的。这个机制是指当一个类加载器需要加载一个类时，它会先委派给它的父类加载器去加载，如果父类加载器无法加载该类，那么它会再次委派给它的父类加载器，直到最终委派到顶层的启动类加载器。如果所有的父类加载器都无法加载该类，那么该类加载器会尝试自己去加载该类。
> 
> 这个机制的好处是可以保证Java程序的安全性和稳定性。因为如果一个类被恶意篡改，那么它的父类加载器会先加载原始的类，而不是被篡改后的类。这样就可以避免恶意代码的执行。
> 
> 总结一下，Java类加载器的执行顺序是按照双亲委派机制来执行的，这个机制可以保证Java程序的安全性和稳定性。

5. 自定义类加载器可以做什么逻辑？
> 
> 自定义类加载器可以实现以下逻辑：
> 
> 	1. 加载非标准的类文件：自定义类加载器可以加载非标准的类文件，例如从网络或数据库中获取类文件。
> 
> 	2. 实现类隔离：自定义类加载器可以实现类隔离，即在不同的类加载器中加载同名的类，从而避免类冲突。
> 
> 	3. 实现热部署：自定义类加载器可以实现热部署，即在运行时动态加载新的类文件，从而实现代码的更新和升级。
> 
> 	4. 加载加密的类文件：自定义类加载器可以加载加密的类文件，从而保护代码的安全性。
> 
> 	5. 实现类的动态生成：自定义类加载器可以实现类的动态生成，从而实现动态代理、AOP等功能。
> 
> 	6. 实现类的版本控制：自定义类加载器可以实现类的版本控制，从而实现类的回滚和版本管理。

6. Tomcat自定义的类加载器做了什么逻辑？是怎么实现的？
> 
>    Tomcat自定义的类加载器主要是为了解决Web应用程序中类的隔离问题。它的实现逻辑如下：
> 
>     1. 首先，Tomcat会为每个Web应用程序创建一个独立的ClassLoader，这个ClassLoader会从Web应用程序的classpath中加载类。
> 
>     2. 如果Web应用程序中的类需要访问Tomcat的类库，Tomcat会使用自定义的ClassLoader来加载这些类。这个ClassLoader会首先尝试从Web应用程序的classpath中加载类，如果找不到，就会从Tomcat的共享类库中加载类。
> 
>     3. 如果Tomcat的共享类库中也没有找到需要的类，那么Tomcat会尝试使用父ClassLoader来加载类。这个父ClassLoader可以是系统ClassLoader，也可以是Tomcat的BootstrapClassLoader。
> 
>     4. 如果父ClassLoader也无法加载需要的类，那么Tomcat会抛出ClassNotFoundException异常。
> 
>    Tomcat自定义的类加载器实现主要是通过继承Java的ClassLoader类来实现的。在实现过程中，需要重写findClass()方法来实现自定义的类加载逻辑。具体实现可以参考Tomcat的源代码。

7. 一个Tomcat可以启动多个Web应用吗？
>
>是的，一个Tomcat可以启动多个Web应用。每个Web应用都有自己的上下文路径和独立的资源。在Tomcat的conf/server.xml文件中，可以配置多个Context元素来定义不同的Web应用。每个Context元素都有自己的docBase属性，指定Web应用的根目录。在Tomcat启动时，每个Web应用都会被加载并运行。

8. Java Agent原理是什么，是启动时修改class文件，还是运行时可以实时修改class文件？
> 
> Java Agent是一种Java技术，它可以在Java应用程序启动时或者在运行时动态地修改或者增强Java应用程序的行为。Java Agent的原理是在Java虚拟机启动时，通过Java Agent的机制，将Java Agent的代码注入到Java应用程序的进程中，从而实现对Java应用程序的监控和控制。
> 
> Java Agent可以在应用程序启动时修改class文件，也可以在程序运行时实时修改class文件。在应用程序启动时，Java Agent可以通过Java Instrumentation API来修改class文件，从而实现对Java应用程序的增强。在程序运行时，Java Agent可以通过Java Reflection API来实时修改class文件，从而实现对Java应用程序的动态修改。
> 
> 总之，Java Agent可以通过多种方式来实现对Java应用程序的增强和修改，具体实现方式取决于具体的应用场景和需求。