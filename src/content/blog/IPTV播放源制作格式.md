---
title: 'IPTV播放源制作格式'
description: 'IPTV直播源有两种播放文件格式——m3u & txt，分别可以在pc、手机和智能电视的播放软件上本地或在线加载播放'
pubDate: 'Mar 24 2025'
heroImage: 'https://gh-proxy.com/https://github.com/RaycornM/person-picture-bed/blob/main/img/image-17-1024x550.png'
---

![image-17.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEDWtpo7O0H0QbRJJ-Pl5h1ZSZp0AP2UQACFiEAAiy-aVdQyuKo8Qi8UzYE.png)

IPTV直播源有两种播放文件格式——m3u & txt，分别可以在pc、手机和智能电视的播放软件上本地或在线加载播放，m3u文件支持在potplayer、zyfun、Kodi、emby等软件打开，txt文件本人目前只知道tvbox使用这种格式，其他软件有待补充。

想要自己制作直播源需要有单独频道的直播地址，需要一定的搜索能力，或者有其他格式的直播源也可以自己转换成需要的格式；

### 新建文本文档

文件第一行开头，txt格式不需要

- ###### m3u

```
#EXTM3U
```

如果想为频道分类的话接下来在下一行添加分类标题：

- ###### m3u
- ###### txt

```
#央视频道
```

```
央视频道,#genre#
```

添加频道：

- ###### m3u
- ###### txt

```
#EXTINF:-1 tvg-name="CCTV1" tvg-logo="https://live.fanmingming.com/tv/CCTV1.png" group-title="央视频道",CCTV-1 综合
http://ottrrs.hl.chinamobile.com/PLTV/88888888/224/3221226559/index.m3u8
```

```
CCTV-1 综合,http://ottrrs.hl.chinamobile.com/PLTV/88888888/224/3221226559/index.m3u8
```

m3u格式：tvg-logo是该频道对应logo的路径链接，group-title是该频道的分类，CCTV-1是这个源的名称，接着的链接就是直播链接；

txt格式：txt比较简单，直接直播源名称跟着直播链接就可以

剩下的频道按照上面的格式就可以继续添加了；最后文件保存为m3u或者txt格式，就可以扔到播放器或者tvbox中播放了。

### 部分找源网址：

- [https://iptv-org.github.io/](https://iptv-org.github.io/)
- [https://tonkiang.us/](https://tonkiang.us/)
- [https://epg.pw/](https://epg.pw/)
- [https://aktv.space/](https://aktv.space/)
- [http://www.guangbomi.com/tv](http://www.guangbomi.com/tv)
- [https://www.chaojidianshi.net/gangtaizhibo/](https://www.chaojidianshi.net/gangtaizhibo/)
- [https://iptv.hacks.tools/#google_vignette](https://iptv.hacks.tools/#google_vignette)

### 在线检测m3u8工具：

[Free HLS Player - Tencent EdgeOne](https://edgeone.ai/tools/hls-player)

### 在线直播源转换工具：

[https://guihet.com/tvlistconvert.html](https://guihet.com/tvlistconvert.html)

### 个人直播源仓库：

[RaycornM/TVbox-IPTV: 自用影视源直播源配置仓库 随缘维护](https://github.com/RaycornM/TVbox-IPTV)

## 订阅链接：

### m3u直播源：

[https://raw.githubusercontent.com/RaycornM/TVbox-IPTV/main/Tivi.m3u](https://raw.githubusercontent.com/RaycornM/TVbox-IPTV/main/Tivi.m3u)

## txt直播源：

[https://raw.githubusercontent.com/RaycornM/TVbox-IPTV/main/Tivi.txt](https://raw.githubusercontent.com/RaycornM/TVbox-IPTV/main/Tivi.txt)
