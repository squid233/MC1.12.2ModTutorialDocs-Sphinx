添加食物
========

我们来添加一个食物。

首先创建一个类，名字叫做\ ``ItemFoodChestnut``\。

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

WIP