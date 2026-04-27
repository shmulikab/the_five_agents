---
name: "obsidian-vault-workflow SKILL.md"
description: "תיעוד ה-Skill שמגדיר את פרוטוקול העבודה עם Obsidian vault"
type: reference
---

# claude/skills/obsidian-vault-workflow/SKILL.md

## Overview

קובץ `SKILL.md` בתוך `claude/skills/obsidian-vault-workflow/` מגדיר **Skill** מיוחד שנטען על ידי Claude Code כאשר הוא מופעל. ה-Skill הזה מאמץ פרוטוקול חובה של קריאה וכתיבה ל-vault לפני ואחרי כל משימה. הוא מייצג את "הזיכרון ארוך הטווח" של הפרויקט — כל סשן עבודה נרשם ב-vault ונקרא לפני עבודה חדשה כדי לשמור על רצף.

## פרטי הקובץ

| שדה | ערך |
|-----|-----|
| **נתיב** | `claude/skills/obsidian-vault-workflow/SKILL.md` |
| **שייכות** | Claude Code Skill System (Anthropic) |
| **מי קורא אותו** | Claude Code CLI — נטען כאשר ה-Skill מופעל |
| **מי כותב אותו** | מנהל הפרויקט / DevOps |
| **סטטוס** | פעיל ומלא |

## מה ה-Skill הזה עושה

### Phase 1 — לפני כל משימה
1. **זיהוי נושא** — שם קצר לנושא הסשן
2. **איתור קובץ vault** — חיפוש topic file קיים ב-`vault/`
3. **קריאת הקשר** — Meeting Notes אחרונות, Content Briefs, Brand Guidelines
4. **דיווח** — הצהרה על מה נקרא לפני תחילת העבודה

### Phase 2 — אחרי כל משימה
1. **בחירת תיקיה** — Meeting Notes / Content Briefs / Publishing Log / Brand Guidelines
2. **שם קובץ** — `<topic-hyphenated>.md` (ללא תאריך)
3. **כתיבת session log** — Overview + Open Questions + Session Log entry
4. **wikilinks** — קישורים `[[כך]]` לנושאים קשורים
5. **VerifyRead** — קריאה חוזרת לאימות הכתיבה

## מבנה vault שה-Skill מגדיר

```
vault/
├── Meeting Notes/      ← קוד, ארכיטקטורה, החלטות
├── Content Briefs/     ← בריפים עריכתיים
├── Publishing Log/     ← לוג פרסומים
└── Brand Guidelines/   ← עיצוב, טון, UI
```

## Anti-patterns (מה לא לעשות)

- ❌ שם קובץ עם תאריך (`2026-04-27 topic.md`)
- ❌ ללא תג `[status]` בכותרת session
- ❌ הכנסת session entry מעל entries ישנים
- ❌ שימוש ב-`[markdown links]` במקום `[[wikilinks]]`

## קבצים קשורים

- [[claude-md]] — קובץ ההגדרות הראשי של Claude Code
- [[skills-gitkeep]] — התיקייה שמכילה את ה-Skill הזה
- [[agents-gitkeep]] — תיקיית האייג'נטס המשלימה
