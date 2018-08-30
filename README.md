# new-and-old  
## 温故：
###	资源的释放问题：
		java中需要手动释放的资源目前接触的主要有 1）io流资源 2）jdbc资源
		关闭原则主要是先开后关，从里到外。
		具体实现方法为放在try-catch-finally语句块中。
		其中对于流的关闭，jdk1.7以上还实现了try-with-resources语句，其原理与上述方法相同。
### 事务的操作以及数据库锁机制：
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
