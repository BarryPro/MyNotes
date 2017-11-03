1. 10.34：注解不支持模块范围

   ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/38101042.png)是maven的各个模块之间出现了循环的依赖关系,是由于在pom项目下添加了pom依赖导致的

2. 11.11：使用maven的thrift进行编译：编译命令是 mvn thrift:complie（前提是本地已经配置好thrift-0.8版本的thrift了，这条命令可以直接在IDEA中执行如图）

   ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/56833876.png)

3. ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/50948188.png)

4. 14.09：配置本地的idea的jvm参数

5. -ea -Xmx2G -Xms2G -XX:PermSize=256M -Denvironment=develop -Dspring.profiles.active=develop

6. 还是报 permGen 异常

   ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/52635866.png)

7. ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/53284143.png)

8. ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/53341072.png)

9. 拒绝链接

   ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/54237341.png)

10. ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/55294445.png)

11. 16.40：换用本地的jetty应用服务器进行调试程序（waimai_order_admin）,其他的使用Tomcat

12. jetty服务器出现问题

    ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/60160794.png)

13. idea对单个文件的大小做了限制，这回导致其他的类文件不识别这个大文件类（默认是250处于对内存的保护，可以直接修改idea的启动配置文件，来设置较大的文件大小限制，这样就可以识别大的类文件了）

14. ​    其设置在...JetBrains\IntelliJ IDEA Community Edition 14.1.4\bin 目录下的idea.properties文件

    ![img](file:///var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/9704d4ce-1f9f-41c5-b6f7-98de7fbfec42/index_files/81335734.png)