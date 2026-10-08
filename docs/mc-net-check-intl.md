# MC 跨境网络体检工具（国际版） 使用说明 · MC Net Check (International) User Guide

*mc-net-check-intl v1.0*

本说明中英对照，**\[EN\]** 段落给国外玩家看，**\[CN\]** 段落给国内玩家看。
This guide is bilingual. **\[EN\]** blocks are for the overseas player,
**\[CN\]** blocks are for the Chinese player.

## 一 / 1. 这个工具是干什么的 · What this tool does

**EN** It measures the network between your PC and the Minecraft server, so we can
tell whether the lag is caused by the network or by the game server.
It reports packet loss, latency, jitter, plus three things the older
version did not check: TCP reachability, path MTU, and your NAT type.
It fixes nothing. It only measures.

**CN** 联机玩 Minecraft 时卡、走路被拉回去、挖方块又弹回来，用这个工具查原因。
它测丢包率、延迟、抖动，另外还测三项老版本没有的东西：TCP 端口连通、
路径 MTU、NAT 类型。它不修复任何东西，只负责把数据测出来。

适用场景：国内玩家和国外玩家跨境联机，用 FRP、EasyTier、Tailscale、
playit.gg、ZeroTier 之类的工具中转，出现卡顿或回弹时。

## 二 / 2. 运行条件 · Requirements

**EN** OS Windows 10 / 11
Software nothing extra, PowerShell is built in
Network yes, it is a network tool
Rights normal user, administrator is NOT required

**CN** 系统 Windows 10 / 11
软件 不需要另外装任何东西，PowerShell 是系统自带的
网络 需要联网，它本来就是测网络的
权限 普通用户即可，不需要管理员权限

**重要 / Important**

**EN** Run it on the PC that LAGS - the joining player, not the host.
Keep the tunnel / VPN tool RUNNING the whole time.

**CN** 必须在【会卡、会回弹的那台电脑】上运行，也就是加入的那一方。
测试期间联机软件必须一直开着，不要断开。
在一台没参与联机的电脑上跑，测出来的是那台电脑的线路，没有意义。

## 三 / 3. 怎么用 · How to use

### 第 1 步 / Step 1

**EN** Unzip the package into a normal folder (Desktop is fine).
Do NOT run it from inside the zip. Unzip first.
The `.bat` and the `.ps1` must stay in the same folder.

**CN** 把压缩包解压到一个普通文件夹里（桌面就行，路径里有中文也没关系）。
不要直接在压缩包里双击运行，一定要先解压出来。
`mc-net-check-intl.bat` 和 `mc-net-check-intl.ps1` 必须待在同一个文件夹里。

### 第 2 步 / Step 2

**EN** Start Minecraft and make sure you can actually get into the server
right now, even if it lags. Keep the game and the tunnel tool open.

**CN** 先打开游戏，确认现在确实能连上服务器、能进游戏，哪怕很卡。
游戏和联机软件都保持开着。

### 第 3 步 / Step 3

**EN** Double-click `mc-net-check-intl.bat`

**CN** 双击 `mc-net-check-intl.bat`

### 第 4 步 / Step 4

**EN** It asks you two addresses. Type each one and press Enter.
Leave it empty and press Enter to skip.

- Relay / tunnel node address
  - The node address shown in your tunnel panel or config.
  - May include a port. Example: `us-1.example.com:7000`
  - Not sure? Just press Enter to skip.
- Game server address
  - The exact address you type into Minecraft to join.
  - Example: `xxxx.aternos.me` or `1.2.3.4:25565`
  - Not sure? Just press Enter to skip.
  - If you leave the port out, it assumes 25565.

**CN** 它会问你两个地址，逐个填进去回车。不知道就留空直接回车跳过。

- 中转节点地址
  - 联机面板或配置文件里显示的那个服务器地址，可以带端口。
  - 例如：`us-1.example.com:7000`
- 游戏服务器地址
  - 你在游戏里"直接连接"填的那个地址。
  - 例如：`xxxx.aternos.me` 或 `1.2.3.4:25565`
  - 不写端口的话，按 Minecraft 默认的 25565 测。

### 第 5 步 / Step 5

**EN** Wait 3 to 6 minutes. Do not close the window.

**CN** 等 3 到 6 分钟，中间不要关窗口。

### 第 6 步 / Step 6

**EN** It writes `mc-net-check-intl-result.txt` in the same folder.
Send that whole txt file back.

**CN** 跑完会在同一个文件夹里生成 `mc-net-check-intl-result.txt`。
把这个 txt 文件整个发回来就行。

**EN** During the test, close Thunder / cloud sync / streaming / Windows Update.
They eat bandwidth and distort the result. Prefer a cable over Wi-Fi.

**CN** 测试期间建议关掉迅雷、网盘同步、直播、系统更新，这些会占用带宽让结果失真。
用无线网的话尽量离路由器近一点，能插网线最好插上。

## 四 / 4. 报告里那几个数字是什么意思 · What the numbers mean

### 丢包率 / Packet loss

**EN** The most important one. Minecraft runs on TCP, so every lost packet is
retransmitted, and during the retransmission your position sync freezes.
That is exactly what "getting rubber-banded" looks like.

**CN** 最重要的指标。Minecraft 走 TCP，丢一个包就要重传，重传期间位置同步全部
卡住，表现出来就是回弹。跨境链路上 0% 才算真正正常。

### 延迟 / Latency

**EN** Look at the average, but trust the maximum and the P95 more.
A steady 150 ms plays far better than 60 ms average with 500 ms spikes.

**CN** 看平均值，但更要看最大值和 P95（95% 的包都在这个值以内）。
稳定 150 毫秒，比平均 60 毫秒、最大 500 毫秒舒服得多。

### 抖动 / Jitter

**EN** How much consecutive packets vary. This predicts rubber-banding better
than the average does. High but stable is playable; low but jumpy is not.

**CN** 相邻两个包延迟的波动幅度，以及整体标准差。这个指标比平均延迟更能预测回弹：
延迟高但稳定还能玩，延迟不高但抖得厉害，会频繁被服务器判定移动异常，
然后把你拉回原位。

## 五 / 5. 判定标准 · How the verdict is decided

**EN** This version does NOT use one fixed threshold table. Cross-Pacific links are
150-300 ms by physics, so judging them with a same-city standard would call
every single link broken. Instead the tool measures first, then picks a
profile from the measured average latency, and states which one it used.

**CN** 这一版不再套用一张固定阈值表。跨太平洋线路物理上就有 150~300 毫秒，
拿同城标准去判会把每一条线路都判成有问题。所以工具先测，再按实测平均
延迟选一档标准，并在报告里写明用的是哪一档。

| 分档 / Profile | 触发条件 / Trigger | 说明 / Meaning |
|---|---|---|
| LOCAL | 平均延迟 < 60 ms | 本地 / 同城链路 |
| REGIONAL | 60 ~ 130 ms | 区域内 / 跨州链路 |
| LONG-HAUL | >= 130 ms | 跨洋 / 长距离链路 |

| 指标 / Metric | LOCAL | REGIONAL | LONG-HAUL |
|---|---|---|---|
| 丢包 loss | 1% / 3% | 2% / 5% | 3% / 8% |
| 抖动 jitter | 10 / 25 ms | 15 / 30 ms | 25 / 50 ms |
| 平均延迟 avg | 60 / 120 ms | 130 / 250 ms | 300 / 450 ms |

每格的两个值：左=偏高 右=过高 / left=high, right=very high

**EN** Packet loss is always judged strictly, in every profile. Loss is never
"normal" on a long link - it is worse on a long link, not better.
Three or more burst-loss runs (2+ packets lost in a row) is flagged as
congestion in every profile.

**CN** 丢包在每一档里都判得严。长链路上丢包不会变得"正常"，只会更致命。
连续丢包段达到 3 次以上，在任何一档里都判定为链路拥塞。

## 六 / 6. 这三项是新加的 · The three new tests

### 【5】TCP 端口连通 / TCP port reachability

**EN** The decisive test. Minecraft runs on TCP, and many servers, ISPs and cloud
security groups block ICMP (ping) outright. When that happens the ping
section shows 100% loss while the game works fine. This test actually
opens a TCP connection to the server port, 20 times, and measures the
handshake time and the success rate.
If this one fails, the game really cannot connect.

**CN** 关键项。Minecraft 走 TCP，而大量服务器、运营商和云厂商的安全组直接屏蔽
ICMP（ping）。这种情况下 ping 那一节显示 100% 丢包，但游戏其实是通的。
这一项是真的去连服务器的 TCP 端口，连 20 次，测握手耗时和成功率。
它不通，才代表游戏是真的连不上。
握手耗时大致等于一个来回的延迟，可以和 ping 的数字互相印证。

### 【6】路径 MTU / Path MTU

**EN** The most common tunnel and accelerator problem that nobody checks.
Small pings pass, but the moment the game transfers a chunk of data -
a big packet - it gets dropped, and the game stutters or freezes.
The tool sends unfragmented pings of decreasing size and finds the
largest one that gets through.
MTU below 1500 means tunnel/VPN overhead. Below 1400 is a real problem.

**CN** 隧道和加速器最常见的坑，但几乎没人测。小包 ping 一路正常，可游戏一开始
传输区块数据（大包）就卡，就是这个问题。
工具会发送不分片的大包，逐步缩小尺寸，找出能通过的最大值。
MTU 不到 1500 说明隧道有额外开销；低于 1400 就是真问题。

### 【8】出口公网 IP 与 NAT 类型 / Public IP and NAT type

**EN** Answers "can I host the server myself?".

- PUBLIC - you are directly on the internet, you can host.
- NAT - behind your own router, you can host but must forward the port.
- CGNAT - behind your ISP's NAT. Port forwarding is useless.
  You cannot host directly. Use a relay, a VPN mesh, or rent one.

**CN** 回答"我能不能自己开服"。

- PUBLIC - 直接在公网上，可以开服。
- NAT - 在自己路由器后面，可以开服，但要做端口映射。
- CGNAT - 在运营商大内网里，路由器上做映射也没用，自己开服开不了。
  这种情况必须走中转节点、组网工具，或者直接租服务器。

美国不少家宽（T-Mobile Home Internet、部分 Starlink 等）就是 CGNAT。

## 七 / 7. 常见问题 · FAQ

### 问：双击 .bat 一闪就没了

Q: The .bat window flashed and closed

**答 / A:** 看是不是没解压，直接在压缩包里点了。必须先解压出来再双击。
另外确认 `.bat` 和 `.ps1` 在同一个文件夹里。

**A:** You probably ran it from inside the zip. Unzip first, then double-click.
Also make sure the `.bat` and the `.ps1` are in the same folder.

### 问：Windows 弹出"已保护你的电脑"蓝色提示

Q: Windows shows a blue "Windows protected your PC" box

**答 / A:** 这是 SmartScreen 对来源未知文件的常规提醒，不是报毒。
点"更多信息"，再点"仍要运行"。

**A:** That is the standard SmartScreen warning for files it has not seen before,
not a virus alert. Click "More info", then "Run anyway".

### 问：提示"禁止运行脚本"或者执行策略报错

Q: "Running scripts is disabled" or an execution policy error

**答 / A:** 用 `.bat` 启动，它自带绕过参数。不要直接双击 `.ps1`。

**A:** Launch it through the `.bat` file - it passes the bypass flag for you.
Do not double-click the `.ps1` directly.

### 问：报告打开是乱码

Q: The report file looks like garbage

**答 / A:** 报告是带 BOM 的 UTF-8，用记事本、写字板或者 VS Code 打开。
别用老式的 GBK 编辑器。

**A:** The report is UTF-8 with BOM. Open it with Notepad, WordPad or VS Code.

### 问：某一行显示 100% 丢包，但游戏能正常玩

Q: Something shows 100% loss but the game works fine

**答 / A:** 见第六节。对方屏蔽了 ICMP。去看【5】TCP 端口连通那一节，那才是结论。

**A:** That target blocks ICMP. See section 6. Look at the TCP section instead -
that one reflects reality.

### 问：中转节点地址不知道填哪个

Q: I do not know what to put as the relay node

**答 / A:** 填面板上显示的那个服务器地址，不是你游戏的端口。
实在找不到就留空回车，只测服务器地址那一项，也能看出主要问题。

**A:** Use the node address shown in your tunnel panel, not your game port.
If you cannot find it, just press Enter and skip - testing the server
address alone still shows the main problem.

### 问：能不能在别的电脑上帮我测

Q: Can someone else run this for me?

**答 / A:** 不行。网络测量的结果只对跑测量的那台电脑到目标的线路有意义。
必须是会卡的那一方自己跑。

**A:** No. A measurement is only meaningful on the machine that ran it.
The player who lags has to run it, on their own PC.

### 问：游戏卡，但报告说全是"良好"

Q: The game lags but the report says everything is OK

**答 / A:** 那就不是网络问题。去查服务端 TPS，见报告最后一节。

**A:** Then it is not the network. Check the server TPS - see the last section
of the report.

## 八 / 8. 安全说明 · Privacy and safety

**EN**

- It only measures the network and reads local NIC information.
  It does not change any system setting.
- It does not upload any local data.
- Administrator rights are NOT required.
- Both files are plain text. You can open them in Notepad and read them.
- ONE exception: to detect CGNAT it asks a public service (ipify /
  icanhazip) for your egress IP address. That request sends nothing about
  you. Skip it entirely by running the `.ps1` with `-SkipPublicIp`.
- The report contains your private LAN addresses and gateway. If you do
  not want to share those, delete section 【1】 before sending it.

**CN**

- 只做网络测量和读取本机网卡信息，不修改系统任何设置
- 不会上传任何东西，报告只存在你本地的 txt 文件里
- 不需要管理员权限
- 两个文件都是纯文本，可以用记事本打开自行检查
- 唯一的例外：为了判断 CGNAT，会向公共查询服务（ipify / icanhazip）
  问一次你的出口 IP。这个请求不含任何关于你的信息。
  不想让它发，就用 `-SkipPublicIp` 参数运行 `.ps1`。
- 报告里有你的内网地址和网关。不想让别人看到，发之前把【1】那一节删掉。

唯一会产生的文件是 `mc-net-check-intl-result.txt`，就是你发回来的那份报告。
The only file it creates is `mc-net-check-intl-result.txt`.

## 九 / 9. 版本 · Version

本次发布 / Release v1.0

**EN** First release of the international build. Differences from the mainland
build mc-net-check v1.1:

- bilingual output, English first
- latency profiles instead of one fixed threshold table
- TCP port reachability test (works when ICMP is blocked)
- path MTU probe
- public IP and CGNAT detection
- IPv6 tested against several targets instead of one hard-coded DNS

**CN** 国际版首次发布。与国内版 mc-net-check v1.1 的区别：

- 中英对照输出，英文在前
- 按实测延迟分档判定，不再套用一张固定阈值表
- 新增 TCP 端口连通测试（ICMP 被屏蔽时仍然有效）
- 新增路径 MTU 探测
- 新增出口公网 IP 与 CGNAT 判断
- IPv6 改为多目标探测，不再写死某一个 DNS

详细问题请连同 `mc-net-check-intl-result.txt` 一起发回。
Send the whole `mc-net-check-intl-result.txt` back with any question.
