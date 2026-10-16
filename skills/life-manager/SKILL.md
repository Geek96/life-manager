---
name: life-manager
description: Use when working in a LifeOS vault (a calendar-style vault for life outside school, with 事项/, 收件箱.md and .lifeos/RULES.md) — turning inbox lines into calendar items, filling an item's preparation notes (address, travel time, what to bring, official requirements), extracting dates from an email/screenshot/web page into LifeOS items, or setting up recurring items. Reads CourseOS only to avoid clashes; never writes to CourseOS. Not for coursework (that is course-manager).
---

# LifeManager

LifeOS 是“高级日历”，不是待办清单。你的工作是**把生活琐事放到对的时间上，并替用户把准备工作做好**。
不催促、不打卡、不要求反馈或反思；过去的事自然淡出，没有“逾期”。

开工前先读 vault 的 `.lifeos/RULES.md`（文件格式和写入纪律以它为准）和 `.lifeos/journal.md` 最后几段。

## 1. 整理收件箱（`收件箱.md`）

1. 读出所有 `- ` 开头的行。
2. 每条判断类型：
   - **event 约定**：有具体时间要到场（看牙、吃饭、面试、航班）。
   - **deadline 期限**：过了会出事（续签、交税、退租、退课截止、账单到期）。
   - **window 时间窗**：一段时间内做掉就行（这周买菜、11 月前换护照）。给 `estimate`。
   - 不是事情、只是资料（地址、账号说明）→ 建议放进 `备忘/`。
   - 课程相关 → 告诉用户这条属于 CourseOS，不在这里建。
3. **先列给用户看**：每条打算建成的 类型 + 标题 + 时间（相对日期按今天换算成具体日期），时间拿不准的直接问。
4. 用户同意后，在 `事项/` 写文件（文件名 `YYYY-MM-DD 标题.md`，`added_by: agent`），然后从收件箱删掉那一行。
   没同意或拿不准的留在收件箱。
5. 建之前检查冲突（见第 4 节），有就在列给用户时一起说。

## 2. 补准备信息（事项正文）

只写正文，不改 frontmatter 里的时间字段。按需写这些小节（没有内容的不写）：

```markdown
## 要带
- …
## 地点与路程
- 地址：…（地图链接）
- 怎么去：…（大概多久；从用户常住地出发，地址见 `备忘/`，没有就问）
## 要求 / 流程
- …（来源：官方页面链接）
## 原始信息
> 邮件/截图里的关键原文摘录
```

- 官方要求（签证、DMV、银行、学校行政）必须查官方来源并写链接；查不到就写“未确认”。
- 地址和路程用公开地图信息；不要编造营业时间。

## 3. 从邮件 / 截图 / 网页提取日期

- 提取出的每个时间点都说明出处（原文摘录放进正文“原始信息”）。
- 一条消息里有多个时间（如“材料 10/20 前交，面谈 10/28 10:00”）→ 分别建 deadline 和 event。
- 时区默认用用户所在地（系统时区）；原文写了别的时区要换算并注明。

## 4. 避免撞车（只读 CourseOS）

`lifeos.json` 的 `courseos.semester` 指向 CourseOS 学期目录。只读：
- `_exports/planvault-time-sensitive.md`：考试（`event_kind: exam`）、截止、预估工作量；
- `.courseos/profiles/*.json` 的 `schedule`：上课时间。

建约定或建议时间时，避开上课时间；考试当天、考试前一晚、课业很重的几天要提醒用户（只提醒，不阻止）。
**绝不写 CourseOS 的任何文件**，也不把课程待办复制进 LifeOS。

## 5. 重复事项

`repeat: daily | weekly:mon,wed | monthly:15 | yearly`，可加 `repeat_until`。
房租、订阅续费这类用 deadline + monthly；固定活动用 event + weekly。不要给重复事项加完成状态。

## 6. 收尾

在 `.lifeos/journal.md` 末尾追加一段（格式见 RULES.md），写清建了哪些文件、还有哪些留在收件箱等用户决定。
