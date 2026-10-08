# MC 跨境联机教程 使用说明

*中国玩家 + 国外朋友，从零玩到一起*

## 一、先看这里（30 秒看完）

1. 国外朋友下不了 PCL，是因为 PCL 的下载放在国内网盘（蓝奏云、百度网盘）。
   - 解决办法：国外朋友改下 HMCL，它的下载站在 GitHub，全球都能直连。

两边不需要用同一个启动器。一个用 PCL、一个用 HMCL，完全可以联机。
真正必须一样的是：游戏版本 + 模组。

2. 开服四个方案，按情况挑一个：

| 方案 | 谁花钱 | 服务器在哪 | 大概延迟 | 适合谁 |
|---|---|---|---|---|
| A 免费 | 不花钱 | 国外朋友那边 | 150 到 300 毫秒 | 想先试试、玩纯净服 |
| B 免费 | 不花钱 | 国内玩家这边 | 200 到 400 毫秒 | 想自己开、愿意折腾 |
| C 付费 | 约 20-70 元/月 | 中立节点（新加坡等） | 两边都 50 到 120 毫秒 | 长期玩，最稳 |
| D 付费 | 约 25-40 元/月 | 香港轻量服务器 | 国内 30 到 60，国外 100 到 250 | 国内玩家主导 |

懒人结论：想零成本选 A；想玩得舒服选 C。

3. 两边必须对齐：同一个游戏版本，完全一样的模组。
   - 最省事的做法是两个人装同一份整合包（Modrinth 上的）。纯净服就不用装模组。

## 二、第 1 步：两边各装一个启动器

### 【国外朋友】装 HMCL

1. 打开 <https://github.com/HMCL-dev/HMCL/releases>
2. 在最新版本下面的 Assets 里，下载 `HMCL-x.x.x.exe`
3. 双击运行，界面是中文的，可以在设置里改成英文
4. 如果提示找不到 Java，先装 Java 21：<https://adoptium.net>
   - 下载 Temurin 21 的 `.msi`，一路"下一步"装完，再双击 HMCL
5. exe 实在跑不起来，就下载 `HMCL-x.x.x.jar`，装好 Java 21 后双击它

HMCL 能自动下载游戏本体、自动装 Forge / Fabric、自动装整合包，全程点鼠标。

### 【国内玩家】用 PCL 就行

- 官方发布页在爱发电，搜索"龙腾猫跃"，按页面说明下载。
- PCL 官方下载走国内网盘，你在国内下没问题。

### 【国外朋友如果一定要 PCL】

- PCL 社区版在 GitHub 有发布页：<https://github.com/PCL-Community/PCL-CE/releases>
- 下载 `PCL2_CE_Release_x64.exe`。
- 注意：这个版本需要先装微软的 .NET 10 桌面运行时，
  去 <https://dotnet.microsoft.com/download/dotnet/10.0> 下载安装，
  装完再打开 PCL。比 HMCL 多一步，所以还是推荐 HMCL。

## 三、第 2 步：把版本和模组对齐（做错这步，后面全白搭）

- 版本号必须完全一样。1.20.1 和 1.20.4 连不上。
- 有模组的话，两边模组必须一模一样，包括版本号，多一个少一个都不行。
- 最省事：找同一份整合包，两个人各装一份。
  - 去哪找：<https://modrinth.com/modpacks>
  - <https://www.curseforge.com/minecraft/modpacks>
  - HMCL 和 PCL 里都能直接搜 Modrinth / CurseForge 的整合包，搜到点安装。
- 第一次联机建议先用纯净版（不加模组）试通，再加模组。
- Java 不用自己装，启动器会自动下载对应版本。

对齐之后，各自先单机进一次游戏，能进到主界面再往下做。

## 四、第 3 步：选一个开服方案

### 【方案 A】免费 · 国外朋友开服，用 Aternos

最适合"就是想玩玩看"。

1. 第 1 步  国外朋友打开 <https://aternos.org>，用邮箱注册并登录
2. 第 2 步  点"创建服务器"，选版本（必须和两边客户端一致），可加模组或整合包
3. 第 3 步  建好后点"启动"。免费服要排队，等状态变成绿色在线
4. 第 4 步  页面上会显示服务器地址，形如 `xxxx.aternos.me`
5. 第 5 步  把地址发给对方，游戏里"多人游戏 → 添加服务器"填进去

缺点：要排队；长时间没人会自动关机；性能一般，人多会卡。
同类免费站：<https://minehut.com>

### 【方案 B】免费 · 国内玩家开服，用组网工具让朋友连进来

适合：你电脑还不错，想自己开。
前提：国内家宽一般没有公网 IP，必须用组网工具，直接给 IP 对方连不上。

1. 第 1 步  两边都装 Tailscale：<https://tailscale.com/download>
   - 用同一个账号登录（你注册，把对方的设备加进来也行）
2. 第 2 步  两台电脑都打开 Tailscale，确认都显示在线
   - 在 Tailscale 面板能看到你这台机器的地址，形如 `100.x.x.x`
3. 第 3 步  你打开 Minecraft，进入一个世界，按 ESC →"对局域网开放"
   - 端口默认 `25565`，点确定，记住这个端口
4. 第 4 步  把 `100.x.x.x` 和端口发给对方
   - 他在游戏里"直接连接"，填 `100.x.x.x:25565`

注意：

- 你的游戏必须一直开着，关了局域网就断了
- 想长期挂机，用 PCL / HMCL 下载一个服务端（Paper 最省事）单独跑
- Tailscale 两边连不上就换 ZeroTier：<https://www.zerotier.com/download>
- 还不行就用 EasyTier（国产，国内节点多）：<https://github.com/EasyTier/EasyTier/releases>

### 【方案 C】付费 · 租一台中立服务器（长期玩最推荐）

为什么推荐：两边延迟都在 50 到 120 毫秒，谁都不吃亏，
也不用谁的电脑一直开着。

去哪租：

- 省事型（网页控制面板，点几下就能开服）
  - PebbleHost    <https://pebblehost.com>      约 $1 到 3 / 月
  - Bloom.host    <https://bloom.host>
  - BisectHosting <https://bisecthosting.com>
- 便宜自由型（自己装服务端）
  - 甲骨文永久免费 <https://www.oracle.com/cloud/free/>
  - Vultr         <https://www.vultr.com>
  - Hetzner       <https://www.hetzner.com>

选节点：优先新加坡、日本、香港。别选欧美，那样两边都慢。
配置：纯净服 2 核 2G 够用；加十几个模组建议 2 核 4G。
花费：大约每月 20 到 70 元。
谁买：有国际信用卡或 PayPal 的一方买，国外朋友买最方便。
面板类一键开服，跟着网页提示选版本、上传整合包就行。

### 【方案 D】付费 · 国内玩家开服，租香港轻量服务器

适合：你想自己掌控，又不想被跨国线路折腾。

- 阿里云 / 腾讯云 香港轻量应用服务器，约 25 到 40 元 / 月
- 国内连香港 30 到 60 毫秒，国外朋友 100 到 250 毫秒
- 在服务器上装好 Java 和服务端（Paper 最简单），放行端口
- 两边都连"服务器公网 IP:端口"

重要：买之前确认节点是"香港"或"境外"。
买成国内节点的话，国外朋友会被绕远，甚至连不上。

## 五、第 4 步：进游戏

1. 拿到服务器地址（形如 `xxxx.aternos.me` 或 `1.2.3.4:25565`）
2. 打开启动器，启动游戏
3. 主菜单 → 多人游戏 → 添加服务器 → 名称随便填，地址粘进去 → 完成
4. 双击加入

进不去，按这个顺序查：

- 地址有没有多空格、漏掉端口
- 服务器是不是真的在线（免费服可能在排队或已关机）
- 服务器防火墙有没有放行端口
- 两边游戏版本是不是完全一致
- 两边模组是不是完全一致

关于正版：

- 服务器设成离线模式（`online-mode=false`）时，不需要正版账号也能进，
  但任何人都能用同样的名字混进来，建议同时开白名单。
- 服务器设成正版验证时，双方都必须有正版 Minecraft 账号。

## 六、常见问题

### 问：朋友说 PCL 的下载页打不开

答：PCL 官方下载放在国内网盘，国外确实很难下。让他改下 HMCL，或者用 PCL 社区版
（<https://github.com/PCL-Community/PCL-CE/releases>，需要先装 .NET 10 运行时）。
两边启动器不一样，不影响联机。

### 问：GitHub 打不开（国内玩家常见）

答：国内玩家直接用 PCL 官方版就行，不用碰 GitHub。
确实要下 GitHub 上的东西，让国外朋友下好再用聊天软件传给你。

### 问：进服提示 Mod rejections / 不兼容的模组

答：模组对不上。两边用同一份整合包，或者把不一样的模组删到完全一致。

### 问：提示 Outdated server / Outdated client

答：版本号不一致，把两边改成同一个版本。

### 问：一直卡在"正在连接"

答：地址错、服务器没开、或者防火墙挡住了。
用方案 B 的话，先让两边互相 ping 一下 `100.x.x.x`，
能通才说明组网成功，再回游戏里连。

### 问：能进去但是很卡，人会被拉回原位

答：跨国线路本来就有 150 到 300 毫秒延迟，抖得厉害时就会回弹，
这是物理距离决定的，不是谁设置错了。
想舒服就换方案 C，把服务器放在两边中间。

### 问：需要买正版吗

答：见上面"关于正版"。想省事就买正版，不用折腾验证问题。

### 问：免费方案能长期用吗

答：Aternos 这类免费服会排队、会休眠、人多了会卡，适合试水。
真想长期玩，一个月二三十块钱的中立服务器体验好太多。

## 七、下载地址清单

启动器

- HMCL（推荐给国外朋友）  <https://github.com/HMCL-dev/HMCL/releases>
- PCL 社区版（GitHub）    <https://github.com/PCL-Community/PCL-CE/releases>
- PCL 官方版              爱发电搜索"龙腾猫跃"
- Java 21（HMCL 需要时）  <https://adoptium.net>
- .NET 10 运行时（PCL 社区版需要）  <https://dotnet.microsoft.com/download/dotnet/10.0>

整合包和模组

- Modrinth    <https://modrinth.com/modpacks>
- CurseForge  <https://www.curseforge.com/minecraft/modpacks>

免费开服

- Aternos  <https://aternos.org>
- Minehut  <https://minehut.com>

组网工具

- Tailscale  <https://tailscale.com/download>
- ZeroTier   <https://www.zerotier.com/download>
- EasyTier   <https://github.com/EasyTier/EasyTier/releases>

付费开服

- PebbleHost        <https://pebblehost.com>
- Bloom.host        <https://bloom.host>
- BisectHosting     <https://bisecthosting.com>
- 甲骨文永久免费    <https://www.oracle.com/cloud/free/>
- Vultr             <https://www.vultr.com>
- Hetzner           <https://www.hetzner.com>

## 八、版本

- 本次发布    v1.0
- 内容        首次整理。含 HMCL / PCL 两种启动器，免费与付费共四种开服方案。

出错请把截图和游戏版本号一起发回来。
