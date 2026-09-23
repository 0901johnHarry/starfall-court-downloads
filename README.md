# 星陨王庭 · Windows 下载包

源码：[starfall-court](https://github.com/0901johnHarry/starfall-court)。本仓库存放可直接下载的 Windows 运行文件和 3D 模型；[前往 Release 下载](https://github.com/0901johnHarry/starfall-court-downloads/releases/tag/v2026.09.24)。服务端监听 **3000** 端口。

| 附件 | 用途 | 大小 |
| --- | --- | ---: |
| `starfall-runtime-windows-20260924.zip` | Unity 大屏程序、卡牌和系统语音、预览图；先下载这个 | 813 MB |
| `starfall-browser-models-20260924.zip` | 网页 3D 预览使用的 GLB | 779 MB |
| `starfall-model-source-20260924.zip` | 31 个原始 GLB 和清单，用于 Unity 重新导入与后续编辑 | 1.24 GB |

在另一台 Windows 电脑安装 Git、Java 21、Maven，然后执行：

```powershell
git clone https://github.com/0901johnHarry/starfall-court.git
cd starfall-court
Expand-Archive -LiteralPath '下载目录\starfall-runtime-windows-20260924.zip' -DestinationPath . -Force
# 需要网页模型时再解压 browser-models 包；需要 Unity 源模型时再解压 model-source 包
$env:STARFALL_ADMIN_PASSWORD = '请设置自己的管理员密码'
$env:STARFALL_DISPLAY_TOKEN = '请设置自己的大屏令牌'
mvn -s settings.xml spring-boot:run
```

打开 `http://localhost:3000` 登录管理台，创建对局。Unity 大屏程序位于 `data\build-windows\StarfallCourt.exe`，在启动界面输入服务地址、对局 ID 和刚设置的大屏令牌。如果要重建 Unity 模型，先解压源模型包，执行 `python scripts/sync_unity_models.py`，再用 Unity Hub 打开 `unity/`。

这三个公开包不含本机玩家数据库、设备令牌、API 密钥、分析录音或备份；另一台电脑启动时会新建数据库。已存在的玩家和实体卡 UID 分配若要保留，需要私下迁移数据库，**不要提交到公开仓库**。各附件的 SHA-256 值见 Release 同名 `.sha256` 文件。

第三方模型的原作者仍保留其权利；这里的公开下载不改变各素材原有的许可。模型清单在源码仓库的 `assets/models/catalog.json`，进一步传播或修改时应保留相应署名和授权条件。
