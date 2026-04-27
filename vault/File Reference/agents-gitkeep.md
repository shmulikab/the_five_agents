---
name: "claude/agents/.gitkeep"
description: "תיעוד placeholder לתיקיית האייג'נטס"
type: reference
---

# claude/agents/.gitkeep

## Overview

קובץ `.gitkeep` בתיקייה `claude/agents/` הוא placeholder ריק שנועד לשמר את התיקייה במערכת הגרסאות (git). התיקייה `claude/agents/` מיועדת לאחסן **Agent definitions** — קבצי הגדרה של sub-agents מיוחדים שניתן להפעיל דרך Claude Code. זוהי התיקייה שבה יתגוררו חמשת הסוכנים של הפרויקט כשייכתבו.

## פרטי הקובץ

| שדה | ערך |
|-----|-----|
| **נתיב** | `claude/agents/.gitkeep` |
| **שייכות** | תשתית Git — לא שייך לאף מודול לוגי |
| **מי קורא אותו** | Git בלבד (לא קוד, לא Claude) |
| **מי כותב אותו** | נוצר אוטומטית בעת init של הפרויקט |
| **סטטוס** | ריק — ממתין לחמשת הסוכנים |

## מה מגיע לתיקייה הזו

כל Agent שנוסף מקבל תיקייה משלו (או קובץ MD) בתוך `claude/agents/`:

```
claude/agents/
├── .gitkeep      ← הקובץ הזה (placeholder)
├── agent-1.md    ← סוכן עתידי
├── agent-2.md    ← סוכן עתידי
├── agent-3.md    ← סוכן עתידי
├── agent-4.md    ← סוכן עתידי
└── agent-5.md    ← סוכן עתידי
```

## קשר לפרויקט

זוהי התיקייה המרכזית של הפרויקט `the_five_agents` — שמה של הפרויקט מרמז שכאן יוגדרו חמשת הסוכנים הראשיים.

## קבצים קשורים

- [[claude-md]] — קובץ ההגדרות שמפנה לתיקיה זו
- [[skills-gitkeep]] — תיקיית אחות עבור skills/
- [[obsidian-vault-workflow-skill]] — דוגמה לאיך מוגדר skill (דומה לאיך יוגדרו agents)
