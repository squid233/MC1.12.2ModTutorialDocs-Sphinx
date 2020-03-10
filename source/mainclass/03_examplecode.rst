示例代码
--------

ExampleMod.java
~~~~~~~~~~~~~~~

::

   package com.example.examplemod;

   import com.example.examplemod.proxy.CommonProxy;
   import net.minecraft.init.Blocks;
   import net.minecraftforge.fml.common.Mod;
   import net.minecraftforge.fml.common.Mod.EventHandler;
   import net.minecraftforge.fml.common.SidedProxy;
   import net.minecraftforge.fml.common.event.FMLInitializationEvent;
   import net.minecraftforge.fml.common.event.FMLPreInitializationEvent;
   import org.apache.logging.log4j.Logger;

   @Mod(modid = ExampleMod.MODID, name = ExampleMod.NAME, version = ExampleMod.VERSION)
   public class ExampleMod
   {
       public static final String MODID = "examplemod";
       public static final String NAME = "Example Mod";
       public static final String VERSION = "1.0";

       @Mod.Instance(ExampleMod.MODID)
       private static ExampleMod instance;

       @SidedProxy
               (clientSide = "com.example.examplemod.proxy.ClientProxy",
               serverSide = "com.example.examplemod.proxy.CommonProxy"
               )
       private static CommonProxy proxy;

       private static Logger logger;

       @EventHandler
       public void preInit(FMLPreInitializationEvent event)
       {
           logger = event.getModLog();
           logger.info("preInit");
           proxy.preInit(event);
       }

       @EventHandler
       public void init(FMLInitializationEvent event)
       {
           // some example code
           logger.info("DIRT BLOCK >> {}", Blocks.DIRT.getRegistryName());
           proxy.init(event);
       }
   }

CommonProxy.java
~~~~~~~~~~~~~~~~

::

   package com.example.examplemod.proxy;

   import com.example.examplemod.register.*;
   import net.minecraftforge.fml.common.event.FMLInitializationEvent;
   import net.minecraftforge.fml.common.event.FMLPreInitializationEvent;

   public class CommonProxy {
       public void preInit(FMLPreInitializationEvent event) {

       }

       public void init(FMLInitializationEvent event) {

       }

   }

ClientProxy.java
~~~~~~~~~~~~~~~~

::

   package com.example.examplemod.proxy;

   import net.minecraftforge.fml.common.event.FMLInitializationEvent;
   import net.minecraftforge.fml.common.event.FMLPreInitializationEvent;

   public class ClientProxy extends CommonProxy{
       @Override
       public void preInit(FMLPreInitializationEvent event) {
           super.preInit(event);
       }

       @Override
       public void init(FMLInitializationEvent event) {
           super.init(event);
       }
   }

--------------

你的Mod最基本的已经配置完成，很快我们将做出第一个物品。