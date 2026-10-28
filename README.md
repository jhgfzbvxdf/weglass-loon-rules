# 微信输入法（WeType）隐私规则 · Loon

macOS 版微信输入法的上报域名清单与 Loon 拦截规则。

## 审计来源

全部来自本机实测（2026-10-29，WeType 3.0.0 build 670）：

| 项目 | 发现 |
|---|---|
| 上报 SDK | Sentry、Bugly（腾讯）、Flurry、Mars |
| 上报事件 | 38 项，其中 9 项为内容上报（输入/语音/翻译/常用语/删除），采样率 1/10 |
| 实连目标 | 220.196.155.66:443（腾讯云 CDN 边缘节点） |
| 日志上传 | 崩溃时上传 `~/Library/Caches/WeType/Logs/` |
| 本地模式 | `localModeEnabled = 0`（未开启） |

## 使用

把 `weglass-loon-rules.conf` 的内容并入 Loon 配置。

## 重要提醒

1. **不要封 `wetype.wxqcloud.qq.com`** —— 主 API 与词典都走这个域名
2. 主 API 与上报共用域名时，域名规则无法只封上报；这种情况请改用输入法设置里的「本地模式」
3. 规则按域名匹配，不依赖 App 版本，升级后依然有效
