# 基础环境配置

!!! note
    本节内容由手动配置重写为通过模板配置, 旧版你可以到[归档-基础环境配置](../arc/BasicEnv.md)中找到(不推荐)

## Celeste

!!! note
    如果你不是 Windows 用户的话这一步你可以直接跳过.

Everest 需求我们使用 FNA 版本的蔚蓝, 而 Linux 和 MacOS 上的蔚蓝已经就是 FNA 版本了, 而在 Windows 上则是 XNA 版本, 所以我们需要一些方法切换到 FNA 版本:

- 在 Steam 上:  库->Celeste, 右键菜单属性->测试版->Opengl
- 在 itch 上: 重新下载一个 `Celeste Windows OpenGL` 版本
- 在 Epic 上: 已经是 FNA 版本了

!!! note
    Everest 会在运行时将你以 FNA 版本制作的 mod 重链接为 XNA, 所有你不是很需要在意这俩的差距  
    注意更换版本后通常会变回原版, 记得重新安装 Everest


## C# 编程能力 与 开发环境

因为我们是 CodeMod, 嗯, 那么写一些代码是必不可少的, 蔚蓝是使用 `C#` 基于 `.NET framework 4.5.2` 来制作的, 那么学习 `C#` 当然是必不可少的.

!!! info
    理论上所有 **.NET 系**语言比如 `VB.NET` `F#` 都可以, 不过为了方便起见我们还是使用 C#.

好吧这句话可能说的太平淡了(wuwu), 毕竟大部分<del>蔚批</del>蔚蓝 mod 爱好者就是被这一步卡住的, 那么这里...只能给你推荐几个学习渠道了,
毕竟在这里没必要让这个教程过于全能.

1. 视频: [Bilibili - 丑萌气质狗 - 【C#零基础入门教程 Visual Studio 2022】人生低谷来学C#](https://www.bilibili.com/video/av895726228) (全p, 稍微不全)
2. 视频: [Bilibili - C#从入门到精通（第5版）](https://www.bilibili.com/video/av882929680) (1-71p, 109-132p)
3. 视频: [Bilibili - 刘铁猛 - C#语言入门详解-第1季-剪辑版-全33课-分154集](https://www.bilibili.com/video/av906241776) (1-152p)
4. 网站: [Runnob - C# 教程](https://www.runoob.com/csharp/csharp-tutorial.html)
5. 网站: [w3schools - C# 教程](https://www.w3schools.com/cs/index.php) (英文)
6. 书籍: C#入门经典-第7版-C# 6.0

!!! info
    如果你没有能力支持正版书籍的话, 你可以到一些 C# 开发者群内寻找它的电子非正版(比如视频 `1.` up 的群内)  
    上面几个我更加推荐的是 `1.` 和 `3.`  
    借用 `4.` 的目录, 确保你对下面这些概念(画 × 的暂时在蔚蓝 CodeMod 中用不到)有足够清晰的了解在开始你的蔚蓝 CodeMod 之旅之前:  
    ![runnob-1](image-11.png)
    ![runnob-2](image-12.png)
    ![runnob-3](image-10.png)

相信在上面的教程中你应该已经被推荐了一些编辑器/IDE, 那么在本教程中我个人会为了方便**仅**在 `Windows` 上使用 `Visual Studio`, 那你遇到了什么奇怪的问题可以到任何能联系到我的地方问我_(:з」∠)_

## 通过模板创建项目

\_(:з」∠)\_  
根据一些反馈我们发现旧的手动配置环境的方式非常的复杂难操作(  
所以呢这里就推荐一种新的配置环境的方式 - **使用模板**  
考虑到 nuget 安装模板也需要一定的命令行基础...  
所以我觉得还是[提供直接的下载链接更好](https://hongshitieli.lanzouk.com/ih5Cr11o3jaj),
如果有需要的话这是模板的[Github源](https://github.com/Saplonily/celeste-mod-template-sdkstyled), 
下载解压后, 使用你的 vs 打开其中的 csproj 文件, 那么按理来说你会看到这几个文件:

!!! note
    你可能还需要安装 `.NET 6 SDK` 来使用该模板, 你可以[点击这里](https://dotnet.microsoft.com/zh-cn/download/dotnet/thank-you/sdk-6.0.411-windows-x64-installer)下载

- CelesteMod.props
- CelesteMod.targets
- Common.props
- MyCelesteModModule.cs
    
以及你的项目, 它的名字是 `MyCelesteMod`, 不同于旧的方法, 在这里你的配置过程很简单:

- 首先打开 `Common.props`, **将里面的 `CelesteRootPath` 内的内容改成你的蔚蓝安装位置**
- 好像就没了...

```xml hl_lines="3"
<Project>
	<PropertyGroup>
		<CelesteRootPath>C:\Program Files (x86)\Steam\steamapps\common\Celeste</CelesteRootPath>
		<CommonCelesteUsings>true</CommonCelesteUsings>
		<CommonCelesteReferences>true</CommonCelesteReferences>
		<ModAssetsFolderName>ModFolder</ModAssetsFolderName>
	</PropertyGroup>
</Project>
```

咳咳这就是新方法的便利(啊?), 现在你可以按下 `Ctrl+B` 或者手动点击 `生成->生成解决方案`,
如果你在你的 vs 输出里面看到了类似这一句:
```
1>Copied files in 'ModFolder' to 'C:\Program Files (x86)\Steam\steamapps\common\Celeste\Mods\MyCelesteMod'
```
并且你在你的蔚蓝 Mod 目录下找到了这个被创建的目录,
那么你的环境就算是配完了, 如果你很感兴趣这之中发生了什么, 要引用哪些程序集, 这个模板背后干了什么, 你可以去看那复杂的旧的配置方法.
!!! note
    这个模板使用 `msbuild` 帮助了你很多事!  
    比如当你编译完项目之后它会复制编译结果到项目目录的 `ModFolder` 目录下,
    然后将整个 `ModFolder` 复制到蔚蓝的 `Mods\{你的mod名}` 文件夹下!
    所以当我们需要更改一些比如说 loenn 的配置文件, `everest.yaml` 的内容, 你的测试地图等时, 
    你只需要简单地重新编译一遍项目, 然后等待模板来帮你做剩下的活!  

## 更改细节
通过模板的话依然有些东西需要自行更改, 比如这个 Mod 的名字.  
更改 Mod 的名字很简单, 你只需要简单地在 vs 里重命名项目的名字
比如我想叫做 `MyAwesomeMod`, 那么你可以通过这样:  
![awesome mod!](image-4.png)  
顺便别忘了把类似 `MyCelesteModModule.cs` 的文件名也改成类似 `MyAwesomeModModule.cs`,
以及改名后清理一下 ModFolder 下面可能有的一些以过去名字命名的 .dll 和 .pdb 文件!  

## Module 类

<!--草啊, 新的环境配置教程还得再写一遍这俩个b东西-->
就像我们的经典的控制台 C# 应用程序一样有个 `Main` 方法, 我们的蔚蓝 Mod 也有一个 类似的东西, 
那就是 Everest 提供给我们的 `EverestModule` 类.  
那么, 现在打开你的 `Module.cs` 那个文件, 你应该会看到结构这样的代码:
```cs
namespace MyCelesteMod;

public class MyAwesomeModModule : EverestModule
{
    public override void Load()
    {
        Logger.Log(LogLevel.Info, "MyCelesteMod", "Hello World!");
        
    }

    public override void Unload()
    {
    }
}
``` 
在开头我们声明了命名空间, 接下来我们声明了一个类, 然后让它继承于 `EverestModule`, 注意这个类是抽象的, 它要求我们实现的两个方法分别为 `Load` 与 `Unload`.  
这两个方法很简单:

- `Load` 方法在你的 mod 被加载时调用.
- `Unload` 方法在你的 mod 被卸载时调用.

通常我们会在 `Load` 方法里加载我们需要的资源, 进行适当的初始化, 在 `Unload` 方法里释放我们的资源.  
在这里为了明显可见, 我们在 `Load` 方法里通过一个蔚蓝中的类 `Logger` 打印出了一句 "Hello World".

??? note "如果你好奇 `Logger.Log` 这个方法你可以展开来了解"
    `Logger` 是一个蔚蓝底层引擎 `Monocle` 的一个工具类, 它帮助你打印输出一些调试信息,
    通常这些信息会被打印进控制台的同时写入游戏的 `log.txt` 文件中, 
    这也就解释了为什么你遇到各种问题时别人总要求你发送你的 `log.txt`.  
    `Logger.Log` 有两个重载, 其中一个的签名是:
    ```cs
    public static void Log(LogLevel logLevel, string tag, string str)
    ```
    它会以 `logLevel` 的日志等级打印一个标签为 `tag` 的消息 `str`,
    另一个重载不要求你传入 `logLevel` 但会默认你的 `logLevel` 为 `LogLevel.Verbose`.
    `LogLevel` 枚举包含 `Verbose, Debug, Info, Warn, Error`.
    通常对于普通日志我们会选择 `Info`, 对于较多的调试信息选择 `Debug`,
    对于冗余的信息选择 `Verbose`, 对于一些错误但不影响游戏进行的信息选择 `Warn`, 对于一些致命性错误我们会选择 `Error`.
    一般地, 游戏只会打印 `Info` 等级及以上的日志, 你可以通过在蔚蓝启动的命令行中加入`--loglevel {等级}`来指定过滤等级.

## everest.yaml

ok, 我们前面几乎巴拉巴拉讲了几乎三千多个字, 但是依然没有让蔚蓝加载到我们的mod, 不过别急, 这是倒数第二步了.  
实际上有关 code mod 的所有代码相关的东西我们都已经做完了, 剩余的其实只是一个普通 mod 要做的 ---- 写 `everest.yaml`.
在这里我们需要在 `ModFolder` 这个文件夹里做这件事, 那么, 在你的这个文件夹下创建 `everest.yaml` 空文件, 你的目录结构可能像是:

- ModFolder
    - everest.yaml
    - MyCelesteMod.dll
    - MyCelesteMod.pdb

好的, 现在我们打开 `everest.yaml`, 然后像一个普通的 mapper 一样填写信息:
```yml
- Name: MyCelesteMod
  Version: 0.1.0
  DLL: MyCelesteMod.dll
  Dependencies:
    - Name: Everest
      Version: 1.3971.0
```
这些参数分别是:

- `Name`: 你的 mod 名字
- `Version`: 你的 mod 的版本
- `DLL`: 如果你是 code mod 的话, 这里填入你的 code (也就是 dll 文件) 的位置, 这里我们是直接把 .dll 文件放到这个 yaml 的旁边了, 所以直接写名字就好

最后是最底下的那个依赖, 这里我们只依赖最基础的 Everest, 版本填上你目前使用的 Everest 版本, 这里我就填写 3971 了.  

## 最后一步!

为了方便我们的调试, 我们需要让蔚蓝打开的同时打开控制台, 这一步很简单:

- 找到蔚蓝根目录下的 `everest-launch.txt`, 没有的话新建一个空的就行了
- 向里面写入 `--console`
- 搞定, 走你!

现在, 重新编译项目, 让 `msbuild` 带着你的 `ModFolder` 的内容飞往蔚蓝 Mods 文件夹下, 启动蔚蓝.  
在同时启动的黑乎乎的窗口上你应该能在这附近看到那句熟悉的 Hello world:
```log hl_lines="7"
(07/08/2023 21:18:59) [Everest] [Info] [core] Module DialogCutscene 1.0.0 registered.
(07/08/2023 21:18:59) [Everest] [Info] [core] Module UpdateChecker 1.0.2 registered.
(07/08/2023 21:18:59) [Everest] [Info] [core] Module InfiniteSaves 1.0.0 registered.
(07/08/2023 21:18:59) [Everest] [Info] [core] Module DebugRebind 1.0.0 registered.
(07/08/2023 21:18:59) [Everest] [Info] [core] Module RebindPeriod 1.0.0 registered.
(07/08/2023 21:19:00) [Everest] [Info] [Everest.LuaBoot] Lua ready.
(07/08/2023 21:19:00) [Everest] [Info] [MyCelesteMod] Hello World!
(07/08/2023 21:19:00) [Everest] [Info] [core] Module MyAwesomeMod 0.1.0 registered.
(07/08/2023 21:19:00) [Everest] [Info] [loader] Loading mods with unsatisfied optional dependencies (if any)
FNA3D Driver: D3D11
D3D11 Adapter: Intel(R) UHD Graphics 630
```

## 还没完

在经过如上的配置后, 你会发现在蔚蓝启动的时候, 进行编译并复制资源时会报错, 
这是因为 everest 锁定占用了它们, 导致你不得不让这一切在蔚蓝关闭时进行,
同时由于蔚蓝的重启速度不是很理想, 这大大的拉低了 mod 开发效率.  
 不过好在 everest 提供了一个技术叫做 `hot reload`,
即热重载, 它允许你在游戏运行期间替换你的代码并重载资源, 它目前还在 wip 状态.  
要开启这项功能, 首先到你的蔚蓝根目录下的 Saves 目录, 找到并打开 `modsettings-Everest.celeste` 这个文件,
翻到大概中间的位置, 找到属性 `CodeReload_WIP`, 将其更改为 `true`, 此时重新编译你的项目,
你应该就不会再得到任何错误, 并且 everest 也正确地热重载了你的 mod 和你的 mod 资源.