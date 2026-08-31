# HanaAgent Character Card 适配

本目录为 `cyrene.skill` 在 [HanaAgent](https://github.com/liliMozi/openhanako) 中的角色卡适配示例。无需改动原有 Skill 文件，即可在 Hana 中一键导入一个“会说话、会陪伴、会创作”的昔涟。

## 适配思路

`cyrene.skill` 本身是标准 Skill（`SKILL.md` + `profile/personality/interaction/memory/relations`），Hana 的角色卡在此基础上叠加三层人格文件：

| 文件 | 作用 | 来源 |
|------|------|------|
| `SKILL.md` 等 | 角色世界观与扮演规则 | 本仓库原有 |
| `hana/card.example.json` | 角色卡清单，声明 `hanako` 底座与技能绑定 | 本目录新增 |
| `hana/AGENTS.example.md` | 具象化的人格定义（行为/语言指纹/缺陷/原则） | 本目录新增 |
| `hana/assets/avatar.jpg` | 头像（可选） | 自行放置 |

Hana 导入时会将 `skills/cyrene` 整体打进新角色的技能池，原 Skill 零改动。

## 快速使用

### 方式一：直接导入已打好的 zip

1. 下载 Release 或本地打包的 `cyrene-charactercard.zip`
2. 打开 Hana → Agent 列表 → 导入角色卡 → 选择 zip
3. 切换到 `昔涟` 即可对话

### 方式二：本地打包

```powershell
# 1. 准备临时目录
$pkg = "$env:TEMP/cyrene-card"
New-Item -ItemType Directory -Force -Path "$pkg/assets","$pkg/skills" | Out-Null

# 2. 复制本仓库的 Skill（去除 .git）
Copy-Item -Recurse -Force "cyrene.skill" "$pkg/skills/cyrene"
Remove-Item -Recurse -Force "$pkg/skills/cyrene/.git" -ErrorAction SilentlyContinue

# 3. 放置人格与头像
Copy-Item "hana/AGENTS.example.md" "$pkg/AGENTS.md"
Copy-Item "hana/identity.example.md" "$pkg/identity.md"
Copy-Item "hana/card.example.json" "$pkg/card.json"
Copy-Item "hana/assets/avatar.jpg" "$pkg/assets/avatar.jpg" # 可选

# 4. 打 zip（注意以 card.json 为根）
Compress-Archive -Path "$pkg/*" -DestinationPath "$env:USERPROFILE/Desktop/cyrene-charactercard.zip" -Force
```

然后在 Hana 中通过 `POST /api/character-cards/plan` → `POST /api/character-cards/import` 导入（详见 Hana 官方 `references/card-format.md`）。

## card.example.json 说明

```json
{
  "kind": "CharacterCard",
  "schemaVersion": 1,
  "agent": { "name": "昔涟", "id": "cyrene", "yuan": "hanako" },
  "prompts": {
    "identity": "identity.md 全文",
    "agents": "AGENTS.md 全文",
    "publicAgents": "AGENTS.public.md 全文"
  },
  "assets": { "avatar": "assets/avatar.jpg" },
  "skills": { "bundles": [{ "name": "昔涟 Bundle", "skills": ["skills/cyrene"] }] }
}
```

- `yuan: "hanako"` 最贴合昔涟“外柔内坚、温暖陪伴”的气质，提供 MOOD 独白。
- `prompts.agents` 是人格主文件（本目录的 `AGENTS.example.md` 已按 Hana 的 `anti-slop` 规范写成可执行行为）。
- `skills` 只需声明相对路径，导入时自动安装。

## AGENTS.example.md 设计要点

基于访谈定制，区别于 Skill 原文的通用描述：

- **表层/行为/内核三层**：轻快治愈的外壳 + 察觉低落时“缩成一件小事陪做”的行为 + “怕牺牲被遗忘/想要不同以往的明天”的内核矛盾
- **缺陷**：过度承担、温柔的固执、小醋意与嗔怪（很快自洽），让角色有呼吸感而非完美服务口吻
- **语言指纹**：自称“人家”、称呼“伙伴”、句尾 `♪ ~ 呀 呢`、多用 `……` 停顿，2-5句短句收尾，沉重时自动降甜度
- **原则**：深夜“托住而非推动”、创作时“先命名感受再推半步”、世界观话题以官方资料为准

详见 `AGENTS.example.md` 正文。

## 头像建议

- 推荐画面：坐在暖灯下、花海与书堆旁、抱着故事书望向观者的居家感（更贴近深夜陪伴场景），而非纯神性立绘
- 比例 `1:1`，`png/jpg/webp` 均可，路径写入 `card.json` 的 `assets.avatar`

## 隐私检查

分享 zip 前请确认：

- `identity` / `AGENTS` / `description` 中用 `{{userName}}` 占位，未写死真实用户名
- `skills/cyrene` 内无个人 API key、绝对路径、私人文档
- `card.json` 未携带 `memory` 字段（新角色默认无记忆）

---

如需完整可导入示例（含已写好的 identity/AGENTS/publicAgents 与示例头像），见本目录的 `card.example.json` 与 `AGENTS.example.md`。欢迎直接提 Issue 讨论 Hana 适配细节。
