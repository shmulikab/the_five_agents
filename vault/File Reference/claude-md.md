---
name: "CLAUDE.md"
description: "תיעוד קובץ ההגדרות הראשי של Claude Code לפרויקט"
type: reference
---

# CLAUDE.md

## Overview

קובץ `claude/CLAUDE.md` הוא קובץ ההגדרות הראשי של Claude Code עבור הפרויקט. הוא נקרא אוטומטית על ידי Claude Code בכל פתיחת שיחה, ומספק הקשר, הנחיות, ואמנות עבודה לכל מי שעובד עם הקוד. הקובץ הנוכחי הוא **תבנית בלבד** — כל הסעיפים מכילים הערות placeholder ועדיין לא מולאו.

## פרטי הקובץ

| שדה | ערך |
|-----|-----|
| **נתיב** | `claude/CLAUDE.md` |
| **שייכות** | Claude Code (מנגנון מובנה של Anthropic CLI) |
| **מי קורא אותו** | Claude Code CLI — נטען אוטומטית בכל שיחה |
| **מי כותב אותו** | מפתח הפרויקט / מנהל הפרויקט |
| **סטטוס** | תבנית ריקה — טרם מולא |

## מבנה הקובץ

```
# CLAUDE.md
## Project Overview    ← מה הפרויקט עושה
## Setup               ← פקודות התקנה
## Development Commands← פקודות run/test/lint
## Architecture        ← ארכיטקטורה ומבנה
## Key Conventions     ← אמנות קוד ייחודיות
```

## Open Questions

- מה בדיוק עושים חמשת הסוכנים? (Project Overview ריק)
- איזה stack טכנולוגי משתמשים? (Setup ריק)

## קבצים קשורים

- [[obsidian-vault-workflow-skill]] — ה-Skill שמגדיר פרוטוקול עבודה עם vault
- [[skills-gitkeep]] — תיקיית הסקילס שב-claude/
- [[agents-gitkeep]] — תיקיית האייג'נטס שב-claude/
