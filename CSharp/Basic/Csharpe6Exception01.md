<a id="top" href="#">:running:</a> 异常错误处理 :bird:
-----
`工作流可以使用 TryCatch 活动处理工作流执行期间引发的异常。 可以对这些异常进行处理，或者使用 Rethrow 活动重新引发异常。 Finally 节中的活动在 Try 节或 Catches 节完成时执行。 由工作流承载WorkflowApplication实例还可以使用OnUnhandledException事件处理程序来处理未由处理的异常TryCatch活动。`

- [x] :mountain_bicyclist:	<a href="#ExceptionResultFrom">**`异常原因`**</a>
- [x] :mountain_bicyclist:	<a href="#ExceptionClassLibrary">**`异常类`**</a>
- [x] :mountain_bicyclist:	<a href="#CatchException">**`捕获类`**</a>
- [x] :mountain_bicyclist:	<a href="#ClassException">**`Exception类`**</a>
- [x] :mountain_bicyclist:	<a href="#ExceptionWhen">**`异常过滤器`**</a>
- [x] :mountain_bicyclist:	<a href="#ThrowException">**`抛出异常`**</a>
- [x] :mountain_bicyclist:	<a href="#DefineByUserException">**`用户自定义异常`**</a>
   
##### 数据准备 <a id="ExceptionResultFrom"></a>  :closed_umbrella: <a href="#top"> `置顶` :arrow_up:</a>
* `在工作流中，异常可能通过下列方式生成：`
    * TransactionScope 中的事务超时。

    * 工作流通过使用 Throw 活动引发的显式异常。

    * 某个活动引发的 .NET Framework 4.6.1 异常。

    * 外部代码引发的异常，例如工作流中使用的库、组件或服务。
    
##### 异常类 <a id="ExceptionClassLibrary"></a>  :closed_umbrella: <a href="#top"> `置顶` :arrow_up:</a>
**`Exception 类`** `是所有异常类的基类,所有异常类都在System名称空间中,但IOException类,CompositionException类和派生于这两个类的类除外.IOException 在System.IO名称空间中,CompositionException及其派生类在System.ComponentModel.Composition名称空间中,该空间处理部件和组件的动态加载.`    

* 1、`SystemException类`:`该类是System命名空间中所有其他异常类的基类。都.NET运行库抛出的异常（建议：公共语言运行时引发的异常通常用此类）`
* 2、`ApplicationException类`：`该类表示应用程序发生非致命错误时所引发的异常（建议：应用程序自身引发的异常通常用此类）`   

* 与参数有关的异常类 `此类异常类均派生于SystemException，用于处理给方法成员传递的参数时发生异常`

  * `ArgumentException类`：`该类用于处理参数无效的异常，除了继承来的属性名，此类还提供了string类型的属性ParamName表示引发异常的参数名称。`
  * `FormatException类`：`该类用于处理参数格式错误的异常。`
  * `StackOverFlowException类`:`分配给栈的内存已经满了`
* 与成员访问有关的异常

  * `MemberAccessException类：该类用于处理访问类的成员失败时所引发的异常。失败的原因可能的原因是没有足够的访问权限，也可能是要访问的成员根本不存在（类与类之间调用时常用）`
  * `MemberAccessException类的直接派生类：`
    * `FileAccessException类：该类用于处理访问字段成员失败所引发的异常`
    * `MethodAccessException类：该类用于处理访问方法成员失败所引发的异常`
    * `MissingMemberException类：该类用于处理成员不存在时所引发的异常`
* 与数组有关的异常 `均继承于SystemException类`
  * `IndexOutOfException类：该类用于处理下标超出了数组长度所引发的异常`
  * `ArrayTypeMismatchException类：该类用于处理在数组中存储数据类型不正确的元素所引发的异常`
  * `RankException类：该类用于处理维数错误所引发的异常`
* 与IO有关的异常
  * `IOException类`：`类用于处理进行文件输入输出操作时所引发的异常。`
  * `IOException类的5个直接派生类：`
    * `DirectionNotFoundException类`：`该类用于处理没有找到指定的目录而引发的异常。`
    * `FileNotFoundException类`：`该类用于处理没有找到文件而引发的异常。`
    * `EndOfStreamException类`：`该类用于处理已经到达流的末尾而还要继续读数据而引发的异常。`
    * `FileLoadException类`：`该类用于处理无法加载文件而引发的异常。`
    * `PathTooLongException类`：`该类用于处理由于文件名太长而引发的异常。`
* 与算术有关的异常
  * `ArithmeticException类：该类用于处理与算术有关的异常。`
  * `ArithmeticException类的派生类：`
  * `DivideByZeroException类：表示整数货十进制运算中试图除以零而引发的异常。`
  * `NotFiniteNumberException类：表示浮点数运算中出现无穷打或者非负值时所引发的异常。`
##### 捕获类 <a id="CatchException"></a>  :closed_umbrella: <a href="#top"> `置顶` :arrow_up:</a>
* 子类在前 基类在后
* Finally 一定执行
```C#
  try{
       int[] i={1,5,6,9,2,12};
       WriteLine(i[20]);

   }catch(IndexOutOfRangeException ex){
       WriteLine(ex.Message);
   }catch(Exception e){
       WriteLine(e.Message);
   }finally{
       WriteLine("释放资源");    
   }
```
##### [Exception类](https://msdn.microsoft.com/zh-cn/library/system.exception(v=vs.110).aspx) <a id="ClassException"></a>  :closed_umbrella: <a href="#top"> `置顶` :arrow_up:</a>
* 构造函数

|名称|	说明|
|:----|:----|
|Exception()|	初始化 Exception 类的新实例。|
|Exception(SerializationInfo, StreamingContext)	 |用序列化数据初始化 Exception 类的新实例。|
|Exception(String)	|用指定的错误消息初始化 Exception 类的新实例。|
|Exception(String, Exception)	 |使用指定的错误消息和对作为此异常原因的内部异常的引用来初始化 Exception 类的新实例。|
* 属性

|名称|	说明|
|:----|:----|
|[`Data`](https://msdn.microsoft.com/zh-cn/library/system.exception.data(v=vs.110).aspx)|获取提供有关异常的其他用户定义信息的键/值对集合。|
|HelpLink |获取或设置指向与此异常关联的帮助文件链接。  |
|HResult |获取或设置 HRESULT（一个分配给特定异常的编码数字值）。  |
|InnerException |获取导致当前异常的 Exception 实例。  |
|Message |获取描述当前异常的消息。  |
|Source |获取或设置导致错误的应用程序或对象的名称。 |
|StackTrace |获取引发当前异常的方法。  |
* 方法

|名称|	说明|
|:----|:----|
|Finalize() |在垃圾回收将某一对象回收前允许该对象尝试释放资源并执行其他清理操作。（继承自 Object。） |
	

```C#
    try{
        throw new MyException(404);
    }catch(MyException ex) when (ex.ErrorCode==404){
        WriteLine("网页跳转错误");                
    }
```
##### 异常过滤器 <a id="ExceptionWhen"></a>  :closed_umbrella: <a href="#top">置顶 :arrow_up:</a>
`when 关键字`
```C#
    try{
        throw new MyException(404);
    }catch(MyException ex) when (ex.ErrorCode==404){
        WriteLine("网页跳转错误");                
    }
```
##### 抛出异常 <a id="ThrowException"></a>  :closed_umbrella: <a href="#top">置顶 :arrow_up:</a>
`使用throw关键字抛出异常`
##### 用户自定义异常 <a id="DefineByUserException"></a>  :closed_umbrella: <a href="#top">置顶 :arrow_up:</a>
`用户自定义异常需要基础相应的基类,通过继承实现异常类,抛出接受异常的方法与系统定义异常相同`

* 用户自定义的异常可以在实现了基类的基本构造函数后,添加用户自己需要的属性和方法

```C#
    public class MyException : System.Exception
    {
        public int ErrorCode{get;set;}
        public MyException(int errorCode) {this.ErrorCode=errorCode; }
        public MyException(string message,int errorCode) : base(message) { this.ErrorCode=errorCode;}
        public MyException(string message, System.Exception inner) : base(message, inner) { }
        protected MyException(
            System.Runtime.Serialization.SerializationInfo info,
            System.Runtime.Serialization.StreamingContext context) : base(info, context) { }
    }
```
