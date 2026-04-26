# 场景路由器

本文档帮助模型在开始任何工作前，自行判断任务类型，然后读取对应的 reference 文件。**必须在读取本文件后，再根据任务类型读取相应的参考文件，不可跳过。**

---

## 任务类型识别

根据用户的输入，判断属于以下哪种任务类型：

### 类型 1：原创角色卡 / 原创世界书

**触发关键词：** 创建角色、写卡、角色设定、生成角色、角色卡、写一个角色、设计角色、世界书、生成世界书、创建世界书

**需要读取的 reference：**
- `references/character-guide.md`
- `references/worldbuilding-guide.md`
- `references/config-guide.md`
- `references/position-guide.md`
- 如果涉及物品/能力：`references/extract-item.md`

---

### 类型 2：轻小说/游戏/小说 → 转化世界书

**触发关键词：** 轻小说、小说、转角色卡、根据原文、根据小说、转化、提取、原作、游戏、文本转化、原文

**需要读取的 reference：**
- `references/conversion-guide.md`（转化工作流总览）
- `references/extract-worldbuilding.md`（世界观提取）
- `references/extract-character.md`（角色提取）
- `references/extract-item.md`（物品/能力提取）
- `references/extract-story.md`（故事/章节提取）
- `references/character-guide.md`（角色条目写入规范）
- `references/worldbuilding-guide.md`（世界观条目写入规范）
- `references/config-guide.md`（配置规范）
- `references/position-guide.md`
- **不读** `references/extract-style.md`（除非用户明确要求提取文风）

---

### 类型 3：纯世界观/规则设定

**触发关键词：** 世界观、设定集、规则书、魔法体系、修炼体系、势力设定、地理设定、世界规则

**需要读取的 reference：**
- `references/worldbuilding-guide.md`
- `references/config-guide.md`
- `references/position-guide.md`
- 如果涉及物品/能力：`references/extract-item.md`

---

### 类型 4：物品/能力/装备设定

**触发关键词：** 武器、道具、装备、技能、能力、功法、魔法、物品、神器、防具、消耗品

**需要读取的 reference：**
- `references/extract-item.md`
- `references/worldbuilding-guide.md`（物品需要挂靠世界观）
- `references/config-guide.md`
- `references/position-guide.md`

---

### 类型 5：文风提取/文风设定

**触发关键词：** 文风、写作风格、文笔、笔风、语言风格、模仿写作

**需要读取的 reference：**
- `references/extract-style.md`
- `references/config-guide.md`
- `references/position-guide.md`

---

### 类型 6：故事/章节提取

**触发关键词：** 故事线、章节、总结故事、提取章节、剧情提取、每章总结

**需要读取的 reference：**
- `references/extract-story.md`
- `references/config-guide.md`
- `references/position-guide.md`

---

### 类型 7：修改已有世界书

**触发关键词：** 修改、更新、编辑、添加条目、删除条目、调整

**需要读取的 reference：**
- 先用 `python scripts/query.py <世界书路径>` 查看现有条目
- 根据要修改的内容类型，读取对应的 reference（参考类型 1-6）
- `references/config-guide.md`

---

## 决策流程

```
用户输入 → 匹配关键词 → 确定任务类型 → 读取对应 reference 文件 → 开始执行
```

如果用户输入同时匹配多种类型（如"把这个轻小说转成角色卡"），按**类型 2（转化）**处理，它已包含所有子类型需要的 reference。

如果用户输入不明确，**先询问用户**意图，不要猜测。

---

## 执行原则

1. **先读 reference，再动手。** 不要凭记忆写，必须读过对应 reference 后才开始写条目。
2. **每个任务类型都必须读 `config-guide.md` 和 `position-guide.md`**——配置错误比内容错误更难排查。
3. **转化任务必须先读 `conversion-guide.md`**，它规定了提取→条目创建的整体流程。
4. 对于修改任务，**先用 `query.py` 查看**，再确定改什么。
