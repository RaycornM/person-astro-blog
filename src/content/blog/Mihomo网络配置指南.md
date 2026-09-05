---
title: 'Mihomo网络配置指南'
description: '使用 Docker 在nas部署Mihomo (原 Clash.Meta)容器，并配置其他容器优雅、安全地通过它进行代理上网。'
pubDate: 'Sep 04 2026'
tags: [网络, 自托管, 工具, NAS]
heroImage: 'https://gh-proxy.org/https://raw.githubusercontent.com/RaycornM/person-picture-bed/main/img/20260905172016173.png'
---

### 简介与架构设计

在绿联 NAS (UGOS / UGOS Pro) 中，我们常常会部署许多需要连接外网的容器服务（例如：qBittorrent、Jackett、Radarr、Sonarr 或各类自动化同步/下载工具）。由于网络环境限制，这些容器可能需要通过代理才能正常拉取元数据或进行网络通信。

本指南将介绍如何使用 Docker 部署 **Mihomo (原 Clash.Meta)** 容器，并配置其他容器优雅、安全地通过它进行代理上网。

### 前置准备（获取并上传✈️配置文件）

在运行 Docker 容器之前，**必须**准备好配置文件。如果直接运行，Docker 会因为找不到挂载路径而自动在宿主机创建同名**文件夹**，导致容器报错无法启动。

准备配置文件有两种方法：

#### 1. 编写 mihomo 配置文件

新建一个空文件夹命名为 `mihomo`，在其中新建文本文档 `config.yaml`

可参考下方模板来创建您自己的配置文件，模板参考自官方文档，如果你希望了解配置文件的具体规则，同样请参考官方文档。（本文最后有链接）

该模板中**必须要修改**的是第 19、20 行与 25 行，根据实际情况进行填写，修改模板后不含模板中的尖括号。其中节点提供者名称可自由填写，用于程序区分多个订阅；节点名称前缀会在显示节点信息时插入到原始节点名称前，便于自己区分不同订阅的节点。

第 1 行为代理端口设置，第 6 行为外部控制端口设置（如使用 webUI 控制 mihomo）如有需要可自行更改。

```plaintext
mixed-port: 7890
allow-lan: true
bind-address: '*'
mode: rule
log-level: info
external-controller: '0.0.0.0:9090'

tun:
  enable: false
  stack: mixed
  dns-hijack:
    - "any:53"
    - "tcp://any:53"
  auto-route: true
  auto-redirect: true
  auto-detect-interface: true

proxy-providers:
  <节点提供者名称>:
    url: "<节点订阅链接>"
    type: http
    interval: 86400
    health-check: {enable: true,url: "https://www.gstatic.com/generate_204", interval: 300}
    override:
      additional-prefix: "<节点名称前缀>"

proxies: 
  - name: "直连"
    type: direct
    udp: true

geodata-mode: true
geox-url:
  geoip: "https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/geoip.dat"
  geosite: "https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/geosite.dat"
  mmdb: "https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/country-lite.mmdb"
  asn: "https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/GeoLite2-ASN.mmdb"

dns:
  enable: true
  ipv6: true
  respect-rules: true
  enhanced-mode: fake-ip
  fake-ip-filter:
    - "*"
    - "+.lan"
    - "+.local"
    - "+.market.xiaomi.com"
  nameserver:
    - https://120.53.53.53/dns-query
    - https://223.5.5.5/dns-query
  proxy-server-nameserver:
    - https://120.53.53.53/dns-query
    - https://223.5.5.5/dns-query
  nameserver-policy:
    "geosite:cn,private":
      - https://120.53.53.53/dns-query
      - https://223.5.5.5/dns-query
    "geosite:geolocation-!cn":
      - "https://dns.cloudflare.com/dns-query"
      - "https://dns.google/dns-query"

proxy-groups:

  - name: 默认
    type: select
    proxies: [自动选择,直连,香港,台湾,日本,新加坡,美国,其它地区,全部节点]

  - name: Google
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: Telegram
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: Twitter
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: 哔哩哔哩
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: 巴哈姆特
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: YouTube
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: 海外AI
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: NETFLIX
    type: select
    proxies: [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: Spotify
    type: select
    proxies:  [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: Github
    type: select
    proxies:  [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  - name: 国内
    type: select
    proxies:  [直连,默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择]

  - name: 其他
    type: select
    proxies:  [默认,香港,台湾,日本,新加坡,美国,其它地区,全部节点,自动选择,直连]

  #分隔,下面是地区分组
  - name: 香港
    type: select
    include-all: true
    filter: "(?i)港|hk|hongkong|hong kong"

  - name: 台湾
    type: select
    include-all: true
    filter: "(?i)台|tw|taiwan"

  - name: 日本
    type: select
    include-all: true
    filter: "(?i)日|jp|japan"

  - name: 美国
    type: select
    include-all: true
    filter: "(?i)美|us|unitedstates|united states"

  - name: 新加坡
    type: select
    include-all: true
    filter: "(?i)(新|sg|singapore)"

  - name: 其它地区
    type: select
    include-all: true
    filter: "(?i)^(?!.*(?:🇭🇰|🇯🇵|🇺🇸|🇸🇬|🇨🇳|港|hk|hongkong|台|tw|taiwan|日|jp|japan|新|sg|singapore|美|us|unitedstates)).*"

  - name: 全部节点
    type: select
    include-all: true

  - name: 自动选择
    type: url-test
    include-all: true
    tolerance: 10

rules:
  - GEOIP,lan,直连,no-resolve
  - GEOSITE,twitter,Twitter
  - GEOSITE,youtube,YouTube
  - GEOSITE,category-ai-!cn,海外AI
  - GEOSITE,github,Github
  - GEOSITE,google,Google
  - GEOSITE,telegram,Telegram
  - GEOSITE,netflix,NETFLIX
  - GEOSITE,bilibili,哔哩哔哩
  - GEOSITE,bahamut,巴哈姆特
  - GEOSITE,spotify,Spotify
  - GEOSITE,CN,国内
  - GEOSITE,geolocation-!cn,其他

  - GEOIP,CN,国内
  - MATCH,其他
```

#### 2. 使用✈️提供的 Clash 配置文件

1. **确定挂载路径**：在绿联云客户端的 **文件管理器** 中，进入默认的 docker 共享文件夹，在里面新建一个名为 clash 的文件夹。_（也可直接放到mihomo部署的文件夹内，后续在compose命令修改路径即可，本文默认另外创建clash文件夹存储配置文件，使用路径映射到mihomo部署文件夹）_

> ***💡 提示（如何获取绝对路径）***_：右键点击新建的 clash 文件夹选择 _***属性***_，即可看到其绝对路径（通常为 /volume1/docker/clash 或 /volume2/docker/clash，本指南以 /volume1/docker/clash 为例）。_

2. **下载✈️配置文件**：

登录您的✈️后台，找到 **Clash 订阅链接** 并复制。

在电脑浏览器中新建标签页，将订阅链接粘贴进地址栏并按下回车，浏览器会自动下载一个 .yaml 或 .clash 后缀的配置文件。

将该文件重命名为 **config.yaml**。

3. **上传并添加 NAS 专用参数**：

将改名后的 config.yaml 通过绿联文件管理器上传到 /volume1/docker/clash 目录下。

双击打开该文件进行编辑（或用电脑的文本编辑器修改后重新上传），**在文件的最顶部（第一行开始）**，插入以下绿联 NAS 专用网络配置参数：

```plaintext
# ================= 绿联 NAS 专用配置项 (可确保是否重复后放在文件最顶部或自行修改) =================
port: 7890
socks-port: 7891
mixed-port: 7892             # 混合代理端口，用于其他容器连接
allow-lan: true              # 必须设为 true 以允许局域网内其他设备连接
bind-address: '*'            # 监听所有网卡接口
external-controller: ':9090' # 外部控制面板 API 端口（开放 9090）
# secret: 'YourSecureSecret'   # 你的控制面板连接密钥（建议修改配置或直接留空）

# 本地局域网 .local 解析与 DNS 配置
hosts:
  '<your_nas_name>.local': host.docker.internal
  'time.facebook.com': 17.253.84.125
  'time.android.com': 17.253.84.125

dns:
  enable: true
  listen: :1053
  enhanced-mode: fake-ip
  fake-ip-filter:
    - "*.local"
    - "localhost"
    - "+.lan"
  nameserver:
    - 223.5.5.5
    - 119.29.29.29
# ===========================================================================
```

> ***⚠️ 注意***_：请检查插入代码下方是否存有重复的 port:、mixed-port:、allow-lan: 或 dns: 配置项。如果有，请将下方✈️自带的重复项删掉，避免格式冲突。_

### **使用 docker compose 构建容器**

在绿联云桌面端打开 **容器 (Docker)** 应用：

- 在 **项目** (Compose) 菜单中新建项目，粘贴并运行以下配置（直接将代理核心和 Metacubexd 控制面板一键拉起）：

```plaintext
services:
  mihomo:
    image: metacubex/mihomo:latest
    container_name: mihomo
    restart: always
    network_mode: host
    ports:
      - "7890:7890"  # HTTP 代理端口
      - "7891:7891"  # SOCKS5 代理端口
      - "7892:7892"  # 混合代理端口（推荐其他应用填这个最稳）
      - "9090:9090"  # 外部控制面板 API 端口
    volumes:
      - /volume1/docker/clash:/root/.config/mihomo #配置文件映射
    # extra_hosts 是选填的。仅在使用虚拟域名 host.docker.internal 时才需要开启
    # extra_hosts:
    #   - "host.docker.internal:host-gateway"

  metacubexd:
    image: ghcr.io/metacubex/metacubexd:latest  # 从 GitHub Registry 拉取面板
    container_name: metacubexd
    restart: always
    ports:
      - "18091:80"  # 浏览器访问 http://NAS_IP:18091 来管理代理，可自行修改
```

> ***⚠️ 注意***_：mihomo的网络模式一定要是host，不能是bridge。_
>
> _使用bridge模式时会容易出现在mihomo的Webui界面点击添加连接后端时报错 _`Failed to fetch`_的情况，而host不会。_<span style="color: rgb(28, 31, 35)"><em>host 模式下容器直接共享 NAS 网络栈 9090 不用经过任何端口映射，直接就在 NAS 上监听，不会出现端口接不上的情况。</em></span>

### **访问并使用控制面板 (Web UI)**

在局域网内任意设备浏览器中输入 `设备IP:18091` 即可访问 metacubexd 的界面，后端地址填写 `http://设备IP:9090` ，密钥留空即可，如图所示，点击添加便可管理 mihomo 的各项配置。若在前文中修改了 webUI 访问端口和外部控制端口，请自行替换为自己设置的端口号。

![](https://gh-proxy.org/https://raw.githubusercontent.com/RaycornM/person-picture-bed/main/img/20260905172016173.png)

> _如果你使用 metacubexd 更改了一些设置，那将只会在 mihomo 的本次运行生效，重启 mihomo 会将所有设置重置为你第一步在 config.yaml 中所填写的配置_

**至此已搭建完成，在需要使用网络代理的地方（具体见 常见问题）在代理选项内填入 **`设备IP:7890`** 或**`设备IP:7891`** 或**`设备IP:7892`** （根据实际情况填写）即可使用，如：**

```plaintext
容器支持 HTTP 代理 → http://设备ip:7890
必须 SOCKS5 → socks5://设备ip:7891
或者省事用混合端口 → socks5://设备ip:7893
```

### metacubexd 中一些基本的说明

#### 模板文件的分流规则逻辑

如果是使用上方提供的配置模板，那么 metacubexd 的**代理**页面应该有默认、Google、GLOBAL等分组，这些分组被称为**代理组**，你可以指定各个代理组使用哪个节点。

在 metacubexd 的**配置**页面中的运行模式里，分别有规则、直连、全局几个选项。若使用全局，则所有经过 mihomo 的流量均会通过 **GLOBAL代理组** 内指定的节点转发；若使用规则，则会按配置文件中的规则进行分流，下方会介绍模板文件中的规则逻辑；

**提供的模板文件中**的规则为：当访问一个地址时会优先查询是否**属于代理组中已经指定的网站**，比如 Google，这类网站会直接走你在对应代理组中指定的节点。代理组可以套娃，你如果打开 Google 代理组会注意到里面并不让你选择具体的节点，而是选择其他代理组，则这时会再到对应的代理组中使用你指定的节点。

举例：Google 代理组中指定了“香港”这个代理组，而香港代理组中指定了“香港01”这个节点，那么当访问 Google 时，流量会通过“香港01”这个节点转发。

若访问的网站**不属于**代理组中指定的网站，则会使用“默认”代理组中指定的节点，同样可以套娃。

#### TUN 模式

TUN 模式即虚拟网卡模式，启用该模式会另 mihomo 接管本设备的所有流量，如有需要可在 metacubexd 的**配置**页面启用，如果希望启动 mihomo 时自动打开 TUN 模式，可以将模板配置文件中第 9 行的 false 改为 true。

### 常见问题

1. “在需要使用网络代理的地方填入”是指填入哪

包括但不限于：各系统的系统代理（如 Windows 设置中的代理设置，手机 WiFi 的代理设置）、Linux 中环境变量的 http\_proxy 等代理字段、各软件内部的代理设置等。

- 对于 **系统代理**，以 Windows 举例，并非所有软件都会走系统代理，这种时候你需要查看应用内是否能设置代理；若没有相关选项且应用本身不走系统代理则你需要考虑其他方法让 mihomo 来接管流量，不过这些就不在这篇教程的范畴内了。
- 如果你希望 mihomo 接管 **docker 宿主设备本身** 的所有流量，可以参考教程启用 **TUN 模式**

2. 使用了其他地方寻找的 config.yaml 模板，最后一步点击添加连接后端时报错 `Failed to fetch`

检查 `config.yaml` 内的 `external-controller` 字段，连接后端时以填入该处指定的端口

3. 使用了文章的 config.yaml 模板，依然出现上一个问题

检查是否将 **mihomo 容器**的网络模式更改为 **host**

4. mihomo容器部署异常，不断重启

查看容器日志，若报错内容有
`msg="can't initial GeoIP: can't download MMDB: Get \"https://github.com/MetaCubeX/meta-rules-dat/releases/download/latest/geoip.metadb\": dns resolve failed: couldn't find ip"`

等内容，在配置文件最后添加：

```plaintext
# 使用dat格式数据库，不再依赖mmdb自动下载
geodata-mode: true
# 关闭自动更新geo库，避免每次启动联网超时
geo-auto-update: false
# 自定义国内CDN地址（备用，开启更新时生效）
geox-url:
  geoip: "https://cdn.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geoip.dat"
  geosite: "https://cdn.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geosite.dat"
  mmdb: "https://cdn.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/country.mmdb"
```

可解决网络问题导致geo库无法正常下载的问题
