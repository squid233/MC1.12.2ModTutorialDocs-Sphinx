创造模式物品栏
==============

创建CreativeTab类，在里面写上：

::

    public static final CreativeTabs EXAMPLE_CREATIVE_TAB = new CreativeTabs("example") {
        @SideOnly(Side.CLIENT)
        @Override
        public ItemStack getTabIconItem() {
            return new ItemStack(ItemsRegister.BUBBLE);
        }
    };

其中ItemsRegister.BUBBLE是创造模式物品栏的图标。

完成后把物品改一下：

::

    this.setCreativeTab(CreativeTab.EXAMPLE_CREATIVE_TAB);

再启动游戏就能看到物品了。