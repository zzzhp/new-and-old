# new-and-old
温故：
	资源的释放问题：
		java中需要手动释放的资源目前接触的主要有 1）io流资源 2）jdbc资源
		关闭原则主要是先开后关，从里到外。
		具体实现方法为放在try-catch-finally语句块中。
		其中对于流的关闭，jdk1.7以上还实现了try-with-resources语句，其原理与上述方法相同。
