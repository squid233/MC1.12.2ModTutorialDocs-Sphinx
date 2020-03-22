添加食物
========

我们来添加一个食物。

并不是所有的物品都继承于Item类，例如工具继承于ItemTool类，盔甲继承于ItemArmor类，而食物继承于ItemFood类。

ItemFood类的构造函数有这些：

::

    public ItemFood(int amount, float saturation, boolean isWolfFood)
    {
        this.itemUseDuration = 32;
        this.healAmount = amount;
        this.isWolfsFavoriteMeat = isWolfFood;
        this.saturationModifier = saturation;
        this.setCreativeTab(CreativeTabs.FOOD);
    }

    public ItemFood(int amount, boolean isWolfFood)
    {
        this(amount, 0.6F, isWolfFood);
    }

| amount：回复的饥饿值。int整数类型。
| saturation：回复的饱食度。饱食度越高回血速度就越快。float浮点数类型。
| isWolfFood：狼是否可食用。true为可以，false为不能。

其中，从上看出saturation是可选的。默认值为0.6f。

首先创建一个类，名字叫做\ ``ItemFoodChestnut``\。之后，在类里添加如下代码：

::

    public ItemFoodChestnut() {
        super(1, 0.6f, false);
        String name = "chestnut";
        this.setRegistryName(name).setUnlocalizedName(ExampleMod.MODID+"."+name).setCreativeTab(CreativeTabs.FOOD);
    }

只需要注册这个食物以及添加物品贴图，再进行国际化与本地化就可以了。

我们希望这个食物能在饱的时候也能吃，因此，再添加这一段代码：\ ``setAlwaysEdible();``\

我们还希望可以在吃掉后玩家会获得效果，因此，参考原版金苹果的代码，我们需要重写onFoodEaten方法。

::

    @ParametersAreNonnullByDefault
    @Override
    protected void onFoodEaten(ItemStack stack, World worldIn, EntityPlayer player) {
        if (!worldIn.isRemote) {
            player.addPotionEffect(new PotionEffect(Potion potionIn, int durationIn, int amplifierIn));
        }
        super.onFoodEaten(stack, worldIn, player);
    }

| potionIn：药水效果。例如MobEffects.SPEED就是速度。
| durationIn：效果时长。理论上最长是2147483647，但原版用命令时最高为1000000。
| amplifierIn：效果等级。最高为255。

将这些替换成你想要的数据，就可以了。

注意：一定要将食物类继承ItemFood类！

饮料同理。