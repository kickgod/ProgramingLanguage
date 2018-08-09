<a id="top" href="#top">:checkered_flag: C# 文件和流 :blue_heart:</a> 
----
- [x] :whale2: <a href="#SystemFileManagement">`管理文件系统`</a>
    * <a href="#DriveInfo">  `DriveInfo 检查驱动信息` </a>
    * <a href="#Path">  `Path 路径类` </a>
    * <a href="#File">  `File 文件操作` </a>
    * <a href="#FileInfo">  `FileInfo 文件对象` </a>
    
#### <a href="#SystemFileManagement" id="SystemFileManagement">管理文件系统</a>
* `FileSystemInfo`：`这是表示任何文件系统对象的基类`
* `FileInfo和 File`：`这些类表示文件系统上面的文件`
* `DirectoryInfo和Directory`：`这些类表示文件系统上面的目录`
* `Path`:`这个类包含的静态成员可以用于处理路径名`
* `DriveInfo`:`它的属性和方法提供了指定驱动器的信息`

```c# 
                      基类
               FileSystemInfo
              /              \
             / 继承            \ 继承 
            /                   \   
    DirectoryInfo             FileInfo   

    File[静态类]        Directory[静态类] 
```
* `Directory和File类只包含静态犯法,不能实例化.只要调用一个成员方法,提供合适的文件系统对象的路径,就可以使用这些类.如果只对文件夹或文件执行一个操作这些类
十分有效`
* `DirectoryInfo,FileInfo实现与Directory和File类有大致相同的公共方法,并拥有一些公共属性和构造函数,但他们都是有状态的,并且这些类的成员都不是静态的
需要实例化这些类,之后吧每个实例与特定的文件或者文件夹关联起来。`

#####  <a id="DriveInfo" href="#DriveInfo">  `DriveInfo 检查驱动信息` </a>
[`DirveInfo`](https://msdn.microsoft.com/zh-cn/library/system.io.driveinfo(v=vs.110).aspx) `类可以用于检查驱动器信息,可以描述驱动器列表还可以进一步提供任何关于驱动器的大量细节`
* 构造函数
  * `DriveInfo(String)`:	 `提供对有关指定驱动器的信息的访问。`
* 属性
	* `AvailableFreeSpace`	`指示驱动器上的可用空闲空间总量（以字节为单位）。`
	* `DriveFormat`	`获取文件系统的名称，例如 NTFS 或 FAT32。`
	* `DriveType`	`获取驱动器类型，如 CD-ROM、可移动、网络或固定`
	* `IsReady`	`获取一个指示驱动器是否已准备好的值。`
	* `Name`	`获取驱动器的名称，如 C:\。`
	* `RootDirectory`	`获取驱动器的根目录。`
	* `TotalFreeSpace`	`获取驱动器上的可用空闲空间总量（以字节为单位）。`
	* `TotalSize`	`获取驱动器上存储空间的总大小（以字节为单位）。`
	* `VolumeLabel`	`获取或设置驱动器的卷标。`
* 方法 只有一个方法有用
  * `GetDrives()`:`检索计算机上的所有逻辑驱动器的驱动器名称。`

```C#
      static void Main(string[] args)
      {
          DriveInfo[] drives=DriveInfo.GetDrives();
          foreach(DriveInfo drive in drives){
              if(drive.IsReady){
                  Console.WriteLine("---------------------------------------------------");
                  Console.WriteLine($"磁盘名称:{drive.Name}");
                  Console.WriteLine($"磁盘格式:{drive.DriveFormat}");
                  Console.WriteLine($"磁盘类型:{drive.DriveType}");
                  Console.WriteLine($"磁盘根目录:{drive.RootDirectory}");
                  Console.WriteLine($"磁盘卷标:{drive.VolumeLabel}");
                  Console.WriteLine($"磁盘空余空间:{drive.TotalFreeSpace}");
                  Console.WriteLine($"磁盘可利用大学:“{drive.AvailableFreeSpace}"); 
                  Console.WriteLine($"磁盘总大小:{drive.TotalSize}");
              }
          }   
      }
      //输出
      ---------------------------------------------------
      磁盘名称:C:\
      磁盘格式:NTFS
      磁盘类型:Fixed
      磁盘根目录:C:\
      磁盘卷标:
      磁盘空余空间:79885795328
      磁盘可利用大学:“79885795328
      磁盘总大小:127440777216
      ....
```
##### [Path](https://msdn.microsoft.com/zh-cn/library/system.io.path(v=vs.110).aspx) 路径类 <a id="Path"></a>
`对包含文件或目录路径信息的 String 实例执行操作。 这些操作是以跨平台的方式执行的。`  **`静态列`**

* Path 字段
   * `AltDirectorySeparatorChar`:	`提供平台特定的替换字符，该替换字符用于在反映分层文件系统组织的路径字符串中分隔目录级别。`
   * `DirectorySeparatorChar`	:`提供平台特定的字符，该字符用于在反映分层文件系统组织的路径字符串中分隔目录级别。`
   * `InvalidPathChars[过时]`	:`已过时。 提供平台特定的字符数组，这些字符不能在传递到 Path 类的成员的路径字符串参数中指定。`
   * `PathSeparator`:	`用于在环境变量中分隔路径字符串的平台特定的分隔符。`
   * `VolumeSeparatorChar`:	`提供平台特定的卷分隔符。`
* 方法
   * `Combine(String[])`:`将字符串数组组合成一个路径。`
   * `GetDirectoryName(String)`:`返回指定路径字符串的目录信息。`
   * `GetExtension(String)[重要]`:`返回指定的路径字符串的扩展名`
   * `GetFileName(String)[重要]`:`返回指定路径字符串的文件名和扩展名`
   * `GetFileNameWithoutExtension(String)[重要]`:`返回不具有扩展名的指定路径字符串的文件名`
   * **`GetFullPath(String)[重要]`**:`返回指定路径字符串的绝对路径`
   * **`HasExtension(String)[重要]`**:`确定路径是否包括文件扩展名`
   * `IsPathRooted(String)`:`获取一个值，该值指示指定的路径字符串是否包含根`
   * `GetInvalidFileNameChars()`:`获取包含不允许在文件名中使用的字符的数组`
   * `GetInvalidPathChars()`:`获取包含不允许在路径名中使用的字符的数组`
   * `GetPathRoot(String)`:`获取指定路径的根目录信息`
   * `GetTempFileName()`:`在磁盘上创建磁唯一命名的零字节的临时文件并返回该文件的完整路径`
   * `GetTempPath()`:`返回当前用户的临时文件夹的路径`
```C#
      string path2 = @"G:\Acigela\DotnetConsole2\resource";
      string path3 = @"filtering-labels.html";
      string path4 = @"G:\Acigela\DotnetConsole2\resource\multi-axis.html";

      Console.WriteLine($"{Path.AltDirectorySeparatorChar}");
      Console.WriteLine($"{Path.DirectorySeparatorChar}");
      Console.WriteLine($"{Path.PathSeparator}");
      Console.WriteLine($"{Path.VolumeSeparatorChar}");

      //	Combine(String, String)
      Console.WriteLine($"路径: {Path.Combine(path2,path3)}");
      //	GetDirectoryName(String)
      Console.WriteLine($"目录信息:{Path.GetDirectoryName(path4)}");  
      //	GetInvalidFileNameChars()
      foreach(var i in Path.GetInvalidFileNameChars()){
          Console.WriteLine($"文件禁止字符:{i}");
      }

      //	GetInvalidPathChars()
      foreach(var i in Path.GetInvalidPathChars()){
          Console.WriteLine($"路径禁止字符:{i}");
      }
      //  GetRandomFileName() 	返回随机文件夹名或文件名
      Console.WriteLine($"{Path.GetRandomFileName()}");
      // 	GetTempFileName() 在磁盘上创建磁唯一命名的零字节的临时文件并返回该文件的完整路径
      Console.WriteLine($"{Path.GetTempFileName()}");
      //  GetTempPath() 返回当前用户的临时文件夹的路径
      Console.WriteLine($"{Path.GetTempPath()}");
```
##### [File](https://msdn.microsoft.com/zh-cn/library/system.io.file(v=vs.110).aspx) 文件操作 <a id="File"></a>
`提供用于创建、复制、删除、移动和打开单一文件的静态方法，并协助创建 FileStream 对象。静态类`
* 文件编码:[Encoding 类](https://msdn.microsoft.com/zh-cn/library/system.text.encoding(v=vs.110).aspx)  `System.Text.Encoding`

* 方法
  * **`AppendAllLines(String, IEnumerable<String>)`**:`向一个文件中追加行，然后关闭该文件。 如果指定文件不存在，此方法会创建一个文件，向其中写入指定的行，然后关闭该文件`
  * **`AppendAllLines(String, IEnumerable<String>, Encoding)`**:`使用指定的编码向一个文件中追加行，然后关闭该文件。 如果指定文件不存在，此方法会创建一个文件，向其中写入指定的行，然后关闭该文件`
  * **`AppendAllText(String, String)`**:`打开一个文件，向其中追加指定的字符串，然后关闭该文件。 如果文件不存在，此方法将创建一个文件，将指定的字符串写入文件，然后关闭该文件。`
  * **`AppendAllText(String, String, Encoding)`**:`将指定的字符串追加到文件中，如果文件还不存在则创建该文件。`
  * **`AppendText(String)`**:`创建一个 StreamWriter，它将 UTF-8 编码文本追加到现有文件或新文件（如果指定文件不存在）`
  * **`Copy(String, String)[重要]`**:`将现有文件复制到新文件。 不允许覆盖同名的文件。`
  * **`Copy(String, String, Boolean)`**:`将现有文件复制到新文件。 允许覆盖同名的文件。`
  * **`Create(String)`**:`在指定路径中创建或覆盖文件。`
  * **`Create(String, Int32)`**:`创建或覆盖指定的文件。`
  * **`Create(String, Int32, FileOptions)`**:`创建或覆盖指定的文件，指定缓冲区大小和一个描述如何创建或覆盖该文件的 FileOptions 值。`
  * **`Create(String, Int32, FileOptions, FileSecurity)`**:`创建或覆盖具有指定的缓冲区大小、文件选项和文件安全性的指定文件`
  * **`CreateText(String)[重要]`**:`创建或打开用于写入 UTF-8 编码文本的文件`
  * **`Decrypt(String)`**:`使用 Encrypt 方法解密由当前帐户加密的文件`
  * **`Exists(String)`**:`确定指定的文件是否存在`
  * **`Encrypt(String)`**:`将某个文件加密，使得只有加密该文件的帐户才能将其解密`
  * **`GetAccessControl(String)`**:`获取一个 FileSecurity 对象，它封装指定文件的访问控制列表 (ACL) 条目`
  * **`Move(String, String)[重要]`**:`将指定文件移到新位置，提供要指定新文件名的选项。`
  * **`Open(String, FileMode)`**:`以读/写访问权限打开指定路径上的 FileStream`
  * **`Open(String, FileMode, FileAccess)`**:`以指定的模式和访问权限打开指定路径上的 FileStream。`
  * **`Open(String, FileMode, FileAccess, FileShare)`**:`打开指定路径上的 FileStream，具有带读、写或读/写访问的指定模式和指定的共享选项`
  * **`OpenRead(String)`**:`打开现有文件以进行读取`
  * **`OpenText(String)`**:`打开现有 UTF-8 编码文本文件以进行读取`
  * **`OpenWrite(String)`**:`	打开一个现有文件或创建一个新文件以进行写入`
  * **`ReadAllBytes(String)`**:`打开一个二进制文件，将文件的内容读入一个字节数组，然后关闭该文件。`
  * **`ReadAllLines(String)`**:`打开一个文本文件，读取文件的所有行，然后关闭该文件`
  * **`ReadAllLines(String, Encoding)`**:`打开一个文件，使用指定的编码读取文件的所有行，然后关闭该文件`
  * **`Replace(String, String, String)`**:`使用其他文件的内容替换指定文件的内容，这一过程将删除原始文件，并创建被替换文件的备份。`
  * **`Replace(String, String, String, Boolean)`**:`用其他文件的内容替换指定文件的内容，这一过程将删除原始文件，并创建被替换文件的备份，还可以忽略合并错误。`
  * **`WriteAllText(String, String, Encoding)`**:`创建一个新文件，使用指定编码向其中写入指定的字符串，然后关闭文件。 如果目标文件已存在，则覆盖该文件`
  * **`WriteAllText(String, String)`**:`创建一个新文件，向其中写入指定的字符串，然后关闭文件。 如果目标文件已存在，则覆盖该文件`
  * **`WriteAllLines(String, String[], Encoding)`**:`创建一个新文件，使用指定编码在其中写入指定的字符串数组，然后关闭该文件`
  * **`WriteAllLines(String, String[])`**:`建一个新文件，在其中写入指定的字节数组，然后关闭该文件`
  * **`WriteAllLines(String, IEnumerable<String>)`**:`创建一个新文件，向其中写入一个字符串集合，然后关闭该文件`
  * **`WriteAllLines(String, IEnumerable<String>, Encoding)`**:`使用指定的编码创建一个新文件，向其中写入一个字符串集合，然后关闭该文件`
  * **`WriteAllBytes(String, Byte[])`**:`创建一个新文件，在其中写入指定的字节数组，然后关闭该文件。 如果目标文件已存在，则覆盖该文件`
  * **`SetAttributes(String, FileAttributes)`**:`获取指定路径上的文件的指定 FileAttributes。`

##### `按行读出文件`
```C#
     var path=@"resource\filtering-labels.html";
     Console.WriteLine($"绝对路径 Path :{Path.GetFullPath(path)}");
     if(File.Exists(path)){
         //按照行读出文件
         var listallline=File.ReadAllLines(path,Encoding.UTF8);
          foreach(var line in listallline){
              Console.WriteLine(line);   
          }
     }
```
##### `覆盖或者新建文件 修改内容为`

* 文件覆盖内容
```C#
     /*覆盖文件 */     
     var pathw=@"resource\user.cs"; 

     File.WriteAllText(pathw," using System;\n using System.Text;\n using System.IO;\n using System.
     Collections.Generic;\n using System.Collections;using System.Threading; \n using System.Threading.Tasks;"); 
```
* 按照行覆盖文件
```C#
      var path=@"resource\filtering-labels.html";
      List<String> str=new List<string>();

      if(File.Exists(path)){
          //按照行读出文件
          var listallline=File.ReadAllLines(path,Encoding.UTF8);
              foreach(var line in listallline){
                  str.Add(line);
              }
      }
     /*覆盖或者新建文件*/     
     var pathw=@"resource\index.html";

     File.WriteAllLines(pathw,str,Encoding.UTF8);
```
##### 追加文件

* 追加文件字符串
```C#
     /*追加文件 */     
    var pathw=@"resource\user.cs"; 

    File.AppendAllText(pathw," using System;\n using System.Text;\n using System.IO;\n using
    System.Collections.Generic;\n using System.Collections;using System.Threading; 
    \n using System.Threading.Tasks;"); 

```
* 按照行追加文件
```C#
    var path=@"resource\multi-axis.html";
    List<String> str=new List<string>();

    if(File.Exists(path)){
        //按照行读出文件
        var listallline=File.ReadAllLines(path,Encoding.UTF8);
            foreach(var line in listallline){
                str.Add(line);
            }
    }
    /*覆盖或者新建文件*/     
    var pathw=@"resource\index.html";

    File.AppendAllLines(pathw,str,Encoding.UTF8); 
```

##### `创建文件`
```C#
   //创建UTF-8 的文本文件
   File.CreateText("resource/ac.cs");
   File.CreateText("resource/index.html");
   // 创建文件 注意是文件 不能创建目录
   File.Create("resource/sd.md");
```
##### `删除文件`
```C#
   /*删除文件*/     
   var pathw=@"resource\sd.md";
   if(File.Exists(pathw)){
        File.Delete(pathw);
   }
```
##### `复制文件`
```C#
   /*复制文件*/     
   var pathw=@"resource\indexs.html";
   Console.WriteLine($"{Path.GetDirectoryName(pathw)}\\2016110418xing.html");
   if(File.Exists(pathw)){
       File.Copy(pathw, $"{Path.GetDirectoryName(pathw)}\\2016110418xing.html",true);
       File.Delete(pathw);
   }
```
##### `移动文件`
`根据随机文件名称,重命名文件`
```C#
   /*移动文件*/     
   string code="qwertyuiopasdfghjklzxcvbnm".ToUpper();
   Random r=new Random();
   int val= r.Next(0,code.Length);	//会产生0 但是不会产生26
   int valt= r.Next(0,code.Length);	//会产生0 但是不会产生26
   var now=DateTime.Now;
   var pathw=@"resource\GP20188918343995.html";
   var name=$"{Path.GetDirectoryName(pathw)}\\{code[val]}{code[valt]}{now.Year}{now.Month}{now.Day}
   {now.Hour}{now.Minute}{now.Second}{now.Millisecond}{Path.GetExtension(pathw)}";
   var pathnew=$"{Path.GetFullPath(name)}";
    Console.WriteLine($"新文件路径: {pathnew}");
    if(File.Exists(pathw)){
        File.Move(pathw, pathnew);
    }
```
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  