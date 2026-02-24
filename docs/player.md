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
在Jsmacros里面获取到的文本内容都是经过`TextHelper`包装的, 可以使用Jsmacros的方式来处理文本内容, 如果需要获取字符串的话需要再进行`getString()`。 
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
const targetEntity = World.getEntities('zombie')[0]
player.attack(targetEntity)
```
这里通过`World.getEntities('zombie')`获取到一个`EntityHelper`数组, 然后将数组的第一个元素作为目标实体进行攻击。
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
        这里使用了一个死循环, 每隔100ms就对距离玩家4.5格以内的第一个`zombie`实体进行攻击。
## setLongAttack(false)
```javascript
const player = Player.getPlayer()
player.setLongAttack(false)
```
使用`setLongAttack(true)`方法可以开启长攻击, 长按左键。
## setLongAttack(true)
```javascript
const player = Player.getPlayer()
player.setLongAttack(true)
```
使用`setLongAttack(false)`方法可以关闭长攻击。
!!! question "挖掘方块"
    制作一个挖掘方块的功能, 让玩家挖掘脸上的方块。
    ```javascript
    const player = Player.getPlayer()

    ```
## 交互
### interact()
```javascript
const player = Player.getPlayer()
player.interact()
```
使用`interact()`方法可以与准心处进行交互, 相当于按下右键。
### interact(entity)
```javascript
const player = Player.getPlayer()
const targetEntity = World.getEntities('villager')[0]
player.interact(targetEntity)
```
使用`interact(entity)`方法可以与指定实体进行交互。
### setLongInteract(false)
```javascript
const player = Player.getPlayer()
player.setLongInteract(false)
```
使用`setLongInteract(true)`方法可以开启长交互, 长按右键。
## setLongInteract(true)
```javascript
const player = Player.getPlayer()
player.setLongInteract(true)
```
使用`setLongInteract(false)`方法可以关闭长交互。