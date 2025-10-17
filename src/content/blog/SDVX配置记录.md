---
title: 'SDVX配置记录'
description: '沙东卫星从配置到腱鞘炎'
pubDate: 'Mar 25 2025'
heroImage: 'https://gh-proxy.com/https://github.com/RaycornM/person-picture-bed/blob/main/img/subbg_0005.png'
---


### 本文只记录配置沙东卫星的过程，仅作学习探讨，不提供不传播任何资源

## 准备文件

下载并解压完压缩包后，得到这几个文件夹：

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-50.png)

下载的包不同可能文件有些区别，可能个别有些解压完后存在“**modules**”文件夹，这是Spice自动检测的配置文件夹，使文件目录保持简洁。如果解压完的游戏没有这个文件夹，则会在根目录中存在许多不同的dll文件，例如_**soundvoltex.dll**_。

如果没有**modules**文件夹又想根目录整洁一点，可以自己创建一个**modules**文件夹，将所有“.dll”文件转移进去

---

## 更新数据

*如果不需要更新可以直接跳到下一步*

社区上传的更新包一般命名为 ：KFC-DATECODE-to-DATECODE

例如：KFC-2024111900-to-2024121000
2024111900为当前数据的版本
2024121000为更新版本

1.解压更新数据内容并以与文件结构匹配的方式将文件复制到现有数据中，同意替换目标中的文件。

2.前往“**prop**”文件夹然后打开**ea3-config.xml**文件，使用文本编辑器打开，找到以下内容：

```
    <soft>
        <model __type="str">KFC</model>
        <dest __type="str">J</dest>
        <spec __type="str">G</spec>
        <rev __type="str">A</rev>
        <ext __type="str">2024052100</ext>
    </soft>
```

修改_ **&lt;ext **​ **_**​ **_**​**type="str"&gt;2024052100**​ **&lt;/ext&gt;** _中的数字为当前版本号日期，格式为：年+月+日+00

---

## 安装Spice

如果已经安装好了Spice，可以跳过当前进行下一步

前往 [spice2x.github.io](https://spice2x.github.io/) 并下载最新版本。

将解压的**exe文件**复制到游戏的根目录中：**spice.exe**、**spice64.exe**、**spicecfg.exe**；

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-51.png)

## 如果使用的是AMD显卡，则需要另外复制三个** *.dll***文件放到游戏目录，N卡用户不需要

解压出来的.dll文件：*stubs*​ *\*​*64*​ *\*

复制到根目录或者是“**modules**”文件夹，如图：

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-52.png)

---

## 配置 Spice

在游戏文件目录打开**spicecfg.exe**

#### 绑定键位（Buttons）

连接手台绑定对应的按键

（device missing是我做记录的时候没有连手台）

service是投币按钮

P1 键盘：keypad 0 到 9，Keypad Insert Card（刷卡）

如果使用手台那么start后面VOL-L LEFT 到 VOL- R RIGHT不用绑定

使用手台绑定旋钮需要切换到Analogs选项卡（手台按钮分配图后接着）

**仅当**使用键盘时：

- **旋钮：**  VOL-L LEFT ，VOL-L RIGHT，VOL-R LEFT ，VOL- R RIGHT

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-53.png)

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-54.png)

绑定旋钮（Analogs）

点击Bind，在Device选项栏选择手台（可能会有多个相同名称选择，任选其一即可），Control左X、右Y，Sensitivity根据你打歌时旋钮的灵敏度自行调整，如果绑定成功，在手台扭对应的旋钮下方的黄色指针会跟随一起旋转

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-56.png)

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-57.png)

#### Overlay（翻译直接就是覆盖？）

修改此部分中的按钮不是必需的，但可以自由更改所需的按钮。

#### 灯光（Lights）

部分手台可能支持让游戏通过 spice2x 控制其灯光，如果是这样，可以通过以下方式将不同的作链接到手台的灯光：

- 点击Bind
- 在Device中，选择手台
- 在Light Control中，选择相应的光源
- 点击Close
- 对其他灯光控制重复上述步骤

#### 卡号（Cards）

卡号跟随服务器网络一起设置

#### 补丁（Patches）

自行选择是否修改配置

自 2024-09-10 更新以来，补丁内置了描述。

要查看它，请将鼠标悬停在每个补丁名称左侧的 (?) 或 (!) 上。

### **为防止出现问题，请避免修改不需要或不了解的内容**

如果想要修改，可以参考：

点击 Import from URL，输入 https://sp2x.two-torial.xyz/ 并确定

勾选 Auto apply patches on game start，然后下面根据自己的需求来勾选即可

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-58.png)

#### 接口（API）

一般人直接跳过就可以了

#### 设置（Options）

## 如果不知道选项的作用，可以将鼠标悬停在最左侧的问号上。

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-59.png)

##### 必要设置

勾选**SDVX Disable Cameras**

|SDVX Disable Cameras|\-sdvxdisablecams|ON|
| --------------------| ----------------| --|

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-61.png)

##### 可选设置

下拉找到图形选项，勾选NVIDIA 配置优化

|NVIDIA profile optimization|\-nvprofile|ON|
| ---------------------------| ----------| --|

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/20251014141029957.png)

##### 网络

设置网络有两种方案，分在线服务器和本地服务器

###### 在线服务器

以米网为例，在options选项卡里下拉找到network设置

在EA Service URL 一栏里填写 **http://rice.sdvx.moe:5730/**

在 PCBID 栏填上你得到的 PCBID，如果不想联机对战其实PCBID也可以空在那里，相同的 PCBID 视作一个店铺，可以查看店铺排名

（本人目前了解到除米网外还有A网和理网，不过另外两个服务器都采用的邀请制，需要有一定能力找到大佬邀请才能加入）

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-62.png)

如果还没有卡号，那么做完这些就可以回到Cards选项卡去生成自己的卡号了，点击Generate会给你自动生成一个卡号，保险起见你可以把自己的卡号备份一份，如果游戏目录内的卡号丢失，可以通过Card Path定向备份的卡号

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-63.png)

你生成的卡号以后也可以用来注册WebUI账号和找回数据。使用 WebUI 控制台，注册账号可以进行查看成绩和个性化等功能。

###### 本地服务器（Asphyxia core）

访问 asphyxia 的官网，下载asphyxia 服务端

主页：[https://asphyxia-core.github.io/](https://asphyxia-core.github.io/)
本体：[https://github.com/asphyxia-core/asphyxia-core.github.io/releases](https://github.com/asphyxia-core/asphyxia-core.github.io/releases)
插件：[https://github.com/asphyxia-core/plugins/releases](https://github.com/asphyxia-core/plugins/releases)

下载完的服务器本体文件解压到跟SDVX同一个文件夹内（只是方便寻找，你随便放哪都可以，只要不是C盘）或者直接解压到 SDVX的目录内，asphyxia 的文件与游戏本体不存在文件冲突，可以直接放在同一个文件夹；

插件（*sdvx@asphyxia*）下载完成后把解压出来的文件夹直接放入本体根目录下的 *plugins* 文件夹下

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-64.png)

###### 启动服务器（Asphyxia core）

做完以上步骤之后，双击_**asphyxia-core-win-x64.exe**_启动服务器，它将自动打开一个网页，这是服务器的WebUI；如果没有网页打开可以复制控制台窗口内的链接到浏览器打开：[http://localhost:8083](http://localhost:8083)（端口号一般是 8083，想修改成其他端口号也没问题，进入网页之后在_CORE Settings_的Port部分修改）

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-65.png)

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-66.png)

打开后网页应该如下图所示

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-67.png)

在左侧边栏的 Plugins 分类找到 SDVX，在overview部分确保**Plugin Settings**的这些内容是启用的，修改完记得点击右下角的Apply：

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-68.png)

还有一步使用懒人包的应该不需要，在Import Assets部分导入游戏目录的绝对路径，完成后，单击Submit 。如果弹出窗口，指出：/游戏绝对路径 Submit Imported Successfully！ 说明导入成功

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-69.png)

到这一步基本就可以启动游戏了，我们回到spicecfg.exe，在网络那里填入本地服务器地址：[http://localhost:8083](http://localhost:8083)（修改了端口号的把8083改成自己修改的端口）

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-70.png)

做完以上步骤没有错误的话就可以启动游戏了！在创建完账户之后还可以回到WebUI页面对你的账户做一些设置：

在SDVX的profiles部分，点击你账号右下角的detail绿色按钮

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-71.png)

在detail部分可以查看基础信息和打歌分数，在setting部分可以自定义设置：

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-72.png)

提交保存后再次回到游戏文件夹。如果在导入时插入了正确的路径并且一切正常且没有任何错误，将会生成一个名为webui的文件夹。复制此文件夹并将其粘贴到plugins\\sdvx@asphyxia中。如果出现提示，则覆盖文件。然后重启asphyxia-core-x64.exe

检查是否安装ffmpeg，打开控制台输入ffmpeg，如果弹出下图内容，说明已经安装：

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-77.png)

现在本地服务器的创建已经完成了使其正常工作所需的所有步骤，你可以打开spice64.exe运行游戏

###### 如果没有ffmpeg

使用浏览器访问：https://www.gyan.dev/ffmpeg/builds/  
打开后，在下面有两个.7z 文件，选择其一下载，如果没有特别的需求，一般下载第一个就可以  
​![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-73.png)  
下载后，将压缩包解压到一个自己顺手的地方，按 Win + R，输入 SystemPropertiesAdvanced，打开高级系统设置  
​![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-74.png)  
点击环境变量，选择上面的 Path，然后点击编辑  
​![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-76.png)​  
在弹出来的窗口，点击新建或者双击空白的栏目，输入自己的 ffmpeg 路径 +\\bin，然后选择确定，这个时候 ffmpeg 就安装好了  
如果在安装前 asphyxia 开着，需要重新启动

## 首次启动前

##### VCRedist & DirectX

确保电脑已经安装了DirectX和最新的VCRedist

[https://github.com/abbodi1406/vcredist/releases/latest](https://github.com/abbodi1406/vcredist/releases/latest) (VisualCppRedist\_AIO\_x86\_x64.exe)

[https://www.microsoft.com/en-us/download/details.aspx?id=8109](https://www.microsoft.com/en-us/download/details.aspx?id=8109)

或者直接装一遍3dm的游戏运行库：[游戏常用运行库 合集 | Game Runtime Libraries Package（6.2.25.0409） - 模拟器综合讨论区 - 3DMGAME论坛 - Powered by Discuz!](https://bbs.3dmgame.com/thread-6584973-1-1.html)

##### 音频

在开始游戏之前，先调整音频设置以尽量减少启动时的崩溃。

如果还没关闭spicecfg.exe的话，可以通过spicecfg进入音频设置：

在spicecfg界面最上方菜单栏找到**Shortcuts**，点击出现三个选项选择**Audio Playback Devices**

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-78.png)

在弹出的窗口，找到默认播放设备，右键选择属性

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-79.png)

点击 “**高级**” 选项卡并将默认格式设置为 **44100 Hz**，同时确保下方独占模式两个选项勾选，最后点击右下方的应用就完成设置了

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-80.png)

直接在电脑设置找到音频设置

右键选择电脑任务栏右侧的声音图标

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-81.png)

打开声音设置，往下拉在高级那一栏找到更多声音设置

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-82.png)

在弹出的窗口，找到你的默认播放设备，右键选择属性

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-79.png)

点击 “高级” 选项卡并将默认格式设置为 44100 Hz，同时确保下方独占模式两个选项勾选，最后点击右下方的应用就完成设置了

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-80.png)

##### 屏幕设置

如果屏幕能竖起来，可以直接打开spice.exe启动游戏，或者是现在桌面右键选择显示设置，把显示方向调成纵向

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-83.png)

如果电脑屏幕不能竖起来，像使用笔记本等，打开**spicecfg.exe**，选择**Options**选项卡，下拉找到**Graphics(Windowed)** ，勾选**Windowed Mode**

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-84.png)

window border style根据需要自行修改，我这里选了无边框模式；window size设置，如果启动游戏后有大面积遮挡，那么就根据使用的屏幕大小进行修改

## 初次设定

打开游戏，弹出几个窗口之后会弹出游戏本体的窗口，如果正常启动的话会开始自检

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-85.png)

自检通过后，如果是第一次启动游戏，那么会出现这样的界面：

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-86.png)

按下在spicecfg里面绑定的**Test**键开始进行校准，游戏会提示在菜单中导航到哪里

- 按下**BT-A**即可向上
- 按下**BT-B**即可向下
- 按下**Start**以选择

选择**I/O CHECK**并按下Start

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-87.png)

选择**CALIBRATION SETTINGS**并按下**Start**

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-88.png)

接着选择**CALIBRATION**并按下**Start**

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-89.png)

根据提示****慢慢地****逆时针旋转左旋钮**（**VOL-L Left**），如果使用键盘，只需按住绑定的 **VOL-L Left** 按钮即可，直到第一行显示COUNT = OK**，完成此操作后按下 **Start** 按钮

随后****慢慢地**顺时针扭动左旋钮** 直到显示 **COUNT = OK**，按下 **Start** 按钮

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-90.png)

使用右侧旋钮重复相同的步骤。完成后，选择 **SAVE AND EXIT**并按**Start**按钮

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-91.png)

返回到上一层菜单，选择**GAME MODE**并按下**Start**

大功告成！游戏现在应该可以正常加载了🤓☝️

## 进入游戏

如果首次进入游戏，我们需要注册一个账号，先按在spicecfg中绑定的投币按钮（**Service**)，我这里绑定的是鼠标侧键之一

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-93.png)

模拟投币完再来模拟刷卡，按绑定的刷卡按钮（**Keypad Insert Card**），我这里是另一个鼠标侧键；因为是首次进游戏，刷卡后会弹出一个界面，选择**新规登录**（选择和确认使用**左右旋钮**和**Start**按钮）：

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-94.png)

同意协议后会让你设置一个密码，之后每一次刷卡都要用到这个密码，务必记住

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-95.png)

接着设置名字，使用滚轮来选择字母，按**Start**确定字母，选好了就选择 END 然后按下**Start**

![](https://cdn.jsdelivr.net/gh/RaycornM/person-picture-bed@main/img/image-96.png)

之后就能正式开始游戏了！啪唧啪唧啪唧

## 附录一些收集来的指令

显示器可以竖屏的启动脚本（本地服务器）

```
@echo off
:: Start Local Server
start "" "asphyxia-core-x64.exe"

:: Start SDVX VI
start "" "spice64.exe" -sdvxdisablecams -url http://127.0.0.1:8083
```

想横屏游玩的启动脚本（本地服务器）

```
@echo off
:: Start Local Server
start "" "asphyxia-core-x64.exe"

:: Start SDVX VI
start "" "spice64.exe" -sdvxdisablecams -url http://127.0.0.1:8083 -w -windowborder 0 -windowsize 720,1080
```

解除端口占用

```
netstat -ano | findstr PORT
taskkill   /pid PID /f
```

WebUI米网控制台

```
http://152.136.108.195:23333/login?next=%2F
```

A网

```
http://arcana.nu
```
