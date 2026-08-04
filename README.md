# feishu-meeting-minutes-card

将飞书会议纪要文档（语音转写或手动记录）整理为结构清晰、格式统一的飞书 interactive 卡片。
> 面向 Claude Code / MiniMax Code 的飞书会议纪要卡片 Skill

## 功能

- 读取飞书文档链接或直接粘贴的会议记录
- 删除语气词、重复内容和无效对话
- 将时间线讨论重组为 3–8 个主题议题
- 提取参会人、关键决策、待解决问题和 Action Items
- 生成 violet 主题的飞书 interactive 卡片
- 将 Action Items 明确到负责人并按优先级标记

## 前置条件

- 已安装 Claude Code 或 MiniMax Code
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
- 3–8 个议题模块
- 关键决策与已达成共识
- Gap、风险和待解决事项
- 明确到负责人的 Action Items

Action Items 优先级：

- 🔴 紧急 / 本周内
- 🔵 常规 / 近期
- 🟢 后续 / 长期

## 卡片规范

- Header 使用 `violet` 主题
- 议题使用中文数字编号
- 模块之间使用 `hr` 分隔
- 使用 `├` / `└` 表达内容层级
- 关键人名加粗
- Gap 使用 ⚠️ 标记
- 共识或决议使用 ✅ 标记
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

参考案例暂不随仓库公开，请根据自己的会议场景补充脱敏后的截图或示例内容。


## License

[MIT](LICENSE)
