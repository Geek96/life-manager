# LifeManager

[LifeOS](https://github.com/Geek96/lifeos)（生活“高级日历”）的 agent skill：

- 整理收件箱：把随手记的一句话变成日历事项（约定 / 期限 / 时间窗），先问用户再写
- 补准备信息：地址、路程、要带的材料、官方要求（附来源）
- 从邮件 / 截图 / 网页提取日期
- 只读 [CourseOS](https://github.com/Geek96/courseos) 的学期目录，避开上课和考试；从不写回

## 安装

```bash
npx skills add Geek96/life-manager
```

或手动：`ln -s "$PWD/skills/life-manager" ~/.claude/skills/life-manager`

vault 格式见 LifeOS 仓库的 `templates/vault/.lifeos/RULES.md`。
