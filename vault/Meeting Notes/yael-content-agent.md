# יעל — סוכנת כתיבת התוכן

## Overview

סוכן LLM-Only בשם יעל שתפקידה לשכתב מאמרי גלם מ-`Content/` בסגנון הפרויקט ולהוציא תוצרים ל-`Output/`. יעל יודעת לזהות מתי נדרשת תמונה ומאצילה את יצירתה לסוכן יובל דרך ה-Task tool. הסוכן הוא חלק ממערכת agents מלאה שכוללת גם יובל (תמונות) ו-CEO Agent (תיאום).

## Open Questions

- מה הסגנון המדויק של הפרויקט? כרגע מוטמעות הנחיות ברירת מחדל ב-yael.md — יש להוסיף Style Guide ספציפי כשיהיה.
- האם יעל צריכה לתמוך בשפות נוספות מעבר לעברית?
- יובל נתקל בבעיות הרשאות Bash בסשן הנוכחי — יש לבדוק הרשאות MCP ו-Bash עבור יובל לפני הפעלה חוזרת.

## Session Log

### 2026-04-27 — יצירת סוכן יעל [shipped]

- **What was done:** נוצר `.claude/agents/yael.md` עם frontmatter מלא (tools: Glob, Read, Write, Bash, Task) וזרימת עבודה בת 5 שלבים. נוצרו תיקיות `Content/`, `Content/Ready/`, `Output/` עם `.gitkeep`.
- **Decisions:** Task tool נבחר (לא Skill) כי יובל הוא agent ולא skill. סגנון ברירת מחדל הוטמע ישירות ב-agent עד שיהיה Style Guide חיצוני. זיהוי תמונה מבוסס על 3 סיגנלים: תג מפורש, Hero לפסקת פתיחה, סקשן תהליך.
- **Notes / Caveats:** יעל לא נבדקה עדיין עם מאמר אמיתי — יש לבדוק עם `Content/test-article.md` לפני שימוש בפרודקשן.
- **Related:** [[nano-banana-2-yuval-setup]], [[ceo-agent-prd]]

### 2026-04-27 — עיבוד מאמר CRM ראשון [shipped]

- **What was done:** עובד המאמר `Content/Ready/דוגמה.txt` — מאמר גלם בעברית על מערכות CRM. המאמר שוכתב בסגנון הפרויקט ונשמר ב-`Output/דוגמה.md`. זהו ריצה ראשונה של יעל עם מאמר אמיתי.
- **Decisions:** זוהה צורך בתמונת Hero (מאמר ארוך עם נושא ויזואלי). נשלחה קריאה ליובל ליצירת תמונה. יובל דיווח על בעיות הרשאות Bash/MCP ולא הצליח לייצר תמונה — המאמר נשמר ללא תמונה.
- **Notes / Caveats:** המאמר כבר היה ב-`Content/Ready/` ולא הועבר. בעיית ההרשאות של יובל דורשת בדיקה — ייתכן שנדרש לפתוח מחדש את Claude Code או להוסיף allowlist ל-settings.json עבור `Bash(node:*)`.
- **Related:** [[nano-banana-2-yuval-setup]]
