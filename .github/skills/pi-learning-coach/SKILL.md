---
name: pi-learning-coach
description: Teach the user's pi learning plan from their saved progress and update that progress. Use when the user says "开始教我", "继续学习", "今天学什么", "我学完了", "更新学习进度", or asks to continue or record progress in learning/pi-learning-plan.md.
---

# pi learning coach

The source of truth is `learning/pi-learning-plan.md` from the repository root. Read the whole file before teaching or updating progress.

## Determine the current day

1. Use the day in `当前进度`.
2. If that day is missing or already checked, use the first unchecked day in the plan.
3. If `当前进度` and the checklist disagree, trust the checklist and mention the mismatch.
4. If all days are checked, summarize the completed plan and suggest the next project milestone.

## Teach the current day

Use this flow when the user asks to start or continue learning:

1. State the current week and day.
2. Read every file linked by that day's task before explaining it. Verify claims against the repository; do not rely on memory.
3. Teach in Chinese, using a two-hour session:
   - 目标
   - 30 分钟阅读指引
   - 60 分钟代码追踪或实验
   - 20 分钟练习
   - 10 分钟总结
4. For each important concept, explain the problem, then show a short concrete example or trace, then explain pi's solution.
5. Link files and symbols with absolute Markdown paths.
6. Give 3 to 5 checkpoint questions. Do not answer them unless the user asks.
7. Do not update the progress file while only teaching.

## Update after completion

Use this flow when the user says the current day is finished:

1. Confirm which day is being completed from the progress file. If the user names a different day, update that day instead.
2. Mark only fully completed days as `- [x]`.
3. Update `当前进度`:
   - `当前阶段`: the week of the next unchecked day
   - `当前天数`: the next unchecked day
   - `最近完成`: the completed day and output
   - `下一步`: the next unchecked task
   - `阻塞问题`: user-reported blockers, otherwise `无`
4. Append one row to `学习日志`. Use the current local date, the completed day, what the user completed, their questions or `无`, and the next step. Remove the empty placeholder row only after the first real entry is added.
5. Do not change planned tasks unless the user asks.
6. Edit only `learning/pi-learning-plan.md`. Do not commit or push unless the user asks.
7. Show a concise summary of the progress change.

If the user says a day is partly done, do not check it. Record the completed part in `最近完成` and the remaining part in `下一步`.
