# ShiYi 配置文件

一套面向 Surge、Loon、Stash、Shadowrocket 和 Egern 的个人分流配置。

按服务选择出口 · 常用国内应用直连 · 支持自建节点与订阅节点

> 本项目提供配置文件，不提供节点或订阅服务。不同客户端的配置格式和规则优先级不同，请使用对应文件，并在导入后检查实际命中情况。

## 配置文件

| 客户端 | 查看配置 | 原始地址 |
| --- | --- | --- |
| Surge | [Surge.conf](https://github.com/wanxiao-wx/ShiYi/blob/main/Surge.conf) | [Raw](https://raw.githubusercontent.com/wanxiao-wx/ShiYi/main/Surge.conf) |
| Loon | [Loon.conf](https://github.com/wanxiao-wx/ShiYi/blob/main/Loon.conf) | [Raw](https://raw.githubusercontent.com/wanxiao-wx/ShiYi/main/Loon.conf) |
| Stash | [Stash.yaml](https://github.com/wanxiao-wx/ShiYi/blob/main/Stash.yaml) | [Raw](https://raw.githubusercontent.com/wanxiao-wx/ShiYi/main/Stash.yaml) |
| Shadowrocket | [Shadowrocket.conf](https://github.com/wanxiao-wx/ShiYi/blob/main/Shadowrocket.conf) | [Raw](https://raw.githubusercontent.com/wanxiao-wx/ShiYi/main/Shadowrocket.conf) |
| Egern | [Egern.yaml](https://github.com/wanxiao-wx/ShiYi/blob/main/Egern.yaml) | [Raw](https://raw.githubusercontent.com/wanxiao-wx/ShiYi/main/Egern.yaml) |

> 配置可能包含个人节点、密码或订阅地址。使用和分享前，请检查文件内容，删除或替换不属于你的节点信息；不要将自己的私人凭据提交到公开仓库。

## 功能概览

| 功能 | 说明 |
| --- | --- |
| 节点选择 | 在自建节点、订阅节点和直连等可用策略之间切换；具体选项依客户端而异 |
| 地区策略 | Loon、Stash、Shadowrocket、Egern 提供香港、日本、新加坡、美国和德国的手动策略组 |
| 服务分流 | 常用服务可独立选择出口，包括 AI、Telegram、X、TikTok、Netflix、Emby、Google 和苹果、微软服务 |
| 国外媒体 | YouTube 等流量可使用国外媒体策略；Netflix 和 TikTok 使用独立策略 |
| 国内应用 | 微信、网易云音乐、B站、微博、小红书配置了直连规则集，具体命中仍受规则顺序和客户端配置影响 |
| 金融服务 | Loon、Stash、Shadowrocket、Egern 将国内金融、国际支付和数字资产分开；后三者还提供国际券商策略 |
| PT 与测速 | 提供 PT 站点策略和 Speedtest 策略，便于按用途选择出口 |

各端并非完全相同：**Surge 文件保留原有策略结构**，包含台湾、韩国、英国等地区及 HBO、Spotify、OneDrive、Bilibili、WeChat、E-Hentai 等独立策略；不要将其他客户端的精简结果视为 Surge 已同步修改。

## 快速开始

1. 备份客户端当前配置，下载上表中与你的客户端对应的文件并导入。
2. 按下表添加自己的订阅。`https://YOUR_SUBSCRIPTION_URL` 是占位地址，不能直接使用。
3. 如需自建节点，在本地配置或客户端中添加，并将节点加入相应策略组。不要提交包含密码的配置。
4. 启用配置，更新远程规则和订阅，然后在策略组中选择节点。Shadowrocket 还需确认“全局路由”使用配置模式。
5. 使用客户端的请求记录或规则测试功能，检查常用服务实际命中了哪条规则、使用了哪个出口。

| 客户端 | 添加订阅的位置 |
| --- | --- |
| Surge | `[Proxy Group]` 中的 `订阅节点`，修改 `policy-path` |
| Loon | `[Remote Proxy]` 中的 `订阅`；重命名订阅后，同步检查 `[Remote Filter]` 引用 |
| Stash | `proxy-providers` → `订阅` → `url` |
| Shadowrocket | 在 App 的“订阅”中添加；配置中的地区组按节点名称筛选 |
| Egern | `policy_groups` 中的 `订阅节点` → `urls` |

订阅内容需要与目标客户端兼容；同一链接能否用于全部客户端取决于订阅服务提供的格式。首次获取远程规则可能受网络或上游资源可用性影响。

## 策略组

### 核心策略

| 策略 | 用途 |
| --- | --- |
| `节点选择` | 主要代理入口，供业务策略和最终兜底规则引用 |
| `自建节点` | 选择本地配置的节点；添加节点后需确认已加入该组 |
| `订阅节点` | 从配置或客户端添加的订阅中选择节点 |
| `自动选择` | Surge、Loon、Shadowrocket 配置了自动选优或测速；当前 Stash 和 Egern 文件中同名组是手动选择 |
| `兜底后备策略` | Loon、Stash、Shadowrocket 和 Egern 提供故障转移策略，具体候选节点以各文件为准 |
| `全球手动策略` | 部分客户端提供对订阅节点的手动选择 |

`DIRECT` 表示直连，不经过代理节点。选择“自建节点”后，还要在该组内部选定实际节点；如果它当前选中的是 `DIRECT`，流量仍会直连。

### 地区策略

| 地区 | 常见节点名称标识 |
| --- | --- |
| 香港 | 香港、Hong Kong、HK |
| 日本 | 日本、Japan、JP |
| 新加坡 | 新加坡、狮城、Singapore、SG |
| 美国 | 美国、United States、US |
| 德国 | 德国、Germany、DE |

地区组通过节点名称筛选，命名不符合筛选条件时可能为空。地区组与自建节点组的数据来源可能不同；没有单独的韩国、台湾或英国地区组，不代表这些地区的订阅节点会被排除在全球节点或自动策略之外。

### 业务策略

| 策略 | 用途 |
| --- | --- |
| `AI`、`Google` | AI 和 Google 相关服务 |
| `Telegram`、`X` | Telegram 及社交平台相关流量；`X` 也可能承接其他社交规则 |
| `TikTok`、`Netflix`、`国外媒体`、`Emby` | 分别控制对应服务或国外媒体流量 |
| `苹果服务`、`微软服务` | 苹果和微软相关服务，通常提供直连和代理选项 |
| `国内金融`、`国际支付`、`国际券商`、`数字资产` | 按业务分别选择出口；国际券商组仅在 Stash、Shadowrocket、Egern 中提供 |
| `PT站点`、`Speedtest` | 分别控制 PT 站点和测速服务 |

金融服务对出口地区或变化可能较敏感，请根据账户使用情况自行选择稳定的出口。规则集中的共享域名、IP 或第三方服务可能与其他业务重叠，具体以请求记录为准。

## 规则与 DNS

配置通常先处理个人定制和具体业务，再处理国内、通用代理和最终兜底规则。Loon 的规则来源优先级与其他客户端不同；各客户端也可能受到插件、模块或覆写的影响，实际顺序请以对应软件的规则列表为准。

- 未被其他规则命中的流量由最终策略处理，不一定直连。
- 国内应用规则设置为 `DIRECT`，但较早命中的规则或插件仍可能改变实际结果。
- 部分配置使用 Fake IP、真实 IP 例外或 DNS 劫持；不同客户端的设置并非逐项相同。
- 规则集来自远程仓库或第三方服务，会随上游更新；建议定期检查下载状态和匹配结果。

## 插件与证书

Loon 配置包含去广告及其他插件；插件的规则、脚本和复写可能影响请求处理。部分插件需要在客户端启用 MITM 并安装、信任客户端生成的证书，具体要求以插件说明为准。其他客户端不一定包含相同插件或功能。

不应分享 MITM 私钥、订阅链接或节点密码。变更节点或证书后，请在本地重新检查连接，不要把私人配置直接推送到公开仓库。

## 常见问题

**策略组里没有节点？** 检查订阅是否成功更新、节点名称是否符合地区筛选条件，以及自建节点是否已加入策略组。

**选择了节点，流量仍然直连？** 检查业务策略组当前选项、“节点选择”和“自建节点”的实际选择，以及请求是否先命中了 `DIRECT` 规则。

**配置或规则集更新失败？** 检查网络、订阅格式、远程地址和客户端版本；保留可用的本地配置以便回退。

## 规则来源与参考

- [blackmatrix7 / ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
- [wenjinliuu / Lane](https://github.com/wenjinliuu/Lane)
- [Repcz / EgernRules](https://github.com/Repcz/EgernRules)
- [Sub-Store](https://github.com/sub-store-org/Sub-Store)
- [Koolson / Qure](https://github.com/Koolson/Qure)、[Orz-3 / mini](https://github.com/Orz-3/mini)

具体来源以各配置中实际引用的地址为准，感谢规则与图标作者的维护。
