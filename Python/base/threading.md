## threading

### Thread类
#### 实例化定义传入参数
- target   
	- 指定进程的任务函数地址
- args   
	- 指定任务函数的参数，元组格式传入
- kwargs   
	- 指定任务函数的参数，字典格式传入
- 示例

	```python
	from threading import Thread, get_ident
	import time
	
	
	def task(num):
	    print(get_ident(), "开始运行", num)
	    time.sleep(1)
	    print(get_ident(), "结束运行")
	
	
	for i in range(5):
	    t = Thread(target=task, args=(i,))
	    t.start()
	```

#### 方法   
- start
	- 向操作系统发送线程开启请求(开线程必须有的方法)
- join
	- 主线程等待线程结束
	- 参数timeout，设定等待时间
- getName
	- 获取当前线程名
- isDaemon   
	- 判断当前线程是否是守护线程
- isAlive   
	- 判断当前线程是否未结束

#### 属性
- daemon
	- True时设置线程为主线程的守护线程
	- 当主线程等待所有非守护线程结束后，守护线程被回收
	- 必须在startfan方法启用前使用
- name
	- 当前线程名
- ident
	- 当前线程id

### Queue类
- 参数maxsize
	- 队列允许的最大项数，省略则无限制
- put
	- 插入数据到队列中
	- 参数blocked 
		- False时，当Queue已满则抛出异常
	- 参数timeout
		- blocked为True时，当Queue已满时，阻塞指定时长，超时则抛出异常
- get
	- 从队列读取并且删除一个元素
	- 参数blocked
		- False时，当Queue为空立即抛出异常
	- 参数timeout 
		- blocked为True时，Queue为空时,阻塞指定时长，超时抛出异常
- close
	- 关闭队列，防止队列加入更多数据
	- 后台线程会继续写入已经加入队列但尚未写入的数据
- JoinableQueue子类
	- 生产者消费者模型适用
	- task_down
		- 消费者使用此方法表示q.get()的返回项目已经被处理
	- join
		- 生产者调用此方法进行阻塞，知道队列之中所有项目均被处理，阻塞会持续到队列每个项目均调用q.task_done()

### Lock类
- acquire
	- 当前进程/线程独享下文资源，直到l.release()
- release
	- 解除当前进程/线程独享上文资源的状态
- RLock递归锁
	- 可以解决单线程加锁造成的死锁现象
- Semaphore信号量
	- 可以设置使用资源的进程/线程数目上限
	- 即同一把锁可以被使用的次数，默认锁只能用一次，递归锁除外

### Event类
- isset
	- 返回Event状态量
- wait
	- 如果状态量为False，则阻塞；状态量为True，停止阻塞
	- 参数timeout，设置最大等待时间
- set
	- 设置状态量为True
- clear
	- 设置状态量为False

### Timer类
#### 方法
- currentThread
- get_ident
- activeCount
- enumerate
- main_thread
