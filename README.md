# feishu-meeting-minutes-card

当前版本：**v2.0**

将飞书会议纪要文档（语音转写或手动记录）整理为结构清晰、格式统一的飞书 interactive 卡片。
> 面向 Claude Code / Codex / MiniMax Code 的飞书会议纪要卡片 Skill

## 功能

- 读取飞书文档链接或直接粘贴的会议记录
- 删除语气词、重复内容和无效对话
- 将时间线讨论重组为 3–8 个主题议题
- 提取参会人、关键决策、待解决问题和 Action Items
- 生成默认随机使用绿色（`green`）或蓝色（`blue`）主题的飞书 interactive 卡片
- 将 Action Items 明确到负责人并按优先级标记

## 前置条件

- 已安装 Claude Code、Codex 或 MiniMax Code
- 已配置可读取飞书文档、发送飞书消息的 MCP / CLI 工具
- 飞书应用具备文档读取与消息发送权限
- 目标文档已向对应 Bot 或应用开放阅读权限

> 不同环境里的飞书工具名称可能不同。安装后请按实际工具接口调整 `SKILL.md` 中的文档读取与卡片发送步骤。

## 安装

### Claude Code

```bash
mkdir -p ~/.claude/skills/feishu-meeting-minutes-card
cp SKILL.md ~/.claude/skills/feishu-meeting-minutes-card/SKILL.md
```

### Codex

安装为用户级 Skill，可在所有项目中使用：

```bash
mkdir -p ~/.agents/skills/feishu-meeting-minutes-card
cp SKILL.md ~/.agents/skills/feishu-meeting-minutes-card/SKILL.md
```

如果只想在当前项目中使用，可安装到项目目录：

```bash
mkdir -p .agents/skills/feishu-meeting-minutes-card
cp SKILL.md .agents/skills/feishu-meeting-minutes-card/SKILL.md
```

Codex 会自动检测 Skill 变更。可以在 Codex CLI 或 IDE 扩展中运行 `/skills` 查看，或输入 `$feishu-meeting-minutes-card` 显式调用；如果未显示，请重启 Codex。

> 参考：[OpenAI Codex Skills 官方文档](https://developers.openai.com/codex/skills)

### MiniMax Code

将 `SKILL.md` 放入当前 MiniMax Code 配置所使用的 skills 目录，并重新加载 Skill。

## 使用方式

可以通过以下方式触发：

```text
根据 https://example.feishu.cn/docx/xxxxx 整理一个会议纪要卡片
```

```text
帮我总结这个会议纪要，并生成飞书卡片：
[粘贴会议记录]
```

典型触发词：

- 会议纪要
- 整理会议纪要
- 会议纪要卡片
- 会议总结
- 会议要点
- 总结一下这个会

## 输出结构

卡片默认包含：

- 会议时间、时长和参会人
- 顶部三个核心重点：优先突出有依据的数据、节点，也支持关键结论；信息不足时不凑数
- 3–8 个独立议题色块
- 关键决策与已达成共识
- Gap、风险和待解决事项
- 明确到负责人的 Action Items

Action Items 优先级：

- 🔴 紧急 / 本周内
- 🔵 常规 / 近期
- 🟢 后续 / 长期

## 卡片规范

- Header 第一行为“会议纪要｜会议主题”，第二行小字仅显示会议时间与时长；不展示 revision、修订号或状态标签

- Header 默认从 `green`（绿色）和 `blue`（蓝色）中等概率随机选择主题；用户明确指定颜色时遵循用户要求
- 议题使用中文数字编号
- 顶部使用三个等宽并列的浅紫、浅蓝、浅橙重点色块，摘要保持 `heading-4`；说明精炼为单行短文，按列宽选择 `normal` 或 `notation`，避免孤字换行
- 每个议题独立使用浅蓝背景、深蓝标题和圆点要点列表；议题标题与正文同字号（`normal`），用加粗和颜色突出
- 关键 Gap 与待解决问题使用浅红底，后续 Action Items 使用浅灰底
- Header 随机颜色不改变正文布局与配色
- 主要要点使用圆点，嵌套细节可使用 `├` / `└`
- 正文与章节标题使用 `normal`；重点说明按长度与列宽调整字号；参会人保留 `notation` 小字设计
- 底部仅保留“查看会议原文”超链接，不附加其他文字
- 关键人名加粗
- Gap 使用 ⚠️ 标记
- 正文重点结论、已完成事项及明确共识使用 ✅ 标记，并加粗短标签；保留条件与完成范围，待确认事项不标成完成
- 已有结论、风险或优先级标记时不再叠加圆点
- 不使用 Markdown 表格，避免飞书卡片渲染异常

## 文件结构

```text
feishu-meeting-minutes-card/
├── SKILL.md
├── README.md
├── LICENSE
└── .gitignore
```

## 效果示例

<img width="1007" height="1562" alt="image" src="https://github.com/user-attachments/assets/28264254-202c-4024-9862-971861f862fa" />
<img width="1070" height="1470" alt="image" src="https://github.com/user-attachments/assets/d796ddb4-b03e-4b8f-a8be-e3d400105327" />


## License

[MIT](LICENSE)
