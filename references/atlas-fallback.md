# Atlas Fallback

仅当飞书控制台 UI 已确认卡住时再读本文件。

## Warning

- 这是开发者后台内部接口兜底，不是首选方案。
- 这些路径可能随飞书前端更新而变化。
- 先确认正常控制台路径无法完成，再使用。

## Verified Internal Endpoints

- 创建版本：
  - `/developers/v1/app_version/create/:clientId`
- 版本列表：
  - `/developers/v1/app_version/list/:clientId`
- 版本详情：
  - `/developers/v1/app_version/detail/:clientId/:versionId`
- 提交发布：
  - `/developers/v1/publish/commit/:clientId/:versionId`
- 查询事件配置：
  - `/developers/v1/event/:clientId`

## Minimal Create Payload

这个 payload 已验证可以创建一个新版本草稿：

```json
{
  "appVersion": "1.1.11",
  "mobileDefaultAbility": "bot",
  "pcDefaultAbility": "bot",
  "changeLog": "Enable message receive event.",
  "autoPublish": false
}
```

## Commit Payload

提交发布时可以直接用空对象：

```json
{}
```

## What To Verify Before Commit

- `/developers/v1/event/:clientId` 返回：
  - `eventMode: 4`
  - `events` 中包含 `im.message.receive_v1`
- 新创建版本确实出现在 `/developers/v1/app_version/list/:clientId`

## What To Verify After Commit

- 新版本在内部版本列表中状态变成已发布
- 飞书公开接口中的线上版本号发生变化
- 线上版本事件列表包含：
  - `im.message.receive_v1`
  - 可选：`im.chat.access_event.bot_p2p_chat_entered_v1`
