# mpv-Lite 精简版说明

基于 [mpv-Yaozhi 1.0.2](https://github.com/Yaozhil/mpv-Yaozhi) （mpv v0.41.0 自编译内核）精简而来的本地播放版本。
- 原作者：Yaozhil 

说明：年龄大了，不喜欢太多的冗余的功能，所以做了一个精简版回归播放器本质，作为养老版本使用，不再折腾了。
想体验完整版功能，可以去原作者项目页，下载使用。

去掉在线播放生态、AI/实验功能、等多余的内容，保留完整的本地播放、画质、字幕、网盘与界面体验。

所有修改基于 mpv-Yaozhi 1.0.2 本地文件修改。
在Releases 下载打包的 portable即可使用。

---

## 一、体积变化

|名称                   | 体积 |
|---|---|
| 原版 mpv-Yaozhi 1.0.2 | 约 900 MB |
| mpv-Lite 精简后       | 约 270 MB |
| **缩减**              | **约 630 MB（70%）** |

主要体积来源的变化：

| 组件                                   | 原版 | mpv-Lite |
|---|---|---|
| online-media/（Python 运行时 + 解析脚本） | 188 MB | 已删除 |
| experimental/omniphony（Atmos 实验引擎） | 143 MB | 已删除 |
| jre/ + libbluray jar（蓝光 BD-J 菜单）   | 146 MB | 已删除 |
| experimental/video-enhancement（RIFE 补帧模型） | 49 MB | 已删除 |
| atmos-components（Atmos 组件）          | 109 MB | 已删除 |
| shaders/（画质着色器）                   | 21 MB   | 保留 |
| mpv.exe + fonts/ + 其他配置             | 约 250 MB | 保留 |

---

## 二、删减的功能

### 大型模块
- **在线媒体播放**：YouTube / B站 / 抖音在线解析与播放（online-media 运行时、online-media.lua、平台路由模块）
- **蓝光原盘 BD-J 动态菜单**（jre、libbluray jar、disc-menu.lua）；蓝光/UHD 标题列表菜单（bluray-titles-menu.lua）
- **Dolby Atmos 实验模式**（omniphony 渲染引擎、mpv-Atmos.exe 启动器、yaozhi-atmos-mode.lua）
- **RIFE AI 补帧**（rife-ncnn-vulkan 模型、vs/ 脚本、ai-interpolation.lua）；"超分与补帧"整套菜单

### 在线与账号
- B站扫码登录（bilibili-account.lua）、YouTube Cookie 登录（youtube-account.lua）
- SponsorBlock 赞助片段自动跳过（sponsorblock_minimal.lua）

### 字幕工具
- AI 语音识别生成字幕（sub-fastwhisper.lua）
- 字幕导出（sub_export.lua，ALT+m）

### 视频剪辑类
- 无损片段剪切（slicing_copy.lua，c/a/CTRL+C）
- GIF/webp 动图导出（mpv-animated.lua，w/W/CTRL+w/CTRL+W）
- 台词长截图（mpv-cropscreen.lua）

### 光盘与 ISO
- ISO 自动播放入口（auto_iso_loader.lua）——打开 ISO 回退到 mpv 原生加载，可正常播放
- 以上蓝光菜单相关全部功能

### 杂项
- 赞赏卡片（yaozhi-donation.lua 及素材目录）、关于页（yaozhi-home.lua 及素材目录）
- 更新检查模块（yaozhi-release.lua）
- 清理了 input.conf 中所有指向已删功能的菜单项和按键绑定（约 20 条）
- 起播格式角标、HDR 识别等显示 "Dolby Atmos / TrueHD" 等片源格式的功能不受影响

---

## 四、保留的功能

### 界面与基础
- **uosc 界面**：控件带、右键菜单、菜单系统；进度条悬停缩略图（thumbfast）
- 文件浏览器（file-browser，含网盘浏览）、打开文件/文件夹/URL 对话框（open_dialog）
- 快捷键可视化管理（keybinding-manager）、按键循环命令、属性监听
- 自动连播同目录（autoload）、垃圾文件过滤、STRM 兼容、剧集间记住音轨/字幕选择、智能选轨
- 播放列表管理、最近播放、历史记录、历史续播、进度书签
- seek 撤销/重做、长按快进（B站风格）、三态窗口置顶、画中画、自动全屏、最小化暂停、音乐模式
- 删除当前文件、截图到桌面、统计信息页（自定义版 stats.lua）
- 起播格式角标（HDR/DV/Atmos 等片源格式识别显示）、空闲启动界面、启动窗口时序

### 画质与音频
- **自适应画质**（adaptive-quality：按 GPU 分级自动调整，无着色器时自动降级为内置算法）
- 自动去黑边（dynamic-crop）、HDR 显示器模式自动切换（hdr-mode，Windows 10+）
- 音频源码输出切换（audio-passthrough）、PGS 图形字幕亮度自适应
- 音量均衡/响度标准化滤镜、去色块/旋转/翻转/帧率等视频滤镜
- HDR→SDR 映射、ICC 校色、杜比视界/HDR10+ 片源正常播放（走 mpv 原生映射）
- **画质着色器**（shaders/ 全部：Anime4K、Ani4K、AnimeJaNai、FSRCNNX、SSim、ravu、nnedi3 等）；mpv.conf 中对应的着色器配置组

### 网盘（Alist/WebDAV）
- WebDAV 网盘快捷访问（webdav_shortcut.lua）、Alist 挂载盘速度显示
- 网盘签名 URL 的 TLS 修复（network-backend.lua）

### 弹幕
- uosc_danmaku：本地/在线视频弹幕加载与发送（B站直播弹幕等脚本保留）

### 字幕（保留部分）
- 字幕下载菜单（射手网 sub-assrt）
- 字幕时间轴自动校正（autosubsync + alass.exe）
- 字幕内容选择菜单、视频旁 Fonts 目录自动识别
- 跳过 OP/ED（chapterskip）、片头片尾片段跳过（skip-segments）
- 完整的字幕样式/兼容性/位置/延迟调整菜单

### 光盘播放（保留部分）
- 蓝光/DVD 光盘导航按键（mpv 内置 discnav，方向键/回车操作菜单）
- 直接播放蓝光/DVD 目录和 ISO 正片（原生加载）

---

## 五、技术性说明

1. **ytdl_hook 空转**：mpv.conf 中 `ytdl=no` 且路由脚本已删，内置桥接脚本无副作用地保留。
2. **adaptive-quality 休眠状态机**：RIFE 时钟保护逻辑（约百行）与正常画质管理交织，因触发属性永不置位而永久休眠，保留不动。
3. **uosc 死代码已清**：超分补帧菜单、Atmos 注入、赞赏置顶、在线画质切换等约 300 行死分支已从 uosc 源码移除，所有改动文件通过 luajit 语法校验。
4. **原始版本**：原始 mpv-Yaozhi 1.0.2 可从原作者：Yaozhil的 GitHub 项目发布页获取。

- 本修改版遵循原项目许可证（请以原仓库 LICENSE 为准）。
(https://github.com/Yaozhil/mpv-Yaozhi)
- 原作者：Yaozhil 