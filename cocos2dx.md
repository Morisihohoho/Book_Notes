# Cocos2dx

## 基本概念

### 导演（Director）

1. 负责Scene的替换和转换，Director是一个共享的单例对象，在代码的任何地方调用

### 场景（Scene）

1. Scene Graph 
   1. cocos2dx的一种数据结构，树状图类型。一个场景是一个书，场景里的元素是一个节点。

![img](https://docs.cocos.com/cocos2d-x/manual/en/basic_concepts/basic_concepts-img/tree.jpg)

2. cocos2dx使用中序遍历，先遍历左子树，然后是根，最后是右子树。上图的遍历序列是：D,B,E,A,C,F,H,G

3. z-order

   1. z-order为负的节点会被放置在左子树，非负的节点会被放在右子树

4. 创建子节点方法

   ```c++
   // Adds a child with the z-order of -2, that means
   // it goes to the "left" side of the tree (because it is negative)
   scene->addChild(title_node, -2);
   
   // When you don't specify the z-order, it will use 0
   scene->addChild(label_node);
   
   // Adds a child with the z-order of 1, that means
   // it goes to the "right" side of the tree (because it is positive)
   scene->addChild(sprite_node, 1);
   ```

   渲染时,z-order值大的节点对象后绘制，值小的先绘制。如果两个节点对象绘制范围有重叠，z-order值大的可能会覆盖z-order值小的

### 精灵（Sprite）

1. 就是能够被控制的对象

2. 实例

   ```c++
   // This is how to create a sprite
   auto mySprite = Sprite::create("mysprite.png");
   //Sprite类的create方法，用的一张png图片创建
   
   // this is how to change the properties of the sprite
   mySprite->setPosition(Vec2(500, 0));
   //设置Sprite的位置，Vec2是STL容器，可以存放两个float值
   mySprite->setRotation(40);
   //设置旋度
   mySprite->setScale(2.0); // sets both the scale of the X and Y axis uniformly
   //设置大小
   mySprite->setAnchorPoint(Vec2(0, 0));
   //设置锚点
   ```

3. 锚点(cocos2dx的默认锚点在左下角)

   1. 显示区域的相对位置

![img](https://docs.cocos.com/cocos2d-x/manual/en/basic_concepts/basic_concepts-img/2n_level1_anchorpoint_0_0.png)

![img](https://docs.cocos.com/cocos2d-x/manual/en/basic_concepts/basic_concepts-img/2n_level1_anchorpoint_05_05.png)

![img](https://docs.cocos.com/cocos2d-x/manual/en/basic_concepts/basic_concepts-img/2n_level1_anchorpoint_1_1.png)

### 动作（Action）

1. 执行Sprite的移动（还能创造一个动作序列sequence执行角色的连续运动）

   ```c++
   auto mySprite = Sprite::create("Blue_Front1.png");
   //创建一个精灵
// Move a sprite 50 pixels to the right, and 10 pixels to the top over 2 seconds.
   auto moveBy = MoveBy::create(2, Vec2(50,10));
   mySprite->runAction(moveBy);
   
   // Move a sprite to a specific location over 2 seconds.
   auto moveTo = MoveTo::create(2, Vec2(50,10));
   mySprite->runAction(moveTo);
   ```

### 序列(Sequence)

1. 多个动作按照特定顺序的一个排列

   ```c++
   auto mySprite = Node::create();
   
   // move to point 50,10 over 2 seconds
   auto moveTo1 = MoveTo::create(2, Vec2(50,10));
   
   // move from current position by 100,10 over 2 seconds
   auto moveBy1 = MoveBy::create(2, Vec2(100,10));
   
   // move to point 150,10 over 2 seconds
   auto moveTo2 = MoveTo::create(2, Vec2(150,10));
   
   // create a delay
   auto delay = DelayTime::create(1);
   
   mySprite->runAction(Sequence::create(moveTo1, delay, moveBy1, delay.clone(),
   moveTo2, nullptr));
   //按照创建的序列顺序执行
   ```

2. 多个动作同时被执行

   ```c++
   auto myNode = Node::create();
   
   auto moveTo1 = MoveTo::create(2, Vec2(50,10));
   auto moveBy1 = MoveBy::create(2, Vec2(100,10));
   auto moveTo2 = MoveTo::create(2, Vec2(150,10));
   
   myNode->runAction(Spawn::create(moveTo1, moveBy1, moveTo2, nullptr));
   //Spawn能让多个动作被同时执行
   ```

### 节点关系

改变父节点的属性会影响子节点的属性。（子节点的描点总会是在左下角(0,0)处)

### 日志输出

```c++
log("This would be outputted to the console");
```

