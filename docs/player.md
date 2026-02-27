---
icon: lucide/angry
---

# 玩家
## 获取玩家对象
```javascript
const player = Player.getPlayer()
```
获取到玩家对象后, 后面的操作都需要通过这个对象进行。
## 获取玩家名字
```javascript
const player = Player.getPlayer()
const playerName = player.getName().getString()
```
在JsMacros里面获取到的文本内容都是经过`TextHelper`包装的, 可以使用JsMacros的方式来处理文本内容, 如果需要获取字符串的话需要再进行`getString()`。 
!!! question "输出玩家名字"
    接下来尝试在屏幕输出玩家名字。

    需要方法:
    > `Player.getPlayer()` 方法可以获取到玩家对象。

    > `player.getName().getString()` 方法可以获取到玩家名字。

    > `Chat.log(playerName)`方法可以输出文本到屏幕。
    ???- tip "答案"
        ```javascript
        const player = Player.getPlayer()
        const playerName = player.getName().getString()
        Chat.log(playerName)
        ```
        Chat.log(playerName)方法可以输出文本到屏幕。
## 攻击
### attack()
```javascript
const player = Player.getPlayer()
player.attack()
```
使用`attack()`方法可以对准心处进行攻击, 相当于按下左键。
### attack(entity)
```javascript
const player = Player.getPlayer()
const targetEntity = World.getEntities(4.5, 'zombie')[0]
player.attack(targetEntity)
```
这里通过`World.getEntities('zombie')`获取到一个`EntityHelper`列表, 然后将列表的第一个元素作为目标实体进行攻击。
使用`attack(entity)`方法可以对指定实体进行攻击。
!!! question "杀戮光环"
    制作一个杀戮光环, 让玩家击杀附近的怪物。
    需要方法:
    > `Player.getPlayer()` 方法可以获取到玩家对象。

    > `World.getEntities(4.5, 'zombie')` 方法可以获取到距离玩家4.5格以内的`zombie`实体。

    > `player.attack(entity)` 方法可以对指定实体进行攻击。

    > `Time.sleep(100)` 方法可以让程序暂停一段时间。
    
    ???- tip "答案"
        ``` javascript
        while(true){
            const player = Player.getPlayer()
            const targetEntity = World.getEntities(4.5, 'zombie')[0]
            player.attack(targetEntity)
            Time.sleep(100)
        }
        ```
        这里使用了一个死循环, 每隔100ms就对距离玩家4.5格以内的第一个`zombie`实体进行攻击。(注:"第一个"并不是最近的一个, 如果需要获取最近的，需要排序，后面会教)
        死循环无法退出，需要去jsmacros模组菜单里点左下角"正在运行"然后点×关掉
        后面会教如何使用按键开关脚本
## 交互
### interact()
```javascript
const player = Player.getPlayer()
player.interact()
```
使用`interact()`方法可以与准心处进行交互, 相当于按下右键。
### interactEntity(entity, offHand)
```javascript
const player = Player.getPlayer()
const targetEntity = World.getEntities(4.5, 'villager')[0]
player.interactEntity(targetEntity, false)
```
使用`interactEntity(entity, offHand)`方法可以与指定实体进行交互。
offHand参数是控制交互用的左右手的, 左手为true右手为false
不论左右手都能打开村民界面，但如果直接使用左手交互，会被反作弊检测(如GrimAC-PacketOrderD: Skipped Mainhand) (1.8+)
不过就算用右手交互，也会被反作弊检测(GrimAC-PacketOrderC)因为少发了InteractAt包(左手交互则会同时报PacketOrderC和D) (1.8+)
所以在有反作弊的服请谨慎使用此方法

