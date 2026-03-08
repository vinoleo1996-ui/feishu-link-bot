# Publish Checklist

## Documentation First

- OpenClaw 官方飞书通道文档
- 飞书官方文档：
  - 自建应用
  - 机器人能力
  - 事件订阅
  - 长连接
  - 版本发布

## Local Checklist

- 本地有可用的 `App ID`
- 本地有可用的 `App Secret`
- `openclaw gateway health` 返回 `Feishu: ok`
- `openclaw channels status --probe --json` 里：
  - `configured: true`
  - `running: true`
  - `probe.ok: true`

## Feishu App Checklist

- 应用是自建应用
- 已启用机器人能力
- 订阅方式为长连接
- 事件包含：
  - `im.message.receive_v1`
- 可选事件：
  - `im.chat.access_event.bot_p2p_chat_entered_v1`
- 已发布线上版本，而不是仅有草稿变更

## End-To-End Done Criteria

- 公开接口能看到新的 `online_version_id`
- 公开接口能看到线上版本的 `event_infos`
- 本地探活正常
- 飞书私聊或群 `@` 有真实回复

## Fast Diagnosis

- 本地探活正常，但飞书无响应：
  - 先查线上版本是否真的带了事件
- 草稿里能看到事件，但线上版本没事件：
  - 问题在发布，不在本地配置
- 控制台创建版本页红字很多、保存灰掉：
  - 不要先重配本地
  - 先确认是否只是历史权限污染导致 UI 难用
