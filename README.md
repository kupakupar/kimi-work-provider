# Kimi Work 供应商

使用普通 Kimi 桌面版的 **Work 订阅**作为 Magpie 供应商。和「Kimi Agent」方向相反，也和 Kimi Code 供应商独立。

## 链接安装

在 Magpie 的插件安装框输入：

```text
github:kupakupar/kimi-work-provider
```

插件列表显示为 **Kimi Work**。本包通过 Git 安装，不是 npm 上的同名包；更新时继续使用上述入口。

安装后，在供应商中连接 **Kimi Work**，选择「使用本机 Kimi Work 登录」。需要本机 Kimi 桌面版已登录 Work。模型从官方 Work 网关自动读取；不读取 Magpie 的 Kimi Code API Key，也不回退到 Code API。

实际模型请求使用 `https://agent-gw.kimi.com/coding/v1`；会员用量来自 Kimi 会员接口。一次实测请求的消费明细分类是 `FEATURE_WORK`，Code 的 5 小时与周用量比例未变化。总会员额度按 Kimi 当前规则共享，这不代表免费或无限使用。

Magpie 仅保存本机账号引用；实际登录凭据仍留在 Kimi 自己的配置文件中，每次请求重新读取，因此能跟随桌面端刷新。不会主动消费刷新令牌、修改 Kimi 文件、伪造官方客户端身份，或切换正在使用的 Agent 模型。换账号后需要重新连接供应商，避免悄悄改用另一个账号。

默认使用标准上下文，未启用更高费用的 XL 上下文。Windows 已实测；macOS 路径已实现，实际 Work 推理尚未测试。桌面版内部配置变更时会停止并要求重新登录。

包内没有个人账号、API Key、令牌、提示词或对话。

## 同步与原有配置

Magpie 的加密同步会携带这个 Git 安装入口和供应商配置；缺少插件的设备可自动下载安装。各设备需要使用相同的同步账户与口令，并启用供应商同步。

供应商 ID 始终为 `kimi-work`，模型 ID 沿用 `kimi-work/k3-agent` 等原值。从本地文件夹迁移时，应先备份 Magpie 配置，安装此包，再用上述入口替换原插件条目，保留条目的选项、开关及供应商优先选择。不要同时启用本地版和链接版，也不要清除 `plugin-auth.json` 中的 `kimi-work` 登录记录；现有本机账号引用可以继续使用。

登录状态不通过同步传送。新设备需安装并登录自己的普通 Kimi 桌面版，再连接 Kimi Work 供应商；本插件按 Windows、macOS、Linux 的本机配置路径读取 Work 登录。原机器的实际凭据仍保留在 Kimi 配置中。Kimi Agent 的本地菜单补丁是单独功能，不包含在本包中。

代码使用桌面版内部接口，后续 Kimi 更新可能需要适配。macOS 路径已实现，尚未验证实际推理。
