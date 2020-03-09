主类
====

每个Mod都会有一个主类，每一个主类都会有一个\ ``@Mod``\ 注解。下面这个例子展示出了\ ``@Mod``\ 注解如何使用（注：以后所有的例子都会以ExampleMod为准，请根据自己的需求更改）：

::

   @Mod(modid = ExampleMod.MODID, name = ExampleMod.NAME, version = ExampleMod.VERSION)
   public class ExampleMod
   {
       public static final String MODID = "examplemod";
       public static final String NAME = "Example Mod";
       public static final String VERSION = "1.0";
   }

MODID, NAME,
VERSION就不必解释了。接下来我们在\ ``public static final String VERSION = "1.0";``\ 这段代码的后面添加上下面的代码：

::

   @Mod.Instance(ExampleMod.MODID)
       private static ExampleMod instance;

这段代码用于保存Mod的实例。

然后创建两个新类，分别是\ ``com.example.examplemod.proxy.ClientProxy``\ 和\ ``com.example.examplemod.proxy.CommonProxy``\ 。

在\ ``CommonProxy``\ 中添加如下代码：

::

   public void preInit(FMLPreInitializationEvent event) {

       }

   public void init(FMLInitializationEvent event) {

       }

然后在ClientProxy中添加如下代码：

::

   @Override
   public void preInit(FMLPreInitializationEvent event) {
       super.preInit(event);
   }

   @Override
   public void init(FMLInitializationEvent event) {
       super.init(event);
   }

注意：\ ``ClientProxy``\ 继承于\ ``CommonProxy``\ 。

现在回到\ ``ExampleMod``\ 类，在\ ``private static ExampleMod instance;``\ 的下面加上如下代码：

::

   @SidedProxy
           (clientSide = "com.example.examplemod.proxy.ClientProxy",
            serverSide = "com.example.examplemod.proxy.CommonProxy"
           )
   private static CommonProxy proxy;

接下来在主类的\ ``preInit``\ 方法中加上\ ``proxy.preInit(event);``\ ，在\ ``init``\ 方法中加上\ ``proxy.init(event);``\ 。

--------------

你的Mod最基本的已经配置完成，很快我们将做出第一个物品。