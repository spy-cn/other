# 第一章 windows版MySQL软件的安装与卸载

## 1、卸载

### 1、软件的卸载

#### 方式一：通过控制面板

![image-20201227100554970](J:\other\other\install\img\image-20201227100554970.png)

#### 方式二：通过电脑管家等软件卸载

![img](J:\other\other\install\img\clip_image004.jpg)

#### 方式三：通过安装包中提供的卸载功能卸载

![img](J:\other\other\install\img\clip_image006.jpg)

### 2、清理残余文件

如果再次安装不成功，可以卸载后对残余文件进行清理后再安装

#### （1）清除安装残余文件

![img](J:\other\other\install\img\clip_image008.jpg)

#### （2）清除数据残余文件

请在卸载前做好数据备份

![img](J:\other\other\install\img\clip_image010.jpg)

### 3、清理注册表

如何打开注册表编辑器：在系统的搜索框中输入regedit

如果前两步做了，再次安装还是失败，那么可以清理注册表

1：HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Eventlog\Application\MySQL服务 目录删除

2：HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\MySQL服务 目录删除

3：HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\Eventlog\Application\MySQL服务 目录删除

4：HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\MySQL服务 目录删除

5：HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\MySQL服务目录删除

6：HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MySQL服务删除

注册表中的ControlSet001,ControlSet002,不一定是001和002,可能是ControlSet005、006之类

## 2、安装

### （1）准备安装

![img](J:\other\other\install\img\clip_image012.jpg)

### （2）欢迎安装

![img](J:\other\other\install\img\clip_image014.jpg)

### （3）准许协议

![img](J:\other\other\install\img\clip_image016.jpg)

### （4）选择安装模式

![img](J:\other\other\install\img\clip_image018.jpg)

Typical：表示一般常用的组件都会被安装，默认情况下安装到”C:\Program Files\MySQL\MySQL Server 5.5\”下。

Complete：表示会安装所有的组件。此套件会占用比较大的磁盘空间。

Custom：表示用户可以选择要安装的组件，可以更改默认按照的路径。这种按照类型最灵活，适用于高级用户。

### （5）选择安装组件及安装路径

![img](J:\other\other\install\img\clip_image020.jpg)

这里可以选择安装哪些部分，主要是这里可以设置两个路径：

MySQL Server的应用软件的安装路径，默认在“C:\**Program Files**\MySQL\MySQL Server 5.5\”

Server data files的数据存储的目录路径，默认在“C:\**ProgramData**\MySQL\MySQL Server 5.5\”

建议把数据存储的目录路径修改一下，以防系统崩溃或重装系统时数据保留。

### （6）开始安装

![img](J:\other\other\install\img\clip_image022.jpg)

安装进度

![img](J:\other\other\install\img\clip_image024.jpg)

系统会显示MySQL Enterprise版（企业版）的一些功能介绍界面，可以单击“Next”继续。

![img](J:\other\other\install\img\clip_image026.jpg)

![img](J:\other\other\install\img\clip_image028.jpg)

### （7）安装完成

![img](J:\other\other\install\img\clip_image030.jpg)

单击“Finish”按钮完成安装过程。如果想马上配置数据库连接，选择“Launch the MySQL Instance Configuration Wizard”复选框。如果现在没有配置，以后想要配置或重新配置都可以在“MySQL Server”的安装目录的bin目录下（例如：D:\ProgramFiles\MySQL5.5\MySQL Server 5.5\bin）找到“MySQLInstanceConfig.exe”打开“MySQL Instance Configuration Wizard”向导。

## 3、MySQL的配置

### （1）准备开始

![img](J:\other\other\install\img\clip_image032.jpg)

### （2）选择配置类型

![img](J:\other\other\install\img\clip_image034.jpg)

选择配置方式，“Detailed Configuration（手动精确配置）”、“Standard Configuration（标准配置）”，我们选择“Detailed Configuration”，方便熟悉配置过程。

### （3）选择MySQL的应用模式

![img](J:\other\other\install\img\clip_image036.jpg)

Develop Machine（开发机），使用最小数量的内存

Server Machine（服务器），使用中等大小的内存

Dedicated MySQL Server Machine（专用服务器），使用当前可用的最大内存。

### （4）选择数据库用途选择界面

![img](J:\other\other\install\img\clip_image038.jpg)

选择mysql数据库的大致用途：

“Multifunctional Database（通用多功能型，好）”：此选项对事务性存储引擎（InnoDB）和非事务性（MyISAM）存储引擎的存取速度都很快。

“Transactional Database Only（服务器类型，专注于事务处理，一般）”：此选项主要优化了事务性存储引擎（InnoDB），但是非事务性（MyISAM）存储引擎也能用。

“Non-Transactional Database Only（非事务处理型，较简单）主要做一些监控、记数用，对MyISAM数据类型的支持仅限于non-transactional，注意事务性存储引擎（InnoDB）不能用。

### （5）配置InnoDB数据文件目录

![img](J:\other\other\install\img\clip_image040.jpg)

InnoDB的数据文件会在数据库第一次启动的时候创建，默认会创建在MySQL的安装目录下。用户可以根据实际的空间状况进行路径的选择。

### （6）并发连接设置

![img](J:\other\other\install\img\clip_image042.jpg)

选择您的网站的一般mysql 访问量，同时连接的数目，“Decision Support(DSS)/OLAP（决策支持系统，20个左右）”、“Online Transaction Processing(OLTP)（在线事务系统，500个左右）”、“Manual Setting（手动设置，自己输一个数）”

### （7）网络选项设置

![img](J:\other\other\install\img\clip_image044.jpg)

是否启用TCP/IP连接，设定端口，如果不启用，就只能在自己的机器上访问mysql 数据库了，我这里启用，把前面的勾打上，Port Number：3306，还有一个关于防火墙的设置“Add firewall exception ……”需要选中，将MYSQL服务的监听端口加为windows防火墙例外，避免防火墙阻断。

在这个页面上，您还可以选择“启用标准模式”（Enable Strict Mode），这样MySQL就不会允许细小的语法错误。尽量使用标准模式，因为它可以降低**有害数据**进入数据库的可能性。

### （8）选择字符集

![img](J:\other\other\install\img\clip_image046.jpg)

注意：如果要用原来数据库的数据，最好能确定原来数据库用的是什么编码，如果这里设置的编码和原来数据库数据的编码不一致，在使用的时候可能会出现乱码。

这个比较重要，就是对mysql默认数据库语言编码进行设置，第一个是西文编码，第二个是多字节的通用utf8编码，第三个，手工选择字符集。

提示：

如果安装时选择了字符集和“utf8”，通过命令行客户端来操作数据库时，有时候会出现乱码，

这是因为“命令行客户端”默认是GBK字符集，因此客户端与服务器端就出现了不一致的情况，会出现乱码。

可以在客户端执行：

mysql> set names gbk; 

可以通过以下命令查看：

mysql> show variables like 'character_set_%';

![img](J:\other\other\install\img\clip_image048.jpg)![img](J:\other\other\install\img\clip_image050.jpg)

对于客户端和服务器的交互操作，MySQL提供了3个不同的参数：character_set_client、character_set_connection、character_set_results，分别代表客户端、连接和返回结果的字符集。通常情况下，这3个字符集应该是相同的，才能确保用户写入的数据可以正确的读出和写入。“set names xxx;”命令可以同时修改这3个参数的值，但是需要每次连接都重新设置。

### （9）安全选择

![img](J:\other\other\install\img\clip_image052.jpg)

选择是否将mysql 安装为windows服务，还可以指定Service Name（服务标识名称，例如我这里取名为“MySQL5.5”），是否将mysql的bin目录加入到Windows PATH环境变量中（加入后，就可以直接使用bin下的命令）”，我这里全部打上了勾。

### （10）设置密码

![img](J:\other\other\install\img\clip_image054.jpg)

这一步询问是否要修改默认root 用户（超级管理）的密码（默认为空），“New root password”如果要修改，就在此填入新密码，“Confirm（再输一遍）”内再填一次，防止输错。（如果是重装，并且之前已经设置了密码，在这里更改密码可能会出错，请留空，并将“Modify Security Settings”前面的勾去掉，安装配置完成后另行修改密码）

 

“Enable root access from remotemachines（是否允许root 用户在其它的机器或使用IP地址登陆，如果要安全，就不要勾上，如果要方便，就勾上它）”。如果没有勾选，默认只支持localhost和127.0.0.1连接。

 

最后“Create An Anonymous Account（新建一个匿名用户，匿名用户可以连接数据库，不能操作数据，包括查询，如果要有操作数据的权限需要单独分配）”，一般就不用勾了

### （11）准备执行界面

![img](J:\other\other\install\img\clip_image056.jpg)

### （12）完成

![img](J:\other\other\install\img\clip_image058.jpg)

# 第二章、Windows下MySQL的使用

## 1、启动和停止服务

关系型数据库分为桌面文件共享型数据库，例如Access，和C/S架构的网络共享型数据库，例如：MySQL，Oracle等。MySQL软件的服务器端必须先启动，客户端才可以连接和使用使用数据库。

启动服务的方式：

### 方式一：图形化方式

“我的电脑/计算机”-->右键-->“管理”-->“服务”-->启动和关闭MySQL

“开始菜单”-->“控制面板”-->“管理工具”-->“服务”-->启动和关闭MySQL

“任务管理器”-->“服务”-->启动和关闭MySQL

 

![img](J:\other\other\install\img\clip_image060.jpg)  ![img](J:\other\other\install\img\clip_image062.jpg)

### 方式二：命令行

net start MySQL服务名

net stop MySQL服务名

## 2、客户端登录

### 方式一：MySQL自带客户端

“开始菜单”-->MySQL-->MySQL Server 5.5 --> MySQL 5.5 Command Line Client

![img](J:\other\other\install\img\clip_image064.jpg)

仅限于root用户

### 方式二：命令行

mysql -h 主机名 -P 端口号 -u 用户名 -p密码

例如：mysql -h localhost -P 3306 -u root -proot  

 

注意：

（1）-p与密码之间不能有空格，其他参数名与参数值之间可以有空格也可以没有空格

​          mysql -hlocalhost -P3306 -uroot -proot

（2）密码建议在下一行输入

​          mysql -h localhost -P 3306 -u root -p

​          Enter password:****

（3）如果是连本机：-hlocalhost就可以省略，如果端口号没有修改：-P3306也可以省略

​          简写成：mysql -u root -p

​                Enter password:****

![img](J:\other\other\install\img\clip_image066.jpg)

连接成功后，有关于MySQL Server服务版本的信息，还有第几次连接的id标识。

也可以在命令行通过以下方式获取MySQL Server服务版本的信息

![img](J:\other\other\install\img\clip_image068.jpg)

或**登录**后，通过以下方式查看当前版本信息：

![img](J:\other\other\install\img\clip_image070.jpg)

 

### 方式三：可视化工具

例如：Navicat Preminum，SQLyogEnt等工具

还有其他工具：mysqlfront,phpMyAdmin

#### （1）Navicat Preminum

![img](J:\other\other\install\img\clip_image072.jpg)

![img](J:\other\other\install\img\clip_image074.jpg)

#### （2）SQLyog

![img](J:\other\other\install\img\clip_image076.jpg)

![img](J:\other\other\install\img\clip_image078.jpg)

 



 

# 第三章 linux中mysql安装

### 1.4.1 版本介绍

MySQL 有社区版(Server version: 5.7.31 MySQL Community Server (GPL))和企业版,如果仅仅是从学习角度，直接使用社区版就可以了,只有在需要官方的商业服务的时候才会看出很大区别。主要区别如下 2点:

① 企业版只包含稳定之后的功能，社区版包含所有MySQL的最新功能。也就是说，社区版是企业版的测试版，但是，前者的功能要比后者多。

② 官方的支持服务只针对企业版，用户在使用社区版时出现任何问题，MySQL官方概不负责。至于管理工具，MySQL官方提供的工具都是免费的，从官方网站都可下载到，同样可用在社区版的MySQL上。

### 1.4.2卸载MySQL

第一步：查询mysql ：**rpm -qa|grep mysql**

​                               ![image-20201227095144417](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095144417.png)

第二步：关闭MySQL服务：**systemctl stop mysqld**

第三步：卸载【一定要按顺序卸载】

​       **rpm -e mysql-community-server-5.7.16-1.el7.x86_64**

​       **rpm -e mysql-community-client-5.7.16-1.el7.x86_64**

​       **rpm -e mysql-community-libs-5.7.16-1.el7.x86_64**

​       **rpm -e mysql-community-common-5.7.16-1.el7.x86_64**

 

### 1.4.3下载及安装包介绍

MySQL 官网下载地址：http://dev.mysql.com/downloads/mysql/

 

 ![image-20201227095157256](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095157256.png)

![image-20201227095207044](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095207044.png)

### 1.4.4 检查是否安装过MySQL

第一步：检查是否安装过mysql

​       **CentOS6****：**

​       命令：**rpm –qa|grep mysql**

​       如果存在mysql-libs的旧版本包,请先执行卸载命令：**rpm -e - -nodeps mysql-libs**

​       **CentOS7:**

​       命令：**rpm –qa|grep mariadb**

​       如果存在请先执行命令：**rpm -e --nodeps mariadb-libs**

 

第二步：检查mysql的依赖环境，如果不存在，则进行rpm安装

​       **rpm -qa|grep libaio**

​       **rpm -qa|grep net-tools**

 

第三步：检查/tmp文件夹的权限

​       由于mysql安装过程中，会通过mysql用户在/tmp目录下新建tmp_db文件，所以请给/tmp较大的权限，执行：**chmod -R 777 /tmp**

### 1.4.5 安装MySQL（必须按顺序安装）

 ![image-20201227095215709](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095215709.png)

安装命令：**rpm –ivh** **安装的软件名**

查看安装版本**：****mysqladmin - - version**

查看mysql用户**：** **id mysql**

**提示：如果在检查工作，没有检查mysql****依赖环境，在安装mysql-community-server** **会报错。**

### 1.4.6 MySQL服务初始化    

为了保证数据库目录与文件的所有者为 mysql 登陆用户，如果你是以 root 身份运行 mysql 服务，需要执行命令初始化：**mysqld --initialize --user=mysql**

在进行初始化的时候，可能会遇到如下错误：

 ![image-20201227095223705](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095223705.png)

**解决办法：**只需要将默认的存放mysql数据文件的目录 删除掉，命令：**rm -rf /var/lib/mysql/**，然后再进行执行初始化命令：**mysqld --initialize --user=mysql**

 

另外 --initialize 选项默认以“安全”模式来初始化，会为 root 用户生成一个密码并将该密码标记为过期，登陆后你需要设置一个新的密码，查看密码：**cat /var/log/mysqld.log**

 ![image-20201227095234593](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095234593.png)

### 1.4.7 修改初始化密码

要修改MySQL，首先必须启动MySQL服务，使用初始化密码登录后，才能修改密码：

启动MySQL服务：**systemctl start  mysqld.service**

关闭MySQL服务：**systemctl stop  mysqld.service**

查看MySQL状态：**systemctl status  mysqld.service**

在我们启动的时候可能会报如下错误：

 ![image-20201227095240877](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095240877.png)

我们查看mysql的日志文件：cat /var/log/mysqld.log，可以看到里面的错误日志：

 ![image-20201227095253948](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095253948.png)

**解决方案**：**setenforce 0**，之后我们再次启动mysql，启动成功。

启动成功之后，我们可以查看一下现在的mysql服务：**ps –ef|grep mysql**

 ![image-20201227095259722](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095259722.png)

使用初始化密码进行登录：**mysql -uroot -p'****初始化密码'**

 ![image-20201227095304687](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095304687.png)

利用初始化密码首次登录之后，我们要进行修改密码：ALTER USER 'root'@'localhost' IDENTIFIED BY '新密码';

新密码最好是设置为由数字、大小写字母和特殊字符组成的8位及以上的字符。

设置完新密码之后，我们退出mysql ，再利用新密码进行登录。

 ![image-20201227095314731](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095314731.png)

### 1.4.8 安装目录结构介绍

 ![image-20201227095320942](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095320942.png)

### 1.4.9 MySQL自启动

查看mysql是否为自启动（默认是自启动）：**systemctl list-unit-files|grep mysqld.service**

 ![image-20201227095328543](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095328543.png)

如不是enabled可以运行如下命令设置自启动: **systemctl enable mysqld.service**

### 1.4.10 修改字符集问题

通过**show variables like '%char%';** 可以查看数据库编码问题，会发现默认latin1字符编码，这种字符编码是不支持中文的。

 ![image-20201227095339206](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095339206.png)

**解决办法：**

Ø 第一步：修改vim /etc/my.cnf 文件并在mysqld节点最后添加编码设置。

 ![image-20201227095344884](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095344884.png)

Ø 第二步：重启mysql服务器：systemctl restart mysqld，登录mysql进行查看字符编码。

 ![image-20201227095350408](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095350408.png)

**对于之前已经创建的表，还是litin1****编码，那么该如何更改呢？**

 ![image-20201227095356268](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095356268.png)

**修改以前数据的字符集：alter database** **数据库名 character set 'utf8';**

**修改以前数据表的字符集：alter table****数据表名 convert to character set 'utf8';**

 ![image-20201227095403243](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095403243.png)

  查看字符集编码的命令：**show variables like 'character%';** 或者**show variables like '%char%';**

​    

## 1.5用户与权限管理

### 1.5.1 用户管理

**查看用户**：**select host,user,authentication_string,select_priv,insert_priv,drop_priv from mysql.user;**

 ![image-20201227095409341](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095409341.png)

**创建用户**：**create user spy identified by '1234abc@';**

 ![image-20201227095413844](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095413844.png)

注意：host字段，localhost 字段表示本机访问，%表示远程访问。

查看数据库的当前用户：**select user();**

**设置密码：**

修改某个用户的密码：

**update mysql.user set authentication_string=password('****密码') where user='****用户名';**

**flush privileges;** 【注意】所有通过user表的修改，必须执行该命令才能生效。

**用root****用户修改用户名**：

**update mysql.user set user='****新用户名' where user='****旧用户名';**

**flush prileges;**

**用root****用户删除用户**：

​    **drop user****用户名;** 【注意】删除的时候，即使自己在登录这，也可以将自己删除。

​    不要通过delete from user u where user=’用户名’; 进行删除，因为系统会残留信息。

**拓展：**

 ![image-20201227095421932](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095421932.png)

### 1.5.2 权限管理

**用root****用户授予权限**

命令：grant 权限1,权限2,….权限n on 数据库名.表名 to 用户名@用户地址 identified by ’密码’;

如果发现没有该用户，则会直接创建一个新用户。

例如：给spy用户用本地命令行方式下，授予spy_test 库下的所有表增删改查的权限。

​       

收回权限

收回权限命令：revoke 权限1,权限2,……权限n on 数据库名.表名 from 用户名@用户地址;

例如：收回spy用户对全库全表的所有权限。

​       收回spy用户对mysql库下所有表的增删改查权限。

查看权限

查看当前用户的权限：show grants;

查看某个用户的全局权限：select * from user;

### 1.5.3 通过远程工具访问

步骤：

第一步：先测试是否可以连通数据库服务器的ip地址，确保网络畅通。Ping 数据库服务器ip

第二步：检查数据库服务的防火墙，如果开启则关闭防火墙或者放开3306端口号，并重新加载。

​           **systemctl stop firewalld** 或者**firewall-cmd --zone=public --add-port=3306/tcp –permanent**

第三步：确认mysql 中已经有可以通过远程登录的账户**select host,user,authentication_string from user where host='%';**

​            ![image-20201227095430964](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095430964.png)

​           如果没有可以通过远程登录的账户，先执行如下命令：

grant all privileges on *.* to 用户名@'%' identified by '密码';

flush privileges;

第四步：连接测试。

​            ![image-20201227095437150](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095437150.png)

## 1.6 MySQL配置

**查询所有的系统变量** ：https://dev.mysql.com/doc/refman/5.7/en/server-system-variable-reference.html

**查看mysql****最大连接数：**show variables like 'max_connections';

 ![image-20201227095443675](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095443675.png)

**查看一次连接，最多可以向服务端发送的数据包大小**：show variables like 'max_allow%';

 ![image-20201227095447937](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095447937.png)

**查看用户连接信息**：show processlist; root用户可以查看所有用户的连接，普通用户只可看自己的。

   ![image-20201227095453371](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095453371.png)
 **global****与session****的区别：**

session只对当前窗口生效，但是global对于所有的session都生效，但是需要注意的是global全局参数的设置，对已经开启的session不生效，对于新开启的session才生效。

 ![image-20201227095500541](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20201227095500541.png)

虽然设置了global变量、session变量，但是在mysql服务重启之后，数据库的配置又会按照my.cnf/my.ini配置文件进行重新初始化，所以要永久修改，就需要在my.cnf或者my.ini 配置文件中修改。

