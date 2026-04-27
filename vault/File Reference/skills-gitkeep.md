---
name: "claude/skills/.gitkeep"
description: "תיעוד placeholder לתיקיית הסקילס"
type: reference
---

# claude/skills/.gitkeep

## Overview

קובץ `.gitkeep` בתיקייה `claude/skills/` הוא placeholder ריק שנועד לשמר את התיקייה במערכת הגרסאות (git). ב-git, תיקיות ריקות אינן נשמרות אוטומטית — קובץ זה מאפשר לתיקייה להתקיים בgit גם כשאין בה קבצים ממשיים. התיקייה `claude/skills/` מיועדת לאחסן **Skill files** — קבצי הגדרה שמוסיפים יכולות מיוחדות ל-Claude Code.

## פרטי הקובץ

| שדה | ערך |
|-----|-----|
| **נתיב** | `claude/skills/.gitkeep` |
| **שייכות** | תשתית Git — לא שייך לאף מודול לוגי |
| **מי קורא אותו** | Git בלבד (לא קוד, לא Claude) |
| **מי כותב אותו** | נוצר אוטומטית בעת init של הפרויקט |
| **סטטוס** | ריק — ממתין לסקילס ראשונה |

## מה מגיע לתיקייה הזו

כל Skill שנוסף לפרויקט מקבל תיקייה משלו בתוך `claude/skills/`:

```
claude/skills/
├── .gitkeep                           ← הקובץ הזה (placeholder)
└── obsidian-vault-workflow/
    └── SKILL.md                       ← דוגמה לסקיל קיים
```

## קבצים קשורים

- [[claude-md]] — קובץ ההגדרות שמפנה לתיקיה זו
- [[obsidian-vault-workflow-skill]] — הסקיל הראשון שנוסף לתיקייה
- [[agents-gitkeep]] — אח לתיקיית agents/ (אותה מטרה)
