---
icon: lucide/rocket
---

# 快速开始
## 获取Jsmacros
!!! warning "注意"
    \>= 1.21.1需要从github构建, 或者修改fabric.mod.json(版本没有重大更新的情况),
    或者从GitHub fork下来使用action构建
> 获取[Jsmacros](https://modrinth.com/mod/jsmacros), 并安装到你的Minecraft客户端中。
## 目录结构
```
.minecraft/
├── config/
  └── jsMacros/
    └── LanguageExtensions # 语言扩展, 如果需要使用其他语言, 请将其放入此目录
    └── Macros/ # 存放宏文件
    └── options.json # Jsmacros配置
    └── options.json.v2.bak # Jsmacros配置备份
```
## 创建开发环境
!!! note "提示"
    非必须, 但是建议使用, 方便开发和调试, 提供了类型提示和代码补全等功能。
### 安装VSCode
下载并安装[VSCode](https://code.visualstudio.com/), 推荐以下插件:

- Prettier(代码格式化)
- TabOut(代码缩进)
- indent-rainbow(代码缩进高亮)

### 使用ts进行类型检查和代码提示
``` cmd title="cmd"
cd Macros
git clone https://github.com/TheStoneFish/JsMacros-template.git .
npm install
code .
```
克隆后使用VSCode打开, 然后安装依赖, 即可看到类型提示和代码补全等功能。
![](https://img.mynotes.world//202602262111399.png)
## 创建第一个宏
=== "js"
    ``` js title="test.js"
    Chat.log("Hello, world!")
    ```
    把文件放入.minecraft/config/jsMacros/Macros/src目录下。
=== "ts"
    ``` ts title="test.ts"
    Chat.log("Hello, world!")
    ```
    把文件放入.minecraft/config/jsMacros/Macros/src目录下。
    
    使用ts需要进行编译, 请提前安装依赖。
    ``` cmd title="cmd"
    npm install
    npm run build
    ```
    编译后文件会生成到.minecraft/config/jsMacros/Macros/dist目录下。
## 运行宏
运行宏有两种方式:

| 方法 | 描述  |
| ----------- | ------------------------------------ |
| 按键 | 按下对应的按键即可运行, 可以同时运行多个 |
| 服务 | 在服务内运行对应的宏, 不可用同时运行多个, 可以设置启动客户端自动启动脚本 |

这两种方式没什么区别, 按键方式更方便, 但是服务方式更灵活。
!!! warning "注意"
    运行的脚本不会随着退出服务器而停止, 只有退出游戏才会停止。
### 按键触发
![](https://img.mynotes.world//202602251554510.png)
使用对应的按键触发宏, 运行后需要在左下角正在运行关闭宏来结束运行, 可以同时运行多个宏。

图中的fork和joined状态是Jsmacros的运行状态, 具体含义如下:

| 方法 | 描述  |
| ----------- | ------------------------------------ |
| ![](https://cdn.discordapp.com/emojis/1136842194586697878.webp?size=80) | 这个状态是`fork`状态, 在这个状态上运行的宏不会阻塞运行线程的运行 |
| ![](https://cdn.discordapp.com/emojis/1136842096775532634.webp?size=80) | 这个状态是`joined`状态, 在这个状态上运行的宏会阻塞运行线程的运行 |

默认情况下, 按键触发的宏都是`fork`状态, 如果为`joined`状态脚本就不能运行超过500ms, 不然会触发看门狗, 因为按键触发是在主线程进行的, 所以正常就使用`fork`状态就行。
!!! tip "看门狗"
    当宏运行在主线程时间超过500ms, 则会触发看门狗, 强制结束宏的运行, 防止宏把游戏卡死。
另外在事件监听的时候也可以设置Joined, 是否阻塞运行线程的运行, 在Tick事件等事件中阻塞无任何意义, 如果在

- SendMessage
- RecvMessage
- JoinedTick
- SignEdit
- ClickSlot
- DropSlot

触发, 则会阻塞主线程的运行, 这样可以修改事件的行为(比如修改RecvMessage收到的消息, 修改SendMessage发送的消息)。 `context.releaseLock()`可以解除阻塞, 如果阻塞超过500ms会触发看门狗。
```
JsMacros.on('SendMessage', true, JavaWrapper.methodToJava((e) => {
    Chat.log(`发送消息: ${e.message}`)
    e.cancel()
    Time.sleep(1000)
}))
```
上面触发了看门狗因为joined把主线程阻塞了, 所以应该完成cancel后先解除线程锁。
```
JsMacros.on('SendMessage', true, JavaWrapper.methodToJava((e, context) => {
    Chat.log(`发送消息: ${e.message}`)
    e.cancel()
    context.releaseLock()
    Time.sleep(1000)
}))
```
按键触发的宏可以设置触发条件, 有三种触发条件:

| 方法 | 描述  |
| ----------- | ------------------------------------ |
| ![](https://cdn.discordapp.com/emojis/937122706346889256.webp?size=80) | 松开按键触发 |
| ![](https://cdn.discordapp.com/emojis/937122592588959795.webp?size=80) | 按下按键触发 |
| ![](https://cdn.discordapp.com/emojis/937122792179122176.webp?size=80) | 松开和按下都会触发 |

### 服务触发
![](https://img.mynotes.world//202602262137967.png)
服务触发的宏可以设置启动客户端自动启动脚本, 运行后关闭需要在服务内关闭运行状态, 不能同时运行多个。