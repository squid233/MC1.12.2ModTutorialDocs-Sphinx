#物品
##创建物品
如果你想偷懒，直接`Item item = new Item();`就可以了。但是这只适用于那些无功能的物品，如钻石。我们要做的是一个有功能的物品。

###新建物品类
就拿`Bubble`当例子吧。  
由于大部分的物品都继承于`Item`类，所以我们也要写一个类来**继承**它。  
首先，新建`com.example.examplemod.common.item.ItemBubble`类。  
然后，粘贴：

    private static String name = "bubble";
    public ItemBubble() {
        this.setRegistryName(name);
        this.setUnlocalizedName(ExampleMod.MODID+"."+name);
        this.setCreativeTab(CreativeTabs.MISC);
    }

`setRegistryName`：设置物品的注册名称  
`setUnlocalizedName`:设置物品的未本地化名称  
`setCreativeTab`:设置物品的创造模式物品栏位置  
现在我们需要注册这个物品。

###注册物品
新建`com.example.examplemod.register.ItemsRegister`类。  
首先在`public class ItemsRegister`上面添加`@Mod.EventBusSubscriber`。  
然后添加`public static final Item BUBBLE = new ItemBubble();`。
创建一个构造方法。

    public ItemsRegister() {
        MinecraftForge.EVENT_BUS.register(this);
    }
    
这里我们不使用古老的`GameRegistry`方法来注册物品，而是使用Forge推荐的注册方法。

    @SubscribeEvent
        public static void registerItems(RegistryEvent.Register<Item> event) {
            event.getRegistry().registerAll(
                    BUBBLE
        );
    }
    
你还可以在`BUBBLE`的下面添加更多的物品，只要确保你用`public static final Item xxx = new ItemXXX();`声明了一个物品并创建了对应的类，以及每个物品之间用了逗号隔开。

最后我们只需要在`CommonProxy`类中的的`preInit`方法中`new ItemsRegister()`即可。

现在物品已经成功注册了，运行游戏看一下效果：
![image1.png](https://i.loli.net/2020/03/08/Ep8eNIfdmGD9iRK.png)  
已经可以在创造模式物品栏的杂项中找到了。  

###国际化与本地化
现在这个物品还没有材质和翻译，所以我们要添加语言文件还有材质文件。
在Resources文件夹下创建一个文件：assets\modid\lang\en_us.lang  
其中modid是你的Mod的ID。  
在en_us.lang中添加如下一行：
`item.examplemod.bubble.name=Bubble`

既然是中国的，那么肯定也要有zh_cn.lang。添加好后，物品就翻译完成了。

###添加材质贴图
物品还需要一个材质，因此，我们需要添加材质贴图。  
首先**在资源管理器中**的assets\examplemod文件夹中新建textures\items文件夹，在里面放入bubble.png文件：
![bubble.png](https://i.loli.net/2020/03/11/ZOWQcxkv6zhFTmS.png)  
接着，