4.正式开始构建开发环境
======================

按下Shift＋右键，选择在此处打开命令窗口或PowerShell

| 输入：
| ``gradlew setupDecompWorkspace``
| 这个过程非常耗时间，建议大家搜索Lss233's.Mirror();
| **如果出现BUILD FAILED请重新输入该指令**

| ``gradlew genIntellijRuns``
| **如果出现BUILD FAILED请重新输入该指令**

| 当出现BUILD SUCCESSFUL的时候，差不多就大功告成了。
| 注：BUILD SUCCESSFUL长这个样子：\ |image3.png|

| 之后将其导入IDEA，并点击Gradle面板中的刷新按钮，以确保你的项目能正常工作。
| |image4.png|

还需要设置一下：按下Ctrl+Alt+S，然后按图片中的设置。 |image5.png|

按下Ctrl+Alt+Shift+S，将\ ``Project Compiler Output``\ 设定为\ ``~\out``\ ，其中\ ``~``\ 是你的Mod目录。最后，指定Project
SDK为1.8版本。

--------------

到此为止，工作环境已经配置好了，下一期我们将配置主类和Mod信息

.. |image3.png| image:: https://i.loli.net/2020/03/07/bn4ypjoAvCeKWSw.png
.. |image4.png| image:: https://i.loli.net/2020/03/09/Nz5iqy1dlXjxVna.png
.. |image5.png| image:: https://i.loli.net/2020/03/09/5jWbD2Q3uAFvd4N.png