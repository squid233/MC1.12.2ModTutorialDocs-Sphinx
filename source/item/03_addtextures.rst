添加物品贴图
============

物品已经翻译好了，接下来就该添加物品材质了。

首先创建文件夹\ ``assets/[modid]/textures/items``\，将\ ``bubble.png``\放进去： |image1.png|

之后还需要创建文件\ ``assets/[modid]/models/item/bubble.json``\。文件的内容如下：

::

    {
        "parent": "minecraft:item/generated",
        "textures": {
            "layer0": "examplemod:items/bubble"
        }
    }

- \ ``item/generated``\：使用默认的物品渲染方式

- \ ``layer0``\：使用第0层图层

- \ ``examplemod:items/bubble``\：寻找assets文件夹下的examplemod下的textures下的items下的bubble.png（好长

现在物品模型渲染文件也做好了，接下来，到注册材质的时候了。

注册物品材质
------------

| 要注册材质，我们首先在register文件夹下新建\ ``ModelsRegister``\类。
| 然后我们需要输入

::

    public ModelsRegister() {
        MinecraftForge.EVENT_BUS.register(this);
    }

注：这次不需要在开头加上注解了。

接着我们需要

::

    @SubscribeEvent
    public void registerModels(ModelRegistryEvent event) {
        registerModel(ItemsRegister.BUBBLE);

    }

    private void registerModel(Item item) {
        ModelLoader.setCustomModelResourceLocation(item, 0, new ModelResourceLocation(item.getRegistryName(), "inventory"));
    }

- \ ``registerModel(ItemsRegister.BUBBLE);``\：调用\ ``registerModel``\方法注册物品材质，BUBBLE可以换成其他的已经注册的物品

- \ ``ModelLoader.setCustomModelResourceLocation(item, 0, new ModelResourceLocation(item.getRegistryName(), "inventory"));``\：注册物品模型。0是Metadata。其中"inventory"一般不需要更改。

**不要把方法名搞混了！**

| 物品模型已经注册完成，你只需要在**ClientProxy**类中的\ ``preInit``\方法中\ ``new ModelsRegister();``\即可。
| 让我们进游戏看一下吧：

|image2.png|

|image3.png|

.. |image1.png| image:: https://i.loli.net/2020/03/13/8xAYFLp9vRQ7mCw.png
.. |image2.png| image:: https://i.loli.net/2020/03/13/6p73BQtGgNmwLnD.png
.. |image3.png| image:: https://i.loli.net/2020/03/13/BvRgIAJLGc1srhe.png