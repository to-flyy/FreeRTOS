#  	FreeRTOS实时操作系统

## FreeRTOS移植：

### 		官方文件：

​	D:\STM32\STM32F103RCT6\FreeRTOS\Official Resource\FreeRTOSv202212.01\FreeRTOSv202212.01

### 		参考视频：

​	https://www.bilibili.com/video/BV1394y1h7ho?vd_source=92221f2a9dae5263c2c9f7cbc96d7b18



## Offical_Experience：

### FreeRTOS中常见的线程间通信方式有以下几种：

1.**队列**（Queue）：队列是FreeRTOS中用于线程间通信的一种方式。线程可以向队列发送消息，也可以从队列接收消息。队列可以实现线程间异步通信，并且支持数据的发送和接收。

2.**信号量**（Semaphore）：信号量是一种用于控制共享资源访问的机制。线程可以对信号量进行Give操作（申请资源）和Take操作（释放资源），从而实现线程对共享资源的互斥访问。

3.**事件组**（Event Group）：事件组是一种用于线程间同步的机制。线程可以等待一个或多个事件的发生，以便继续执行后续的操作。

4.**互斥锁**（Mutex）：互斥锁是一种用于确保临界区代码的互斥访问的机制。通过使用互斥锁，可以保证在同一时间只有一个线程可以访问被保护的临界区代码。

5.**消息队列**（Message Queue）：消息队列是一种提供线程间通信的数据结构，线程可以向消息队列发送消息，也可以从消息队列接收消息。消息队列可以实现线程间数据的传递。



### FreeRTOS任务调度如何实现

FreeRTOS任务调度是通过内核的调度器来实现的。FreeRTOS内核会在初始化时创建一个系统计时器（System Tick Timer），用于定时产生时钟节拍，以便实现任务调度。任务调度器会在每个时钟节拍（tick）时被触发，根据任务的优先级和调度策略来选择下一个要运行的任务。

FreeRTOS内核会维护一个任务列表，包括所有已经创建的任务。任务根据其优先级来排序，具有最高优先级的任务将被选择执行。如果有多个任务具有相同的优先级，则根据调度策略（**抢占式调度或者协作式调度**）来决定下一个要执行的任务。

在每个时钟节拍时，中断会触发任务调度器，调度器会检查任务的状态和优先级，然后选择下一个要运行的任务，并将控制权交给它。如果任务的状态为就绪态，即可以立即执行，调度器会把任务加入到运行队列中，开始执行任务的代码。如果任务的状态为阻塞态，则调度器会将任务放入等待队列中，直到满足任务继续执行的条件。

总的来说，FreeRTOS任务调度是通过内核的调度器来实现的，通过系统计时器产生的时钟节拍来触发调度器运行，并根据任务的优先级和状态来选择下一个要执行的任务。



### FreeRTOS的底层逻辑主要包括：

1.任务管理：FreeRTOS通过任务控制块（TCB）来管理任务。每个任务都有自己的任务控制块，其中包含了任务的状态、优先级、堆栈指针等信息。任务的创建、删除、挂起、恢复等操作都是通过操作任务控制块实现的。

2.任务调度：FreeRTOS通过系统计时器产生的时钟节拍来触发任务调度器。任务调度器根据任务的优先级和调度策略来选择下一个要执行的任务，并切换到该任务进行执行。任务调度器的实现是FreeRTOS的核心功能之一。

3.时间管理：FreeRTOS提供了一系列的时间管理功能，包括延时、定时器、时间戳等。通过这些功能，任务可以进行延时等待、定时执行任务、记录时间戳等操作。

4.中断管理：FreeRTOS支持在中断服务程序中使用RTOS接口。在中断服务程序中，可以使用FreeRTOS提供的中断安全的API来进行任务通知、信号量操作等。

5.资源管理：FreeRTOS提供了信号量、互斥锁、消息队列等机制来实现资源的共享和保护。通过这些机制，可以实现多个任务之间的同步和互斥访问。

总的来说，FreeRTOS的底层逻辑主要包括任务管理、任务调度、时间管理、中断管理和资源管理等方面。这些功能的结合使得FreeRTOS成为一款灵活、高效的嵌入式实时操作系统。



### FreeRTOS的好处

FreeRTOS作为一款流行的嵌入式实时操作系统（RTOS），具有许多优点和好处，使其成为众多开发者选择的首选RTOS。以下是FreeRTOS的一些主要好处：

1. 免费开源：FreeRTOS是一款开源软件，在自由软件基金会（Free Software Foundation）的许可证下发布，可以免费获取、使用和修改。这使得开发者可以方便地使用FreeRTOS构建应用程序，无需额外支付昂贵的授权费用。
2. 轻量级且高效：FreeRTOS设计简单、精巧，且占用资源较小，内核代码紧凑，运行效率高。这使得FreeRTOS适合于应用于资源受限的嵌入式系统中，如微控制器和嵌入式设备。
3. 多任务支持：FreeRTOS支持多任务并发，可以同时运行多个任务，实现任务的灵活调度和管理。开发者可以轻松地创建、删除、挂起、恢复任务，并实时调度任务的执行。
4. 实时性：FreeRTOS是一个实时操作系统，具有可预测的任务调度和响应能力。通过优先级调度器和任务间通信机制，可以实现实时性要求较高的应用程序。
5. 丰富的功能库：除了基本的任务管理、中断处理、时间管理等功能之外，FreeRTOS还提供了丰富的功能库，包括互斥锁、信号量、消息队列、定时器、事件组等，为开发者提供了方便、高效的开发工具。
6. 跨平台支持：FreeRTOS支持多种常见的处理器架构和编译器，并提供了抽象的接口层，使得开发者可以轻松地移植FreeRTOS到不同的硬件平台中。
7. 社区支持：FreeRTOS拥有一个庞大的活跃社区，开发者可以在社区中获取支持、交流经验，获得丰富的资料和资源。



### FreeRTOS怎么合理分配一个任务的栈大小

**在FreeRTOS中合理分配任务的栈大小是非常重要的，因为栈大小的不足或者过大都会对系统的稳定性和性能产生负面影响。以下是一些合理分配任务栈大小的建议：**

1. 了解任务的栈使用情况：在创建任务时，FreeRTOS会根据任务函数的大小自动分配一定大小的栈空间。可以通过调试工具、性能分析工具或者任务函数的复杂性来了解任务实际需要的栈空间。这样可以有针对性地确定任务的栈大小。
2. 考虑函数调用深度：任务函数中的函数调用深度会影响任务的栈使用情况。一般来说，递归函数、嵌套调用较多的函数会占用更多的栈空间。需要根据任务函数的实际调用深度来合理估计栈的大小。
3. 关注局部变量和栈空间：任务函数中声明的局部变量和参数也会占用栈空间。需要考虑任务函数内部所需的局部变量和参数的空间占用，以便估算栈的大小。
4. 考虑中断服务程序的栈空间：在FreeRTOS中，中断服务程序（ISR）也会使用任务的栈空间。需要将中断服务程序的栈空间也考虑在内，以确保栈不会溢出。
5. 使用工具辅助分析：一些工具，如FreeRTOS的配置工具、性能分析工具或者堆栈分析工具，可以帮助开发者合理估算任务的栈大小。通过工具的支持，可以更加直观地了解任务在运行时的栈使用情况。
6. 留有适当的余量：为了防止栈溢出，一般建议在合理估算任务需要的栈大小后，再额外分配一定的余量。这样可以在任务运行过程中应对意外的栈空间占用，提高系统的稳定性。

在实际应用中，合理分配任务的栈大小需要结合任务函数的复杂性、函数调用深度、局部变量占用、中断服务程序的需求等多个因素进行综合考量。通过合理的估算和预留适当的余量，可以保证任务的栈大小能够满足任务的运行需求，提高系统的稳定性和性能。



### FreeRTOS两个任务之间是怎么切换的，原理是什么

**在FreeRTOS中，任务之间的切换是通过协作式调度和抢占式调度两种方式实现的。**

1. 协作式调度：
	- 在协作式调度中，任务自行让出CPU使用权，通过显式地调用任务切换函数 `taskYIELD()` 或者 `vTaskDelay()` 来触发任务切换。
	- 当一个任务主动调用任务切换函数时，FreeRTOS会根据任务的优先级等信息，选择下一个要运行的任务，并切换到该任务的上下文执行。
	- 协作式调度适用于非常高可预测性的应用场景，因为任务之间的切换是显式调用的，所以可以确保任务在适当位置进行切换。
2. 抢占式调度：
	- 在抢占式调度中，任务在特定条件下（如时间片耗尽、中断发生等）被系统强制切换，而不需要任务明确地调用任务切换函数。
	- 当一个任务的时间片用完，或者有更高优先级任务就绪时，FreeRTOS会立即进行任务切换，将CPU资源分配给更高优先级的任务。
	- 抢占式调度可以更好地响应实时事件，提高系统的实时性能。

任务之间的切换原理主要在任务切换时保存和恢复任务的上下文信息。当任务切换时，FreeRTOS会保存当前任务的寄存器值、堆栈指针等相关信息，然后恢复下一个要执行的任务的上下文，使得下一个任务可以继续执行。在任务的切换过程中，FreeRTOS确保了任务间的数据隔离和资源共享，保证系统的数据一致性和稳定性。

总的来说，FreeRTOS实现任务之间的切换通过协作式调度和抢占式调度两种方式，通过保存和恢复任务的上下文信息来实现任务的快速切换。不同的调度方式可以适应不同的应用场景，开发者可以根据具体的需求选择合适的调度方式来实现任务的协同工作。



## My_Experience:

### 任务：

​	**创建任务，可在任务里执行程序，如LED闪烁；队列，信号量，事件都是在任务里执行。**



### 队列：

​	**创建队列->写队列->读队列**

​	**在队列中可以存储数据，在任务中读取数据；比如在串口中断写队列即发送串口接收到的数据，在任务中读取该队列发送的数据即读队列，读到队列的数据再进行判断数据为什么值时进行代码逻辑编写。**



### 信号量：

#### 计数值信号量：

​	**就是设置最大计数值和初始计数值，通过释放信号量Give使计数值+1，获取信号量Take使计数值-1，当超出最大计数值使释放信号量Give失败，当无计数值使获取信号量Take失败。**

#### 二值信号量：

​	**简易就是只有二进制的值0-1，释放信号量Give使计数值+1，获取信号量Take使计数值-1，当超出最大计数值使释放信号量Give失败，当无计数值使获取信号量Take失败。**

#### 互斥信号量：



### 事件：

​	**设置若干个条件为事件组的位，当该些条件都成立执行代码逻辑。**



### 任务通知：

​	**就是发送任务通知->获取任务通知，一对一**

#### 二值信号量的任务通知：

​	**先 发送任务通知，发送的句柄是 接收任务通知 的句柄，即实现一对一；**

​	**二值信号量的说法就是，只要成功发送任务通知，就一定能实现接收任务通知 0-1。**



#### 计数值信号量的任务通知：

​	**和直接计数值信号量没啥区别，操作流程差不多**

​	**和二值信号量区别就是pdTRUE和pdFALSE**



#### 消息队列的任务通知：

​	  **我个人感觉采用任务通知实现消息队列过于鸡肋；**

​	**采用这种方法时，我需要在蓝牙中断中每判断一次接收的值才发送一个任务通知；**

​	**又因为任务通知是一对一的，所以我发送的值就只能对应一个获取任务通知，一个任务就需要一个获取任务通知；**

​	**每一个值，都需要发送任务通知和获取任务通知，多个值就需要多个；**

 	**相比队列，我只需要把 发送队列放进串口中断，他会把里面的值发送，然后只需要一个任务去读队列的值；**

 	**在读队列的值时直接判断接收的值，一个任务就能解决；**

 	**相比这种，每个任务通知只对应一个句柄时只能获取一个值，太麻烦；**

  	
  	

#### 事件的任务通知：

​	**和直接事件没啥区别**

​	**无非就是当多个条件同时触发时才跑**



## 常用API函数：

### **任务调度器函数：**

```c
vTaskStartScheduler();					//开启任务调度器
```



### 延迟函数：

**这两个延时函数一旦被调用，当前任务会立马进入*阻塞状态*，而自己写的延时函数(以for循环等形式实现的软件延时)会被当做有效任务而一直执行(自己的Delay函数会占用CPU资源)。**

**相对延时vTaskDelay()**

**相对延时是指每次延时都是从任务执行函数vTaskDelay()开始，延时指定的时间结束；**

```c
vTaskDelay();							//系统时钟节拍周期
```

**绝对延时vTaskDelayUntil()**

**绝对延时是指每隔指定的时间，执行一次调用vTaskDelayUntil()函数的任务。换句话说：任务以固定的频率执行。**

```c
vTaskDelayUntil(TickType_t * pxPreviousWakeTime,//指针，指向一个变量
                TickType_t xTimeIncrement//周期循环时间
               );
```



### 删除函数：

```c
vTaskDelete(任务句柄/NULL(任务本身));
```

### 挂起函数：

**被挂起的任务不再执行,直到任务被恢复**

```c
vTaskSuspend(任务句柄/NULL(任务本身));		//挂起任务
```

### 任务恢复函数：

```c
vTaskResume(任务句柄/NULL(任务本身));		//恢复任务
```

### 任务中断恢复函数：

```c
xTaskResumeFromISR(任务句柄/NULL(任务本身));
```





## 任务创建：

### 	动态任务：

​	**操作系统来动态分配任务所需空间大小**

```c
BaseType_t xTaskCreate(    TaskFunction_t pvTaskCode,				//任务函数名
                            const char * const pcName,				//任务名称（字符串）
                            configSTACK_DEPTH_TYPE usStackDepth,	//任务堆栈大小（128/...）
                            void *pvParameters,						//任务传递参数（NULL/...）
                            UBaseType_t uxPriority,					//任务优先级
                            TaskHandle_t *pxCreatedTask				//任务句柄 需要加&
                          );
```

​	**句柄：**用于描述这个任务的结构体或结构体指针，以后对这个任务操作，比如启动，挂起，删除，调整优先级等等，都是用这个句柄来表示对应的任务

![image-20240307202830705](C:/Users/86135/AppData/Roaming/Typora/typora-user-images/image-20240307202830705.png)



### 静态任务：

​	由我们自己去指定空间大小

```c
TaskHandle_t xTaskCreateStatic( 	TaskFunction_t pxTaskCode,			任务函数名
                                    const char * const pcName,			任务名称（字符串）
                                    const uint32_t ulStackDepth,		任务堆栈大小（128/...）
                                    void * const pvParameters,			任务传递参数（NULL/...）
                                    UBaseType_t uxPriority,				任务优先级
                                    StackType_t * const puxStackBuffer,	任务堆栈（传入的堆栈大小）
                                    StaticTask_t * const pxTaskBuffer )	任务控制块
```

​	**接口函数**(放main函数下面)

```c
StaticTask_t IdleTaskTCB;		
StackType_t IdleTaskStack[configMINIMAL_STACK_SIZE];

/*接口函数	指定内存大小和任务控制块*/
void vApplicationGetIdleTaskMemory( 	StaticTask_t 	**ppxIdleTaskTCBBuffer,		任务控制块
                                        StackType_t 	**ppxIdleTaskStackBuffer,	堆栈空间
                                        uint32_t 		*pulIdleTaskStackSize )		堆栈空间大小
{
	*ppxIdleTaskTCBBuffer = &IdleTaskTCB;
	*ppxIdleTaskStackBuffer = IdleTaskStack;
	*pulIdleTaskStackSize = configMINIMAL_STACK_SIZE;
}
```

![image-20240307201911271](C:/Users/86135/AppData/Roaming/Typora/typora-user-images/image-20240307201911271.png)



### 多任务创建：

**借助一个开始任务创建 也可 直接创建**

![image-20240307211740396](C:/Users/86135/AppData/Roaming/Typora/typora-user-images/image-20240307211740396.png)



## 打印函数（临界区）

由串口发送信息是**非线程安全**，需要保护发送信息的函数

### 临界区实现代码保护

**为了保证PORTA的访问不被中断，将访问操作放入临界区运行**

**进入临界区：**

```c
taskENTER_CRITICAL()
```

**退出临界区：**

```c
taskEXIT_CRITICAL()
```

![image-20240307214427495](C:/Users/86135/AppData/Roaming/Typora/typora-user-images/image-20240307214427495.png)





## 变量名定义：

​	**c		char**

​	**s		int16_t	short**

​	**l		int32_t	long**

​	**x		BaseType_t， 其他非标准的类型：结构体、task handle、queue handle**

​	**u		unsigned**

​	**p		指针**

​	**uc		uint8_t	unsigned char**

​	**pc		char 指针**



## 任务调度含义：

​	**高优先级任务未执行完，低优先级任务无法运行**	

​	**一旦高优先级任务就绪，拿上运行**

​	**最高优先级任务有多个，它们轮流运行**



## 队列：

**创->写->读->删**

### 	动态队列创建：

**返回值**

**非 0：成功，返回句柄，以后使用句柄来操作队列** 

**NULL：失败，因为内存不足**

```c
QueueHandle_t xQueueCreate(UBaseType_t uxQueueLength,   //队列长度，最多能存放多少个数据(item)
                           UBaseType_t uxItemSize		//每个数据(item)的大小：以字节为单位
                           );	
```



### 静态队列创建：

**返回值 非 0：成功，返回句柄，以后使用句柄来操作队列 NULL：失败，因为 pxQueueBuffer 为 NULL**

```c
QueueHandle_t xQueueCreateStatic(UBaseType_t uxQueueLength,	//队列长度，最多能存放多少个数据(item)
                                 UBaseType_t uxItemSize,	//每个数据(item)的大小：以字节为单位
                                 uint8_t *pucQueueStorageBuffer,//如果 uxItemSize 非 0，pucQueueStorageBuffer 必须指向一个 uint8_t 数组，此数组大小至少为"uxQueueLength * uxItemSize"
                                 StaticQueue_t *pxQueueBuffer//必须执行一个 StaticQueue_t 结构体，用来保存队列
的数据结构
 								);
```



### 删除队列：

**只能删除使用动态方法创建的队列，它会释放内存**

```c
void vQueueDelete( QueueHandle_t xQueue );
```



### 队列发送图解：

![image-20240408214640569](C:/Users/86135/AppData/Roaming/Typora/typora-user-images/image-20240408214640569.png)

### 写队列：

**可以把数据写到队列头部，也可以写到尾部**

**返回值 pdPASS：数据成功写入了队列 **

**errQUEUE_FULL：写入失败，因为队列满了。**

**消息放队首优先执行**

```c
BaseType_t xQueueSend(QueueHandle_t xQueue,	//队列句柄，要写哪个队列
                      const void *pvItemToQueue,//数据指针 在创建队列时已经指定了数据大小
                      TickType_t xTicksToWait//xTicksToWait 表示阻塞的最大时间如果被设为 0，无法读出数据时函数会立刻返回；如果被设为 portMAX_DELAY，则会一直阻塞直到有数据可写
 					  );
```

 

**往队列头部写入数据，此函数可以在中断函数中使用，不可阻塞**

**返回值：**

**pdTRUE: 消息成功发送**

**errQUEUE_FULL: 发送失败**

```c
BaseType_t xQueueSendToFrontFromISR(QueueHandle_t xQueue,//队列句柄
                                    const void *pvItemToQueue,//指针，指向队尾发送的消息(前面定义)
                                    BaseType_t *pxHigherPriorityTaskWoken//NULL	
 									);

```



### 读队列：

**返回值 pdPASS：从队列读出数据入**

 **errQUEUE_EMPTY：读取失败，因为队列空了**

**接收完消息后删除该消息**

```c
BaseType_t xQueueReceive(QueueHandle_t xQueue,//队列句柄，要写哪个队列
                         void * const pvBuffer,//bufer 指针 在创建队列时已经指定了数据大小
                         TickType_t xTicksToWait //xTicksToWait 表示阻塞的最大时间如果被设为 0，无法读出数据时函数会立刻返回；如果被设为 portMAX_DELAY，则会一直阻塞直到有数据可写
                        );
```



**返回值：**

**pdTRUE: 返回成功**

**pdFALSE: 返回失败**

**中断接受**

```c
BaseType_t xQueueReceiveFromISR(QueueHandle_t xQueue,
                                void *pvBuffer,
                                BaseType_t *pxTaskWoken
                               );

```







## 参数定义：

### portTICK_RATE_MS：

​	[1ms时间周期](https://so.csdn.net/so/search?q=1ms时间周期&spm=1001.2101.3001.7020)

### taskYIELD()：

**每个task都是不会睡眠的不停的执行自己,当每个task觉得自己占用cpu的时间已经差不多的时候,**

**主动让出cpu,让同优先级的其他task获得cpu,因为没有其他优先级的task,所以调度器不会切换优先级,**



### portMAX_DELAY：

**表示一直处于阻塞等待中**

**当值为0时，表示不需要阻塞等待**



## 信号量：

### 	二值信号量：

**0-1**

 **返回值: 返回句柄，非 NULL 表示成功**

**创建二值信号量**

```c
SemaphoreHandle_t xSemaphoreCreateBinary( void );
```



### 删除信号量：

**对于动态创建的信号量，不再需要它们时，可以删除它们以回收内存。**

**返回值：pdTRUE 表示成功**

**如果二进制信号量的计数值已经是 1，再次调用此函数则返回失 败； 如果计数型信号量的计数值已经是最大值，再次调用此函数则返 回失败**

```c
void vSemaphoreDelete( SemaphoreHandle_t xSemaphore );//信号量句柄，释放哪个信号量
```



### 释放信号量：

**使信号量+1**

**返回值：**

**pdTRUE 表示成功**

**如果二进制信号量的计数值已经是 1，再次调用 此函数则返回失败； 如果计数型信号量的计数值已经是最大值，再 次调用此函数则返回失败**

```c
BaseType_t xSemaphoreGive( SemaphoreHandle_t xSemaphore );
```

### 中断中释放信号量：

**返回值：**

**pdTRUE 表示成功**

**如果二进制信号量的计数值已经是 1，再次调用 此函数则返回失败； 如果计数型信号量的计数值已经是最大值，再 次调用此函数则返回失败**

```c
BaseType_t xSemaphoreGiveFromISR(SemaphoreHandle_t xSemaphore,//信号量句柄，释放哪个信号量
                                 BaseType_t *pxHigherPriorityTaskWoken//如果释放信号量导致更高优先级的任务变为了
//就绪态，则*pxHigherPriorityTaskWoken = pdTRUE
                                 );
```



### 获取信号量：

**使信号量-1**

**返回值** 

**默认为pdPASS**

**pdTRUE 表示成功** **当有信号量时**

```c
BaseType_t xSemaphoreTake(SemaphoreHandle_t xSemaphore,//信号量句柄，释放哪个信号量
                          TickType_t xTicksToWait// 如果无法马上获得信号量，阻塞一会：
//0：不阻塞，马上返回
//portMAX_DELAY: 一直阻塞直到成功
                         );

```



### 在中断获取：

```c
BaseType_t xSemaphoreTakeFromISR(SemaphoreHandle_t xSemaphore,//信号量句柄，释放哪个信号量
                        	     BaseType_t *pxHigherPriorityTaskWoken
                   				);
```



### 计数值信号量：

**返回值:** 

**返回句柄**

**非 NULL 表示成功**

```c
SemaphoreHandle_t xSemaphoreCreateCounting(UBaseType_t uxMaxCount, //最大计数值
                                           UBaseType_t uxInitialCount//初始计数值
                                          );
```



### 互斥信号量：

 **返回值: 返回句柄**

**非 NULL 表示成功**

```c
SemaphoreHandle_t xSemaphoreCreateMutex( void );
```



## 事件：

### 创建动态事件：

 **返回值:**

**返回句柄，**

**非 NULL 表示成功**

```c
EventGroupHandle_t xEventGroupCreate( void );
```



### 事件删除：

```c
void vEventGroupDelete( EventGroupHandle_t xEventGroup ) //事件组句柄
```



### 设置事件组的位：

```c
EventBits_t xEventGroupSetBits( EventGroupHandle_t xEventGroup,	//事件组句柄
 								const EventBits_t uxBitsToSet //设置哪些位?
                              );
```



### 中断设置事件组的位：

```c
BaseType_t xEventGroupSetBitsFromISR( EventGroupHandle_t xEventGroup,//事件组句柄
 									  const EventBits_t uxBitsToSet,//设置哪些位?
 									  BaseType_t * pxHigherPriorityTaskWoken //有没有导致更高优先级的任务进入就绪态? pdTRUE-有, pdFALSE-没有
                                    );
```



### 等待事件发生：

```c
EventBits_t xEventGroupWaitBits( EventGroupHandle_t xEventGroup,//事件组句柄
                                 const EventBits_t uxBitsToWaitFor,//等待哪些位？
                                 const BaseType_t xClearOnExit,// 函数提出前是否要清除事件？
//pdTRUE: 清除 uxBitsToWaitFor 指定的位
//pdFALSE: 不清除
                                 const BaseType_t xWaitForAllBits,// 怎么测试？是"AND"还是"OR"？
//pdTRUE: 等待的位，全部为 1;
//pdFALSE: 等待的位，某一个为 1 即可

                                 TickType_t xTicksToWait//如果期待的事件未发生，阻塞多久。
//可以设置为 0：判断后即刻返回；
//可设置为 portMAX_DELAY：一定等到成功才返回；
//可以设置为期望的 Tick Count，一般用 pdMS_TO_TICKS()把ms 转换为 Tick Count

                               );
```



### 清楚事件（标志位置零）：

```c
EventBits_t xEventGroupClearBits( EventGroupHandle_t xEventGroup, //事件组句柄
								  const EventBits_t uxBitsToClear//清除你要等待的位
							    );
```





## 任务通知：

### 任务通知发送函数：

#### 头文件：

​	**#include "limits.h"**  **宏默认打开**

|             函数             |                             描述                             |
| :--------------------------: | :----------------------------------------------------------: |
|        xTaskNotify()         | 发送通知，带有通知值并且不保留接收任务原通知值，用在任务中。 |
|     xTaskNotifyFromISR()     |           发送通知，函数xTaskNotify()的中断版本。            |
|      xTaskNotifyGive()       | 发送通知，不带通知值并且不保留接收任务的通知值，此函数会将接收任务的通知值加一，用于任务中。 |
|   vTaskNotifyGiveFromISR()   |         发送通知，函数xTaskNotifyGive()的中断版本。          |
|    xTaskNotifyAndQuery()     | 发送通知，带有通知值并且保留接收任务的原通知值，用在任务中。 |
| XTaskNotiryAndQueryFromISR() | 发送通知，函数xTaskNotifyAndQuery()的中断版本，用在中断服务函数中。 |

#### **eAction取值：**

```c
typedef enum
{   
    eNoAction=0,
    eSetBits,//更新指定的bit
    elncrement,//通知值加一
    eSetValueWithOverwrite,//覆写的方式更新通知值
    eSetValueWithoutOverwrite//不覆写通知值
}eNotifyAction;

```



| 参数          |                             描述                             |
| ------------- | :----------------------------------------------------------: |
| xTaskToNotify |          任务句柄，指定任务通知是发送给哪个任务的。          |
| ulValue       |                         任务通知值。                         |
| eAction       | 任务通知更新的方法，eNotifyAction是个枚举类型，在文件task.h中有定义 |
| 返回值        | pdFAIL：当参数eAction设置为eSetValueWithoutOverwrite的时候，如果任务通知值没有更新成功就返回pdFAIL。pdPASS：eAction设置为其他选项的时候统一返回pdPASS。 |

```c
BaseType_t xTaskNotify(TaskHandle_t xTaskToNotify,//任务句柄 不需要加&
                       uint32_t ulValue,//任务通知值	需要加&
                       eNotifyAction eAction//任务通知更新的方法
                      );
```

**（通常用于事件组）**





| 参数          | 描述                                       |
| ------------- | ------------------------------------------ |
| xTaskToNotify | 任务句柄，指定任务通知是发送给哪个任务的。 |
| 返回值        | pdPASS：此函数只会返回pdPASS。             |

（**专门用于二值信号量任务传输**）

```c
BaseType_t xTaskNotifyGive(TaskHandle_t xTaskToNotify);	//句柄无需加&
```

​	

#### 中断任务通知：

|           参数            |                             描述                             |
| :-----------------------: | :----------------------------------------------------------: |
|       xTaskToNotify       |          任务句柄，指定任务通知是发送给哪个任务的。          |
|          ulValue          |                         任务通知值。                         |
|          eAction          |                     任务通知更新的方法。                     |
| pxHigherPriorityTaskWoken | 记退出此函数以后是否进行任务切换，这个变量的值函数会自动设置的，用户不用进行设置，用户只需要提供一个变量来保存这个值就行了。当此值为pdTRUE的时候在退出中断服务函数之前一定要进行一次任务切换。 |
|          返回值           | pdFAIL：当参数eAction设置为eSetValueWithoutOverwrite的时候，如果任务通知值没有更新成功就返回pdFAIL。pdPASS：eAction设置为其他选项的时候统一返回pdPASS。 |

```c
BaseType_t xTaskNotifyFromISR(TaskHandle_t xTaskToNotify,
							  uint32_t ulValue,
                              eNotifyAction eAction,
                              BaseType_t*pxHigherPriorityTaskWoken
                             );
```





|           参数            |                             描述                             |
| :-----------------------: | :----------------------------------------------------------: |
|       xTaskToNotify       |          任务句柄，指定任务通知是发送给哪个任务的。          |
| pxHigherPriorityTaskWoken | 记退出此函数以后是否进行任务切换，这个变量的值函数会自动设置的，用户不用进行设置，用户只需要提供一个变量来保存这个值就行了。当此值为pdTRUE的时候在退出中断服务函数之前一定要进行一次任务切换。 |

```c
void vTaskNotifyGiveFromlSR(TaskHandle_t xTaskHandle,			  //对应接收任务通知的句柄
							BaseType_t* pxHigherPriorityTaskWoken //NULL
                           );
```

**（MINE 常用）**



### 获取任务通知：

|        函数        |                             描述                             |
| :----------------: | :----------------------------------------------------------: |
| ulTaskNotifyTake() | 获取任务通知，可以设置在退出此函数的时候将任务通知值清零或者减一。**当任务通知用作二值信号量或者计数信号量的时候使用此函数来获取信号量。** |
| xTaskNotifyWait()  | 等待任务通知，比ulTaskNotifyTak()更为强大，全功能版任务通知获取函数。 |



#### **ulTaskNotifyTake()**

（**适用于二值信号量和记值信号量**）

|       参数        |                             描述                             |
| :---------------: | :----------------------------------------------------------: |
| XClearCountOnExit | 参数为pdFALSE的话在退出函数ulTaskNotifyTake()的时候任务通知值减一，类似计数型信号量。当此参数为pdTRUE的话在退出函数的时候任务任务通知值清零，类似二值信号量。 |
|    xTickToWait    |                          阻塞时间。                          |
|      返回值       |            任何值：任务通知值减少或者清零之前的值            |

```c
uint32_t ulTaskNotifyTake(BaseType_t xClearCountOnExit,//pdFALSE用于记值信号量 pdTRUE用于二值信号量
						 TickType_t xTicksToWait
                        );
```



#### **xTaskNotifyWait()**

（**不管任务通知用作二值信号量、计数型信号量、队列和事件标志组中的哪一种，都可以使用此函数来获取任务通知**）

|         参数         |                             描述                             |
| :------------------: | :----------------------------------------------------------: |
| ulBitsToClearOnEntry | 当没有接收到任务通知的时候将任务通知值与此参数的取反值进行按位与运算，当此参数为0xffffffff或者ULONG_MAX的时候就会将任务通知值清零。 |
| ulBitsToClearOnExit  | 如果接收到了任务通知，在做完相应的处理退出函数之前将任务通知值与此参数的取反值进行按位与运算，当此参数为0xffffffff或者ULONG_MAX的时候就会将任务通知值清零。 |
| pulNotificationValue |                  此参数用来保存任务通知值。                  |
|     xTickToWait      |                          阻塞时间。                          |
|        返回值        |    pdTRUE：获取到了任务通知。pdFALSE：任务通知获取失败。     |

```c
BaseType_t xTaskNotifyWait(uint32_t ulBitsToClearOnEntry,	//0x0进入函数不清除任务bit
                           uint32_t ulBitsToClearOnExit,	//ULONG_MAX退出函数清除所有的bit
                           uint32_t* pulNotificationValue,	//任务通知值 需要加&
                           TickType_t xTicksToWait			//portMAX_DELAY/0
                          );
```

