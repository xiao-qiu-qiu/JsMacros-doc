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
| `按键` | 按下对应的按键即可运行宏 |
| `服务` | 在服务内运行对应的宏 |

这两种方式没什么区别, 按键方式更方便, 但是服务方式更灵活。