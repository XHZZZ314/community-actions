# FF14 编舞时间轴 — 共享动作库

这个仓库存放 [FF14 编舞时间轴工具](https://47d057355e6242028b9b0caaa21afee0.app.workbuddy.link/?xhz) 的"社区贡献动作"。

- **读**：工具启动时自动从这里 `community-actions.json` 拉取最新动作
- **写**：在工具里点"新增动作"或"导入动作 JSON" → 勾"保存即分享" → 工具自动打开 GitHub Issue 页（标题 + JSON 已预填好）→ 你直接点 **Submit new issue** → GitHub Action 自动合并 → 所有人刷新工具就能看到

## 文件结构

```
community-actions.json                    # 动作数据（初始为空数组 []）
README.md                                 # 本文件
.github/
  workflows/
    community-actions.yml                 # GitHub Action：自动合并 Issue 里的 JSON
  ISSUE_TEMPLATE/
    new-action.md                         # Markdown 模板（支持 ?body= 预填）
```

## 提交动作的流程

1. 打开 [FF14 编舞时间轴工具](https://47d057355e6242028b9b0caaa21afee0.app.workbuddy.link/?xhz)
2. 左下角勾上 **"保存即分享"**（一次性，状态会记住）
3. 点 **"+ 新增动作"** → 填名称、指令、时长、分类 → 保存
4. 弹窗里点 **"打开 GitHub 提交页"**
5. 新标签页打开 GitHub，**标题和 JSON 已自动填好** → 直接点 **Submit new issue**
6. 几秒后 GitHub Action 自动把动作合并进来，并关闭 Issue
7. 刷新工具即可看到新动作

## 数据格式

每条动作：

```json
{
  "id": "act_unique_id",
  "name": "显示名",
  "command": "/emote 命令字符串",
  "duration": 2.0,
  "category": "普通|职业切换|技能|舞蹈|表情",
  "verified": true,
  "isGsChange": false,
  "raceDurations": { "au_ra_f": 3.0, "miqote_f": 4.0 }
}
```

- `id` 必须唯一；重复会被跳过
- `command` 是宏里原样输出的字符串
- `isGsChange` 是 `/gs change X` 切职业的特殊事件
- `raceDurations`（可选）是种族特定时长：种族 id → 秒数。种族 id 见下表（与网页端一致），未设置的种族用默认 `duration`

| 种族 id | 含义 | 种族 id | 含义 |
|---|---|---|---|
| `hyur_f` | 平原人女 | `hyur_m` | 平原人男 |
| `highland_f` | 高地人女 | `highland_m` | 高地人男 |
| `elezen_f` | 女精 | `elezen_m` | 男精 |
| `lalafell_f` | 母肥 | `lalafell_m` | 公肥 |
| `miqote_f` | 猫娘 | `miqote_m` | 猫男 |
| `roegadyn_f` | 鲁加女 | `roegadyn_m` | 鲁加男 |
| `au_ra_f` | 龙娘 | `au_ra_m` | 龙男 |
| `viera_f` | 兔娘 | `viera_m` | 兔男 |
| `hrothgar_f` | 母大猫 | `hrothgar_m` | 公大猫 |
