# MCtools

《我的世界》整合包诊断与联机排查工具集，外加一份跨境联机教程。

全部免费、免安装，解压双击就能用。只支持 **Windows 10 / 11**，用系统自带的 PowerShell 运行，
**不需要管理员权限**，不需要额外装任何东西。

**[⬇ 前往 Releases 页面下载全部工具](https://github.com/beihongliangchu/mctools/releases/latest)**

> ⚠️ **这些工具完全免费、在 GitHub 上开源。严禁二次打包售卖。**
> 若你付费获得该工具，请立即退款并投诉卖家。

## 下载

| 工具 | 版本 | 下载 | 什么时候用 |
| --- | --- | --- | --- |
| 崩溃日志分析 | v1.0 | **[crash-doctor-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/crash-doctor-v1.0.zip)** | 崩了，日志看不懂，不知道是哪个模组的问题 |
| Java 环境诊断 | v1.0 | **[java-doctor-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/java-doctor-v1.0.zip)** | 不知道装了几个 Java、该用哪个、内存该给多少 |
| 模组依赖检查 | v1.0 | **[mod-check-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/mod-check-v1.0.zip)** | 报缺前置、模组冲突、装重复了 |
| 联机方案决策 | v1.0 | **[net-plan-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/net-plan-v1.0.zip)** | 不知道怎么联机，四种方案选哪个 |
| 交付报告生成 | v1.0 | **[report-builder-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/report-builder-v1.0.zip)** | 想把前三个的结果汇总成一份报告 |
| 诊断套件合集 | v1.0 | **[mctools-bundle-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/mctools-bundle-v1.0.zip)** | 五个诊断工具打包，解压到同一个文件夹 |
| 整合包体检 | v3.1 | **[modpack-doctor-v3.1.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/modpack-doctor-v3.1.zip)** | 整合包打不开、闪退、报缺前置、Java 版本不对 |
| 联机网络体检（国内版） | v1.1 | **[mc-net-check-v1.1.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/mc-net-check-v1.1.zip)** | 国内玩家之间联机，卡顿、走路回弹 |
| 跨境网络体检（国际版） | v1.0 | **[mc-net-check-intl-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/mc-net-check-intl-v1.0.zip)** | 国内玩家和国外玩家跨境联机 |
| 跨境联机教程 | v1.0 | **[mc-crossplay-guide-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10.2/mc-crossplay-guide-v1.0.zip)** | 从零教两个人怎么连上，含一页 A4 速查卡 |

> 下载下来的文件名是英文的（`crash-doctor-v1.0.zip` 这样），因为 GitHub 不接受
> 发布包名字里的中文。**解压之后的文件夹和文件仍然是中文名**，不影响使用。

## 整合包诊断套件

前五个工具是一套。各自都能单独用，但配合起来才能从头查到尾。

### 1. 崩溃日志分析 crash-doctor

把 `crash-reports` 和 `logs` 里的英文报错翻成中文结论。

内置 20 多条规则，覆盖 Java 版本、内存、显卡驱动、缺前置、模组冲突、Mixin 报错、
存档损坏、正版验证等常见崩溃。每条结论分 **确定 / 可能 / 提示** 三档，
附上原文依据和具体操作步骤，还会按你日志里的实际数值补一句
（比如「你现在设的是 -Xmx4096m，先往上加 2048 试试」）。

能自动读出游戏版本，和该用的 Java 版本对照，对不上直接标红。

适合：整合包崩了、报错看不懂、不知道该动哪里的。先把日志丢给它，不用再人眼读一遍。

📖 [完整使用说明](docs/crash-doctor.md)

### 2. Java 环境诊断 java-doctor

扫出这台机器上所有 Java，逐个探测版本、位数、厂商，然后告诉你游戏该用哪一个。

附带 **游戏版本 ↔ Java 版本对照表**：

| 游戏版本 | 需要的 Java |
| --- | --- |
| 1.7.10 ~ 1.16.5 | Java 8 |
| 1.17.x | Java 16 或 17 |
| 1.18 ~ 1.20.4 | Java 17 |
| 1.20.5 ~ 1.21.x | Java 21 |

再按你的物理内存和模组数量算出建议内存，外加一套可以直接复制进启动器的 JVM 参数。

适合：「装了 Java 还是崩」——十有八九是装了但没在启动器里指对路径。

📖 [完整使用说明](docs/java-doctor.md)

### 3. 模组依赖检查 mod-check

拆开 `mods` 里每个 jar 读元数据，查五件事：

- **缺前置** —— 列出缺哪个、被几个模组需要
- **重复模组** —— 同一个模组装了两个版本
- **jar 损坏** —— 下载没下完的
- **版本错配** —— 模组要求的游戏版本和你的实例对不上
- **加载器混装** —— Fabric 和 Forge 混在一个文件夹里

支持 Fabric / Quilt / Forge / NeoForge，包括 NeoForge 1.20.5+ 的
`neoforge.mods.toml`、Forge 1.12 及更早的 `mcmod.info`，
以及 jar-in-jar 嵌套（fabric-api 的几十个子模块全在里面）。

适合：报「Missing dependencies」、装了模组起不来、整合包越加越崩。

📖 [完整使用说明](docs/mod-check.md)

### 4. 联机方案决策 net-plan

问四个问题——在不在同一个网、玩哪个版本、肯不肯花钱、有没有国外玩家——
然后直接给出方案、分步骤做法、这个方案的坑、以及备选方案。

四种方案：局域网直连、租云服务器开服、Xbox 好友联机、内网穿透/联机模组。

适合：新手问「我们怎么一起玩」的时候。

📖 [完整使用说明](docs/net-plan.md)

### 5. 交付报告生成 report-builder

把前三个工具的 `.json` 结果汇总成一份排版好的 **HTML 诊断报告**。

报告里有抬头、分区结论、环境信息表、处理建议，**单个文件、不依赖任何外部资源**，
断网也能打开。可以直接发给别人，也可以浏览器里 Ctrl+P 存成 PDF。

适合：想把诊断结果正式交付出去，而不是口头说几句。

📖 [完整使用说明](docs/report-builder.md)

> 💡 **诊断套件跑完之后会自动生成两样能直接发出去的东西**：
> `发给客服.txt`（同时自动复制进剪贴板，聊天框里 Ctrl+V 就行）和
> `发给客服.png`（一张结果卡片图，拖进聊天窗口发送）。
> 因为不少聊天工具不能发文件，只能发文字和图片。

## 网络与联机工具

### 6. 整合包体检 modpack-doctor

检查一个 Minecraft 整合包能不能正常启动。它会核对 Java 版本、扫描模组列表、
找出缺失的前置模组、检查内存配置和常见冲突，最后给一份体检报告。

适合：整合包下载下来打开就崩、进游戏报一堆红字、不知道哪个模组冲突的时候。

📖 [完整使用说明](docs/modpack-doctor.md)

### 7. 联机网络体检 mc-net-check（国内版）

诊断联机卡顿、走路被拉回去、挖方块弹回来到底是链路问题还是服务端问题。
分三段测量：本机到路由器、本机到联机节点（FRP 等）、本机到主机，
各自给出丢包率、延迟、抖动，外加路由走向和 IPv6 可用性。

适合：用 frp、樱花 frp、OpenFrp、EasyTier、ZeroTier、蒲公英之类工具联机的国内玩家。

📖 [完整使用说明](docs/mc-net-check.md)

### 8. 跨境网络体检 mc-net-check-intl（国际版）

同一个工具的国际化版本，专门给不在中国大陆的玩家用。**中英对照输出，英文在前。**

相比国内版做了这些改动：

- 判定阈值按实测延迟自动分档（本地 / 区域 / 跨洋），不再一律套用国内标准
- 新增 **TCP 端口连通测试** —— 大量服务器和云厂商默认屏蔽 ICMP，ping 显示完全不通但游戏其实能连
- 新增 **路径 MTU 探测** —— 隧道和加速器最常见的坑，小包正常大包丢
- 新增 **出口公网 IP 与 CGNAT 判断** —— 直接回答「我能不能自己开服」
- IPv6 测试改用多目标探测，不再写死某一个 DNS

> 这是**两份独立代码**，不是同一个脚本的两个开关。国内版继续按国内网络调优，两边不会自动同步。

📖 [完整使用说明](docs/mc-net-check-intl.md)

### 9. 跨境联机教程

零基础教程：国外朋友下不了 PCL 怎么办、装哪个启动器、怎么把版本和模组对齐、
四种开服方案（免费两个 + 付费两个）分别怎么做、进不去怎么排查。

附带一张**一页 A4 速查卡**，打印出来贴着看，或者直接发微信。

📖 [完整教程](docs/crossplay-guide.md) · [速查卡 PDF](docs/crossplay-card.pdf) · [速查卡 PNG](docs/crossplay-card.png)

## 快速上手

1. 从上面的表格或者 [Releases](https://github.com/beihongliangchu/mctools/releases/latest) 下载对应的 zip
2. 解压到一个普通文件夹，桌面就行
3. 双击里面的 `.bat`

> ⚠️ **一定要先解压再双击。** 直接在压缩包里双击运行会失败，因为脚本会往自己所在目录写报告。
> 解压后必须保证 `.bat` 和 `.ps1` 在同一个文件夹里。

诊断套件想一次跑完的话，下 `mctools-bundle-v1.0.zip`，解压出来五个工具全在同一个文件夹，
依次双击 `crash-doctor.bat` → `java-doctor.bat` → `mod-check.bat` → `report-builder.bat` 就行。

## 运行条件

|  |  |
| --- | --- |
| 系统 | Windows 10 / 11 |
| 软件 | 不需要额外安装，PowerShell 是系统自带的 |
| 权限 | 普通用户即可，不需要管理员权限 |
| 网络 | 两个网络体检工具需要联网，它们本来就是测网络的；诊断套件全程不需要联网 |
| 启动方式 | 双击 `.bat`，不要直接双击 `.ps1`（会被执行策略拦住） |

## 安全说明

- 两个网络体检工具只做网络测量和读取本机网卡信息，**不修改系统任何设置**
- **诊断套件全程只读**：读崩溃日志、读 mods 里的 jar、读 Java 版本，
  **不修改、不移动、不删除你的任何游戏文件**
- **所有工具都不上传任何本地数据**。报告只存在你本地的文件里
- 唯一的例外：国际版为了判断 CGNAT，会向公共查询服务（ipify / icanhazip）问一次你的出口 IP。
  不想让它发，用 `-SkipPublicIp` 参数运行即可
- 诊断套件生成的卡片图里**只写整合包的名字，不写完整路径**，避免把用户名之类的信息带出去
- 所有文件都是纯文本（`.ps1` / `.bat` / `.txt`），可以用记事本打开自行检查

## 更新日志

### 2026.10.2 — 整合包诊断套件

新增五个工具，把「整合包为什么崩」这件事从头到尾覆盖掉。

| 新增 | 作用 |
| --- | --- |
| **崩溃日志分析 crash-doctor** | 把 crash-reports / logs 里的英文报错翻成中文结论和处理步骤 |
| **Java 环境诊断 java-doctor** | 扫出机器上所有 Java，判断游戏该用哪个，给出 JVM 参数和内存建议 |
| **模组依赖检查 mod-check** | 拆开每个 jar 读元数据，查缺前置、重复、损坏、版本错配、加载器混装 |
| **联机方案决策 net-plan** | 问几个问题，直接给出联机方案和分步做法 |
| **交付报告生成 report-builder** | 把上面三个的 json 结果汇总成一份 HTML 诊断报告 |

配套改动：

- 三个诊断工具跑完会自动生成 **`发给客服.txt`**（同时进剪贴板）和 **`发给客服.png`**
  卡片图。很多聊天工具不能发文件，只能发文字和图片，所以结果做成这两种形态
- 交付物里**只写整合包名字，不写完整路径**，不带出用户名之类的信息
- 崩溃日志分析新增 JEI 相关规则；同时修掉两处把**正常日志误判成故障**的规则
  （`GL Caps: ... OpenGL 3.2` 和 Mixin 的 `Error loading class`），
  并给规则加了上下文过滤——命中行必须像"出事了"才算数
- 模组依赖检查重写了元数据解析，支持 NeoForge 1.20.5+ 的 `neoforge.mods.toml`、
  NeoForge 的 `type=required/optional`、Forge 1.12 的 `mcmod.info`（这类文件常常不是合法 JSON）、
  老 Forge 的 `modid@[版本区间]` 写法，以及 Fabric / NeoForge 的 jar-in-jar 嵌套
- 在 10 个真实整合包（合计 2200 多个 jar）上做了回归测试。
  修之前，一个正常运行的整合包会被报出 35 条"缺前置"；修之后降到个位数，
  剩下的人工逐条核对全部属实
- 修掉 `net-plan` 的一个严重缺陷：问答模式下的答案会被参数校验拒绝，
  导致**不管怎么回答都推荐同一个方案**
- **全部工具、全部文档加入版权声明**：免费开源，严禁二次打包售卖；
  付费获得的请立即退款并投诉卖家。声明会打印在运行窗口和报告文件里，
  卡片图页脚也带上了一行

### 2026.10 — 首发

整合包体检 v3.1、联机网络体检 v1.1、跨境网络体检 v1.0、跨境联机教程 v1.0。

## 目录结构

```
.
├── README.md
└── docs/
    ├── crash-doctor.md          崩溃日志分析 · 完整说明
    ├── java-doctor.md           Java 环境诊断 · 完整说明
    ├── mod-check.md             模组依赖检查 · 完整说明
    ├── net-plan.md              联机方案决策 · 完整说明
    ├── report-builder.md        交付报告生成 · 完整说明
    ├── modpack-doctor.md        整合包体检 · 完整说明
    ├── mc-net-check.md          联机网络体检（国内版）· 完整说明
    ├── mc-net-check-intl.md     跨境网络体检（国际版）· 完整说明
    ├── crossplay-guide.md       跨境联机教程 · 完整说明
    ├── crossplay-card.pdf       跨境联机速查卡 · 一页 A4，打印用
    └── crossplay-card.png       跨境联机速查卡 · 图片，发微信/QQ 用
```

十个 zip 分发包不放在仓库里，全部作为 Release 资产提供，点一下直接下载。

## 版权与免责

> ### ⚠️ 该工具为免费发放且在 github 上开源，严禁二次打包售卖
>
> **若你付费获得该工具，请立即退款并投诉卖家。**
>
> 禁止将本工具或其任何部分用于任何形式的盈利活动，包括但不限于：
> **打包售卖、付费代装、随付费服务搭售、放入付费资源包或会员专享内容中分发。**
>
> 想分享给朋友的话，直接发仓库地址就行：
> <https://github.com/beihongliangchu/mctools>

本项目免费开源，**任何人都不应该为获得这些工具而付费**。
所有工具里都内置了同样的声明，运行时会直接打印出来。

仅供学习和自用。请遵守你所在地区的法律法规以及 Minecraft 最终用户许可协议。
工具不包含任何绕过正版验证的功能。使用本工具产生的任何后果由使用者自行承担。
