合成
====

随着Minecraft 1.12的更新,Mojang引入了一种基于JSON文件的新型数据驱动的合成系统。在那之后Forge也改成了这个，Minecraft 1.13中拓展成了数据包。

加载配方
--------

Forge会加载在\ ``./assets/<modid>/recipes/``\目录下的所有配方。你可以随意调用这些文件，考虑到原版约定是在输出物品之后命名它们。 此名称也用作注册密钥，但不影响配方的操作。

| 提示:
| 配方文件不能以下划线开头，因为这是为静态文件保留的。 JSON文件扩展名是必需的。

配方文件
--------

一个基本的配方文件应该如下:

::

    {
        "type": "minecraft:crafting_shaped",
        "pattern":
        [
            "xxa",
            "x x",
            "xxx"
        ],
        "key":
        {
            "x":
            {
                "type": "forge:ore_dict",
                "ore": "gemDiamond"
            },
            "a":
            {
                "item": "mymod:myfirstitem",
                "data": 1
            }
        },
        "result":
        {
            "item": "mymod:myitem",
            "count": 9,
            "data": 2
        }
    }

类型 (Type)
++++

合成的类型。你可以把它当作定义用哪一种合成布局，例如 \ ``minecraft:crafting_shaped``\ (有序合成)或 \ ``minecraft:crafting_shapeless``\(无序合成)。

你也可以定义你自己的合成类型，只需要使用_factories.json文件。

组 (Groups)
+++++++++++

你还可以把你的配方增加到一个组里，这样可以在合成帮助接口里一起显示。group字符串相同的配方会放在同一个组里。例如，这可以用于所有的门的合成配方，这样即使有很多种不同的门，在合成帮助里只会有一个条目。

配方的类型
----------

这样的话，我们可以仔细看一下有序合成和无序合成定义上的区别。

有序合成
++++++++

有序合成需要\ ``pattern``\和\ ``key``\两个关键字。\ ``pattern``\定义物品的排序，它必须以占位符的形式。每一个物品你都可以选择任意的一个字符作为占位符。而key定义了占位符对应的物品。可以添加附加属性\ ``forge:ore_dict``\ ，它可以定义物品是矿物词典的一部分。例如，无论什么铜矿都可以生成铜锭。要这样的效果的话，要用\ ``ore``\标签定义物品，而不是用\ ``item``\定义那个物品。默认有很多这样的类型，你也可以自己定义。\ ``data``\是一个可选标签，用于定义方块或物品的metadata。

| 重要
| 用了\ ``setHasSubtypes(true)``\的物品必须要\ ``data``\字段。如果不用，那么意味着有着任何metadata的该物品都可以用于合成。例如，不定义剑的数据意味着用了一半的剑也可以用于合成!

无序合成
++++++++

无序合成不需要\ ``pattern``\和\ ``key``\关键字。

要定义一个无序合成，你要使用\ ``ingredients``\列表。它定义了合成中要用的物品，也可以用\ ``forge:ore_dict``\它函数式的声明在上方。默认有很多这样的类型，你也可以自己定义。它甚至可以一个对象定义多个实例，意味着合成时必须要在合成台里放多个这样的物品。

| 提示
| 你的配方里有多少ingredients没有限制，原版合成台没有只允许一个合成里放9个物品。

下面这个例子展示了ingredients在JSON里是什么样的:

::

    "ingredients": [
        {
            "type": "forge:ore_dict",
            "ore": "gemDiamond"
        },
        {
            "item": "minecraft:nether_star"
        }
    ],
    ...

烧炼
++++

要定义一个熔炉的烧炼，你要用 \ ``GameRegistry.addSmelting(input, output, exp);``\，因为烧炼现在不是基于JSON的。

TODO
====
