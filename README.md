# ShiYi

面向 **Surge、Loon、Stash、Shadowrocket、Egern** 的本地分流模板。  
策略组与默认倾向对齐同一套设计；Stash / Shadowrocket / Egern 的规则分层来自 [Lane](https://github.com/wenjinliuu/Lane)，Surge / Loon 保留各自常用规则源。

本仓库**只提供分流模板**，不提供节点，不做订阅转换。导入后自行填写订阅地址。

## 下载配置

| 客户端       | 模板文件            | 地址                                                         |
| ------------ | ------------------- | ------------------------------------------------------------ |
| Surge        | `Surge.conf`        | https://raw.githubusercontent.com/wanxiao-wx/ShiYi/refs/heads/main/Surge.conf |
| Loon         | `Loon.conf`         | https://raw.githubusercontent.com/wanxiao-wx/ShiYi/refs/heads/main/Loon.conf |
| Stash        | `Stash.yaml`        | https://raw.githubusercontent.com/wanxiao-wx/ShiYi/refs/heads/main/Stash.yaml |
| Shadowrocket | `Shadowrocket.conf` | https://raw.githubusercontent.com/wanxiao-wx/ShiYi/refs/heads/main/Shadowrocket.conf |
| Egern        | `Egern.yaml`        | https://raw.githubusercontent.com/wanxiao-wx/ShiYi/refs/heads/main/Egern.yaml |

页面浏览也可使用：

- [Surge.conf](https://github.com/wanxiao-wx/ShiYi/blob/main/Surge.conf)
- [Loon.conf](https://github.com/wanxiao-wx/ShiYi/blob/main/Loon.conf)
- [Stash.yaml](https://github.com/wanxiao-wx/ShiYi/blob/main/Stash.yaml)
- [Shadowrocket.conf](https://github.com/wanxiao-wx/ShiYi/blob/main/Shadowrocket.conf)
- [Egern.yaml](https://github.com/wanxiao-wx/ShiYi/blob/main/Egern.yaml)

导入前请保存为**本地配置**。不要把已经填入私人订阅或自建节点的配置推到公开仓库。

## 首次使用

1. 打开上表中对应客户端的配置地址，下载或复制原始链接。
2. 按下表添加自己的节点订阅。`https://YOUR_SUBSCRIPTION_URL` 只是占位，不是有效地址。
3. 保存并启用本地配置，再开启节点订阅和远程规则的自动更新。

| 客户端       | 节点订阅位置                                 |
| ------------ | -------------------------------------------- |
| Surge        | `[Proxy Group]` → `节点订阅` → `policy-path` |
| Loon         | `[Remote Proxy]` → `订阅`                    |
| Stash        | `proxy-providers` → `订阅` → `url`           |
| Egern        | `我的节点` → `urls`                          |
| Shadowrocket | 在 App「订阅」中添加，配置文件不写订阅 URL   |

不同客户端支持的订阅格式并不完全相同，同一条订阅链接不保证五端通用。自建节点请写在各端的 `[Proxy]` / `proxies` 中，不要提交到公开仓库。

## 主要功能

- **地区策略**：美国、日本、香港、台湾、新加坡、韩国、英国、德国。Stash / Shadowrocket / Egern 提供 Auto 与 Manual；Surge / Loon 按节点名过滤到对应地区组。
- **服务策略**：AI、国外媒体 / YouTube / Streaming、TikTok、Emby、Gaming、Telegram、X / Social、Google、微软 / Microsoft、苹果 / Apple、金融服务 / Brokerage、Crypto、Developer、Final / 节点选择。
- **默认倾向**：Apple、Microsoft、Brokerage 默认直连；Telegram、Social 默认走代理入口；其余服务组默认跟随基础入口，可改 DIRECT 或某地区。
- **中国分流**：局域网与已知国内域名优先直连，再以中国 IP / GeoIP 兜底；已知境外域名在 IP 判断之前进入代理入口，避免被后续 GEOIP 误伤。
- **专项规则**：富途 / Moomoo、老虎、长桥、嘉信进入 Brokerage；Binance、OKX、Bybit、Bitget 进入 Crypto（Lane 规则端）。
- **不做的事**：模板不内置落地线路组、不打包 MitM 证书、不收集订阅。

各端基础入口因客户端能力不同，会有少量差异：

| 客户端        | 基础代理入口                                                 |
| ------------- | ------------------------------------------------------------ |
| Surge         | `节点选择`：自动选择 / 自建 / 订阅 / 地区 / DIRECT           |
| Loon          | `节点选择`：url-test 自动选择、fallback 兜底、订阅筛选、地区手动 |
| Stash / Egern | `Proxy` 先进入自动选择与「我的节点」，再选地区 Auto / Manual |
| Shadowrocket  | 使用 App 内置 `PROXY`（首页当前节点），不另建同名基础组      |

## 与 Lane 的关系

Stash、Shadowrocket、Egern 的远程规则清单与分层顺序沿用 Lane。  
本模板在此之上做了这些取舍：

- 增加韩 / 英 / 德地区组
- 去掉按机场落地名拆分的 Smart / 落地组
- 不绑定任何机场订阅或自建节点
- 保留个人高频域名（时间同步、Emby 子域、Apple Relay、Grok、支付等）作为最高优先级本地规则

规则数据仍由 Lane 上游更新；主配置只在策略组或规则顺序变化时才需要整份替换。

## 更新说明

节点列表和远程规则集可独立更新，不必频繁替换本地主配置。  
只有策略组成员、默认倾向、DNS 或规则顺序变化时，才重新下载模板，并再次填入订阅与个人修改。

## 安全

- 公开仓库只放未填写订阅的占位模板。
- 填好订阅或节点后的文件视为私密配置。
- 证书、PSK、订阅 token 不要写进 README 或 Issue。
