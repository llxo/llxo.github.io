+++
title = 'tg高速下载'
date = 2025-07-23T18:15:41+08:00
draft = false
+++

天下苦tg限速久已,今天分享一种可以高速(20mb/s)下载telegram文件的工具


### 预览

![alt text](https://i.mji.rip/2025/07/23/24465055e9d19edb2a180e03524fd2ce.png)

转发到bot即可下载

### 快速开始

感谢开源仓库[saveany-bot](https://github.com/krau/SaveAny-Bot)

首先下载[saveany-bot](https://github.com/krau/SaveAny-Bot/releases)的windows压缩包.

#### 配置文件

在解压后的目录新建`config.toml`文件,填入Bot Token和用户id,proxy端口改成自己的

```
workers = 4 # 同时下载文件数
retry = 3   # 下载失败重试次数
threads = 4 # 单个任务下载最大线程数
stream = false

[telegram]
# Bot Token
# 更换 Bot Token 后请删除数据库文件和 session.db
token = ""
# Telegram API 配置, 若不配置也可运行, 将使用默认的 API ID 和 API HASH
# 推荐使用自己的 API ID 和 API HASH (https://my.telegram.org)
app_id = 
app_hash = ""

[telegram.proxy]
# 启用代理连接 telegram, 只支持 socks5
enable = true
url = "socks5://127.0.0.1:7897"

[[storages]]
name = "本地存储"
type = "local"
enable = true
# 以下是 local 类型存储的自定义配置
base_path = "./saveany"

# 用户列表
[[users]]
# telegram user id
id = 
# 开启黑名单，开启后下方留空以使用所有存储，反之则为白名单，白名单请在下方输入允许的存储名
blacklist = true
# 将列表留空并开启黑名单模式以允许使用所有存储，此处示例为黑名单模式，用户114514 可使用所有存储
storages = []

[temp]
base_path = 'cache/'
cache_ttl = 3600
```

#### cmd启动应用

根目录运行`saveany-bot.exe`

### 开机自启
根目录新建`saveany.vbs`
```
Set oShell = CreateObject("WScript.Shell")
Set oFSO = CreateObject("Scripting.FileSystemObject")

scriptPath = WScript.ScriptFullName
scriptDir = oFSO.GetParentFolderName(scriptPath)

executablePath = Chr(34) & scriptDir & "\saveany-bot.exe" & Chr(34)

oShell.Run executablePath, 0, False

Set oFSO = Nothing
Set oShell = Nothing
```
创建快捷方式到启动目录(win+r输入`shell:startup`)
