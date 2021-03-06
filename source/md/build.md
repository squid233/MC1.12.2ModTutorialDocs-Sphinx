#构建环境
##1.JDK下载
若想制作Mod，必须先构建好开发环境。你需要下载的版本是JDK1.8.0

---
##2.选择IDE
Java运行时环境已经安装完成，接下来就是选择IDE了。这里推荐使用IntelliJ IDEA。  
![image.png](https://i.loli.net/2020/03/07/IEoZKgqejMTJb9d.png)
选择右边免费的社区版下载并安装。
---
##3.Forge MDK包
IDEA安装好后，该下载Forge MDK包了。点击左侧的1.12.2，点击下载MDK。这里用的版本是2847
![image.png](https://i.loli.net/2020/03/07/ZEbznyDOTpMSf6u.png)
包下载好后，将其解压到**全英文路径**（如果不是全英文路径你会遇到一些奇怪的问题）
---
##4.构建开发环境
按下Shift＋右键，选择在此处打开命令窗口或PowerShell 

输入：  
`gradlew setupDecompWorkspace`  
这个过程非常耗时间，建议大家搜索Lss233's.Mirror();  
**如果出现BUILD FAILED请重新输入该指令**  

`gradlew genIntellijRuns`  
**如果出现BUILD FAILED请重新输入该指令**  

当出现BUILD SUCCESSFUL的时候，差不多就大功告成了。  
注：BUILD SUCCESSFUL长这个样子：![image.png](https://i.loli.net/2020/03/07/bn4ypjoAvCeKWSw.png)  

之后将其导入IDEA，并点击Gradle面板中的刷新按钮，以确保你的项目能正常工作。  
![image.png](https://i.loli.net/2020/03/09/Nz5iqy1dlXjxVna.png)

还需要设置一下：按下Ctrl+Alt+S，然后按图片中的设置。
![image.png](https://i.loli.net/2020/03/09/5jWbD2Q3uAFvd4N.png)  
  
按下Ctrl+Alt+Shift+S，将`Project Compiler Output`设定为`~\out`，其中`~`是你的Mod目录。最后，指定Project SDK为1.8版本。  

---
到此为止，工作环境已经配置好了，下一期我们将配置主类和Mod信息