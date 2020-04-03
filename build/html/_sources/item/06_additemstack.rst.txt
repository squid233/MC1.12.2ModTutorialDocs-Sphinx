ItemStack
=========

Minecraft 1.12.2 原版只有4096个物品ID（某些Mod会将其提升至int上限），当我们想写大一些的Mod的话，可不能随便乱用Item声明那个物品。因此，我们要用ItemStack来声明那些物品。

ItemStack可以让多个物品使用同一个ID，例如一些mod的矿石，虽然是多个物品，但是只用了1个ID：ore。

ItemStack使用metadata来区分物品。

声明一个ItemStack
-----------------

我们来试着添加一个ItemStack。该ItemStack含有low_coal, medium_coal, high_coal, super_coal。

::

    Item coals = new Item();
    ItemStack low_coal = new ItemStack(coals);
    ItemStack medium_coal = new ItemStack(coals, 1, 1);
    ItemStack high_coal = new ItemStack(coals, 1, 2);
    ItemStack super_coal = new ItemStack(coals, 1, 3);

| coals: 表示该物品属于coals。
| 数量1: 通常情况下为1。
| metadata1: 表示该物品的metadata值为1。

实战
----

首先，新建一个类，名叫ItemCoals。并让其继承Item类。然后添加上面说的代码。

接着，声明一个构造函数，里面写上

::

   coals.setHasSubtypes(true);
   coals.setRegistryName("coals");
   low_coal.getItem().setUnlocalizedName(ExampleMod.MODID+"."+"low_coal").setCreativeTab(CreativeTabs.MISC);
   medium_coal.getItem().setUnlocalizedName(ExampleMod.MODID+"."+"medium_coal").setCreativeTab(CreativeTabs.MISC);
   high_coal.getItem().setUnlocalizedName(ExampleMod.MODID+"."+"high_coal").setCreativeTab(CreativeTabs.MISC);
   super_coal.getItem().setUnlocalizedName(ExampleMod.MODID+"."+"super_coal").setCreativeTab(CreativeTabs.MISC);

使用getItem();可以把ItemStack转为Item。

再注册物品和物品贴图就好了。

这样，当我们输入/give @p examplemod:coals 1 1时就会获得medium_coal。

此页待完善。
------------
