# FF14 编舞时间轴 — 共享动作库

这个仓库存放 [FF14 编舞时间轴工具](https://47d057355e6242028b9b0caaa21afee0.app.workbuddy.link/?xhz) 的"社区贡献动作"。

- **读**：工具启动时自动从这里 `community-actions.json` 拉取最新动作
- **写**：在工具里点"新增动作"或"导入动作 JSON" → 勾"保存即分享" → 工具打开预填好的 Issue 页 → 你在 GitHub 点 Submit → 这个仓库的 GitHub Action 自动合并到 `community-actions.json` → 所有人刷新工具就能看到

## 第一次创建这个仓库

1. 在 GitHub 上点 **"Use this template"** 创建一个新仓库（Public）
2. 新仓库名建议：`ff14-choreo-actions`
3. 创建完成后，把 `ff14-choreo-editor/src/lib/communityConfig.ts` 里的：
   ```ts
   export const COMMUNITY_REPO_OWNER = 'workbuddy-ff14';
   export const COMMUNITY_REPO_NAME = 'community-actions';
   ```
   改成你自己的 owner/name，重新部署工具即可。

## 提交动作的流程

1. 打开 [FF14 编舞时间轴工具](https://47d057355e6242028b9b0caaa21afee0.app.workbuddy.link/?xhz)
2. 左下角勾上 **"保存即分享"**（一次性，状态会记住）
3. 点 **"+ 新增动作"** 或 **"导入动作 JSON"** → 填表 → 保存
4. 弹窗里点 **"🚀 打开 GitHub 提交页"** → 在新打开的 GitHub Issue 页点 **"Submit new issue"**
5. 几秒后 GitHub Action 自动把动作合并进来，并关闭 Issue
6. 你和所有用户刷新工具即可看到新动作

## 数据格式

每条动作：

```json
{
  "id": "act_unique_id",
  "name": "显示名",
  "command": "/emote 命令字符串",
  "duration": 2.0,
  "category": "通用|舞蹈|表情|社交|职业切换",
  "verified": true,
  "isGsChange": false
}
```

- `id` 必须唯一；重复会被跳过
- `command` 是宏里原样输出的字符串
- `isGsChange` 是 `/gs change X` 切职业的特殊事件
