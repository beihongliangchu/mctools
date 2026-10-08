# MCtools

《我的世界》联机诊断与整合包体检工具，外加一份跨境联机教程。

全部免费、免安装，解压双击就能用。只支持 **Windows 10 / 11**，用系统自带的 PowerShell 运行，
**不需要管理员权限**，不需要额外装任何东西。

**[⬇ 前往 Releases 页面下载全部工具](https://github.com/beihongliangchu/mctools/releases/latest)**

## 下载

| 工具 | 版本 | 下载 | 什么时候用 |
| --- | --- | --- | --- |
| 整合包体检 | v3.1 | **[modpack-doctor-v3.1.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10/modpack-doctor-v3.1.zip)** | 整合包打不开、闪退、报缺前置、Java 版本不对 |
| 联机网络体检（国内版） | v1.1 | **[mc-net-check-v1.1.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10/mc-net-check-v1.1.zip)** | 国内玩家之间联机，卡顿、走路回弹 |
| 跨境网络体检（国际版） | v1.0 | **[mc-net-check-intl-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10/mc-net-check-intl-v1.0.zip)** | 国内玩家和国外玩家跨境联机 |
| 跨境联机教程 | v1.0 | **[mc-crossplay-guide-v1.0.zip](https://github.com/beihongliangchu/mctools/releases/download/2026.10/mc-crossplay-guide-v1.0.zip)** | 从零教两个人怎么连上，含一页 A4 速查卡 |

> 下载下来的文件名是英文的（`modpack-doctor-v3.1.zip` 这样），因为 GitHub 不接受
> 发布包名字里的中文。**解压之后的文件夹和文件仍然是中文名**，不影响使用。

## 四个工具分别是什么

### 1. 整合包体检 modpack-doctor

检查一个 Minecraft 整合包能不能正常启动。它会核对 Java 版本、扫描模组列表、
找出缺失的前置模组、检查内存配置和常见冲突，最后给一份体检报告。

适合：整合包下载下来打开就崩、进游戏报一堆红字、不知道哪个模组冲突的时候。

📖 [完整使用说明](docs/modpack-doctor.md)

### 2. 联机网络体检 mc-net-check（国内版）

诊断联机卡顿、走路被拉回去、挖方块弹回来到底是链路问题还是服务端问题。
分三段测量：本机到路由器、本机到联机节点（FRP 等）、本机到主机，
各自给出丢包率、延迟、抖动，外加路由走向和 IPv6 可用性。

适合：用 frp、樱花 frp、OpenFrp、EasyTier、ZeroTier、蒲公英之类工具联机的国内玩家。

📖 [完整使用说明](docs/mc-net-check.md)

### 3. 跨境网络体检 mc-net-check-intl（国际版）

同一个工具的国际化版本，专门给不在中国大陆的玩家用。**中英对照输出，英文在前。**

相比国内版做了这些改动：

- 判定阈值按实测延迟自动分档（本地 / 区域 / 跨洋），不再一律套用国内标准
- 新增 **TCP 端口连通测试** —— 大量服务器和云厂商默认屏蔽 ICMP，ping 显示完全不通但游戏其实能连
- 新增 **路径 MTU 探测** —— 隧道和加速器最常见的坑，小包正常大包丢
- 新增 **出口公网 IP 与 CGNAT 判断** —— 直接回答「我能不能自己开服」
- IPv6 测试改用多目标探测，不再写死某一个 DNS

> 这是**两份独立代码**，不是同一个脚本的两个开关。国内版继续按国内网络调优，两边不会自动同步。

📖 [完整使用说明](docs/mc-net-check-intl.md)

### 4. 跨境联机教程

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

## 运行条件

|  |  |
| --- | --- |
| 系统 | Windows 10 / 11 |
| 软件 | 不需要额外安装，PowerShell 是系统自带的 |
| 权限 | 普通用户即可，不需要管理员权限 |
| 网络 | 两个网络体检工具需要联网，它们本来就是测网络的 |
| 启动方式 | 双击 `.bat`，不要直接双击 `.ps1`（会被执行策略拦住） |

## 安全说明

- 工具只做网络测量和读取本机网卡信息，**不修改系统任何设置**
- **不上传任何本地数据**。报告只存在你本地的 txt 文件里
- 唯一的例外：国际版为了判断 CGNAT，会向公共查询服务（ipify / icanhazip）问一次你的出口 IP。
  不想让它发，用 `-SkipPublicIp` 参数运行即可
- 所有文件都是纯文本，可以用记事本打开自行检查

## 目录结构

```
.
├── README.md
└── docs/
    ├── modpack-doctor.md        整合包体检 · 完整说明
    ├── mc-net-check.md          联机网络体检（国内版）· 完整说明
    ├── mc-net-check-intl.md     跨境网络体检（国际版）· 完整说明
    ├── crossplay-guide.md       跨境联机教程 · 完整说明
    ├── crossplay-card.pdf       跨境联机速查卡 · 一页 A4，打印用
    └── crossplay-card.png       跨境联机速查卡 · 图片，发微信/QQ 用
```

四个 zip 分发包不放在仓库里，全部作为 Release 资产提供，点一下直接下载。

## 免责

仅供学习和自用。请遵守你所在地区的法律法规以及 Minecraft 最终用户许可协议。
工具不包含任何绕过正版验证的功能。使用本工具产生的任何后果由使用者自行承担。
