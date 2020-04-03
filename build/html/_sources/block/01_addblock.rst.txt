添加方块
========

是时候添加方块了。新建common.block包，并新建ExampleBlock类，然后让ExampleBlock类继承Block类。在里面写上如下代码：

::

    public ExampleBlock() {
        super(Material.GROUND, MapColor.DIRT);
        String name = "example_block";
        this.setRegistryName(name).setUnlocalizedName(ExampleMod.MODID+"."+name).setCreativeTab(CreativeTabs.MISC).setHardness(0.5f).setResistance(10);
    }

| setHardness:设置方块硬度。
| setResistance:设置方块爆炸抗性。

注册方块
--------

我们在register包下新建BlocksRegister类，在里面写上如下代码：

::

    @Mod.EventBusSubscriber
    public class BlocksRegister {
        public static final Block EXAMPLE_BLOCK = new ExampleBlock();

        public BlocksRegister() {
            MinecraftForge.EVENT_BUS.register(this);
        }

        private static Block[] blocks = {
                EXAMPLE_BLOCK
        };

        @SubscribeEvent
        public static void registerBlocks(RegistryEvent.Register<Block> event) {
            for (Block block : blocks) {
                ModelLoader.setCustomModelResourceLocation(Item.getItemFromBlock(block), 0, new ModelResourceLocation(block.getRegistryName(), "inventory"));
                event.getRegistry().register(block);
            }
        }

        @SubscribeEvent
        public static void registerItemBlocks(RegistryEvent.Register<Item> event) {
            for (Block block : blocks) {
                Item itemBlock = new ItemBlock(block).setRegistryName(block.getRegistryName());
                ModelLoader.setCustomModelResourceLocation(itemBlock, 0, new ModelResourceLocation(block.getRegistryName(), "inventory"));
                event.getRegistry().register(itemBlock);
            }
        }
    }

方块就注册完成了。

I18n
----

我们在en_us.lang中写上

::

    tile.examplemod.example_block.name=Example Block

这样就能看到方块的名字了。

添加方块模型
------------

::

    Blockstate: src/main/resources/assets/examplemod/blockstates/example_block.json
    Block Model: src/main/resources/assets/examplemod/models/block/example_block.json
    Item Model: src/main/resources/assets/examplemod/models/item/example_block.json
    Block Texture: src/main/resources/assets/examplemod/textures/block/example_block.png

blockstates/example_block.json

::

    {
    "variants": {
        "": { "model": "examplemod:block/example_block" }
        }
    }

models/block/example_block.json

::

    {
    "parent": "block/cube_all",
    "textures": {
        "all": "examplemod:block/example_block"
        }
    }

models/item/example_block.json

::

    {
        "parent": "examplemod:block/example_block"
    }

textures/block/example_block.png

|image.png|

掉落物
------

在ExampleBlock中添加：

::

    @Override
    public Item getItemDropped(IBlockState state, Random rand, int fortune) {
        return Item.getItemFromBlock(this);
    }

.. |image.png| image:: https://i.loli.net/2020/04/03/w8fN3gA6QyVOTo1.png