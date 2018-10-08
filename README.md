# new-and-old  
## 温故:
### 资源的释放问题:
		java中需要手动释放的资源目前接触的主要有 1）io流资源 2）jdbc资源
		关闭原则主要是先开后关，从里到外。
		具体实现方法为放在try-catch-finally语句块中。
		其中对于流的关闭，jdk1.7以上还实现了try-with-resources语句，其原理与上述方法相同。
### 事务的操作以及数据库锁机制:
		Spring框架提供了编程式事务管理和声明式事务管理
		编程式事务管理：
			可以清楚地控制事务的边界
			可自行实现事务开始时间、结束时间、撤消操作的时机等
			可以实现细粒度的事务控制
		声明式事务管理：
			好处是事务管理的API不介入程序，最符合一个非侵入型轻量级容器的理想
			多数情况下事务不需要细粒度控制，因此建议使用

		锁的种类主要有 1）共享锁 2）更新锁 3）排它锁 4）意向锁 5）计划锁
		加更新锁的含义为 其他事务可以读，但是不能加锁。这样就解决了死锁问题。
		表被锁的原因：
			1）字段不加索引:在执行事务的时候，如果表中没有索引，会执行全表扫描，如果这时候有其他的事务过来，就会发生锁表！
			2）事务处理时间长:事务处理时间较长，当越来越多事务堆积的时候，会发生锁表！
			3）关联操作太多:涉及到很多张表的修改等，在并发量大的时候，会造成大量表数据被锁！
		锁表解决方式：
			1）通过相关的sql语句可以查出是否被锁定，和被锁定的数据！
			2）为加锁进行时间限定，防止无限死锁！
			3）加索引，避免全表扫描！
			4）尽量顺序操作数据！
			5）根据引擎选择合理的锁粒度！
			6）事务中的处理时间尽量短！
### jdbcTemplate:
		jdbcTemplate类是Spring对JDBC支持类库中的核心类
		jdbcTemplate负责：
			创建和释放资源
			执行SQL语句、存储过程，并通过ResultSet来返回数据
			
### ajax:
		$.ajax({  
		     type: "POST",  
		     url: "/login",  
		     contentType: 'application/x-www-form-urlencoded;charset=utf-8',  
		     data: {username:$("#username").val(), password:$("#password").val()},  
		     dataType: "json",  
		     success: function(data){  
				 console.log(data);  
			      }，  
		     error:function(e){  
				 console.log(e);  
		     }  
		 });  
### Hadoop:
		环境搭建
		组件构成和功能
		代码示例
### Linux
		常见目录：
			根目录下的bin和sbin，usr目录下的bin和sbin，这四个目录用来保存系统命令。
			boot启动目录。
			dev特殊文件保存目录。
			etc系统配置文件目录。
			root超级用户的家目录，home普通用户的家目录。
			lib函数库的保存位置。
			media，mnt，misc（空目录）外接存储设备
			proc和sys是保存的是内存的挂载点，不能直接操作。
			tmp临时目录
			usr系统软件资源目录
			var保存系统可变文档目录
		常见命令（命令 [选项] [参数] ）：
			ls 查询目录中内容
			vi 编辑文件
			touch 创建文件
			cat 打印文件内容
			mkdir 建立目录 -p 递归创建
			cd 切换所在目录
			pwd 查询所在目录位置
			rmdir 删除目录（只能删除空白目录）
			rm -rf 删除目录或文件 -r 删除目录 -f 强制
			cp 复制命令 -a 相当于 -pdf所有内容都复制
			mv 剪切或改名命令（在不同文件是复制，相同位置是改名）
			ln 连接命令 -s 软连接（类似Windows中的快捷方式）
			locate 文件搜索命令（在后台数据库中搜索）
			find	文件搜索命令（能进行全目录搜索，也可按搜索范围和条件搜索）
			whereis 命令搜索命令（能看帮助文档所在地）
			which 命令搜索命令（能看别名）
			grep 搜索字符命令
			man 帮助命令 -f 查看级别 -k 查看包含某字符的所有命令
			--help 其他帮助命令
			help 只能获取shell内部命令帮助
			info 详细帮助命令
			wget 文件下载命令
			zip 压缩文件 -r 压缩目录 gzip bzip2（不能压缩目录）
			unzip 解压缩 gunzip bunzip2
			tar -zcvf压缩.tar.gz -jcvf 压缩.tar.bz2
			tar -zxvf解压缩 -jcxf解压缩
			shotdown [选项] 时间 -c 取消上一个命令 -h 关机 -r 重启
			logout 退出登录命令
			mount 挂载命令
			w 查看登录用户信息 
			echo 输出命令 -e 支持控制字符转换
			history 历史命令
## 知新:
### p3c:
		p3c是阿里的java代码规约插件，可以对自身起一个很好的规范作用。
### quartz:
		quartz是由java编写的作业调度框架，在spring中可以很方便的完成定时任务。
		quartz主要由Schedule（任务调度器），Job（作业任务）和Trigger（触发器）三部分组成。
		其中Job配置你想要定时执行的方法，Trigger配置你要执行方法的时间（运用cron表达式）,Schedule用来将两者结合到一起。
### MYbatis:
		MyBatis 主要完成两件事情
			1）根据JDBC 规范建立与数据库的连接
			2）通过Annotaion/XML+JAVA反射技术,实现 Java 对象与关系数据库之间相互转化
### maven:
		maven项目就是在java项目和web项目的上面包裹了一层maven。
		maven主要是通过pom配置文件去导入jar包，而不用去手动导入。
		maven需要从仓库中导入需要的jar包，仓库分为本地仓库，第三方仓库和中央仓库。
### spring boot
		代码:[https://github.com/zzzhp/springboot-study/]
		SpringBoot构造并且返回一个json对象
		SpringBoot使用devtools进行热部署
		SpringBoot资源属性配置
		SpringBoot整合模板引擎
		SpringBoot异常处理
		SpringBoot整合MyBatis
		SpringBoot整合Redis
		SpringBoot整合定时任务
		SpringBoot整合异步任务
		SpringBoot使用拦截器
### kafka
		Kafka是一个分布式的、可分区的、可复制的消息系统。它提供了普通消息系统的功能，但具有自己独特的设计。
		首先让我们看几个基本的消息系统术语：
		Kafka将消息以topic为单位进行归纳。
		将向Kafka topic发布消息的程序成为producers.
		将预订topics并消费消息的程序成为consumer.

