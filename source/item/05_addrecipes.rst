合成
====

简单的配方文件
--------------

一个简单的有序合成配方应该如下：

::

    {
    	"type": "minecraft:crafting_shaped",
    	"pattern": [
    		"xxx",
    		"xax",
    		"xxx"
    	],
    	"key": {
    		"x": {
    			"item": "minecraft:water_bucket"
    		},
    		"a": {
    			"type": "forge:ore_dict",
    			"ore": "gemDiamond"
    		}
    	},
    	"result": {
    		"item": "examplemod:bubble",
    		"count": 9
    	}
    }
    
这个配方允许你用8个水桶来合成9个泡泡。

合成类型
++++++++

你可以把它当作定义用哪一种合成布局，例如\ ``minecraft:crafting_shaped``\ (有序合成)或\ ``minecraft:crafting_shapeless``\ (无序合成)。

你也可以定义你自己的合成类型，只需要使用_factories.json文件。

有序合成
********

有序合成需要\ ``pattern``\和\ ``key``\两个关键字。  

\ ``pattern``\ 定义物品的排序，它必须是占位符的形式。每一个物品你都可以选择任意的一个字符作为占位符。  

\ ``key``\ 定义了占位符对应的物品。可以添加附加属性\ ``forge:ore_dict``\ ，它可以定义物品是矿物词典的一部分。例如，无论什么铜矿都可以生成铜锭。要这样的效果的话，要用\ ``ore``\ 标签定义物品，而不是用\ ``item``\ 定义那个物品。  

默认有很多这样的类型，你也可以自己定义。  

\ ``data``\ 是一个可选标签，用于定义方块或物品的\ ``metadata``\ 。

无序合成
********

无序合成不需要\ ``pattern``\ 和\ ``key``\ 关键字。

要定义一个无序合成，你要使用\ ``ingredients``\ 列表。它定义了合成中要用的物品，也可以用\ ``forge:ore_dict``\ 它函数式的声明在上方。默认有很多这样的类型，你也可以自己定义。它甚至可以一个对象定义多个实例，意味着合成时必须要在合成台里放多个这样的物品。

提示
	你的配方里有多少\ ``ingredients``\ 没有限制，原版合成台没有只允许一个合成里放9个物品。


::

    {
        "type": "crafting_shapeless",
        "ingredients": [{
            "item": "examplemod:bubble"
        },
        {
            "item": "examplemod:bubble"
        }
        ],
        "result": {
            "item": "minecraft:diamond",
            
        }
	}
		
这个配方允许你用2个泡泡来合成1颗钻石。

加载配方
--------

只需要将配方文件放到\ ``./assets/<modid>/recipes/`` \目录下即可。  
配方文件必须为标准的JSON格式。`Be JSON`_ 是一个很好的在线检查JSON格式是否正确的网站。

熔炼
----

要定义一个熔炼配方，我们只需要用1行代码即可。  
新建一个SmeltingRecipes类，并在里面写上：

::

    public SmeltingRecipes() {
	    GameRegistry.addSmelting(ItemsRegister.BUBBLE, new ItemStack(ItemsRegister.BUBBLE, 2), 0.9f);
	}
	
这样当你烧完泡泡的时候，就会出现2个泡泡，并获得0.9点经验。

最后我们只需要在CommonProxy的init方法中new SmeltingRecipes();即可。

.. _Be JSON: http://www.bejson.com/