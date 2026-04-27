# Nano Banana 2 + יובל — הגדרה

## Overview

הוספת שני רכיבים ויזואליים לפרויקט: (1) Skill `nano-banana-2` שעוטף את ה-MCP של Google Nano Banana 2 (gemini-3.1-flash-image-preview) ליצירת תמונות, ו-(2) Agent `yuval` — סוכן קריאייטיב שסורק תמונות reference, מנתח סגנון ויזואלי, מנסח פרומפטים עקביים, ומייצר תמונות ל-outputs/. המערכת מבוססת על MCP server (`nano-banana-2-mcp` ב-npx). אומת בפועל: ה-MCP tool אינו זמין ישירות ב-Agent SDK — במקומו נעשה שימוש ב-Python google-genai SDK עם המודל `gemini-3.1-flash-image-preview` דרך `generateContent` API.

## Open Questions

- אילו תמונות reference יוכנסו לתיקייה (עדיין ריקה)?
- האם יידרש Edit image (עריכת תמונה קיימת) בנוסף ל-Generate?
- האם ניתן להגדיר את ה-MCP כך שיהיה זמין ישירות ב-Agent SDK, או שיש להמשיך דרך Python SDK?

## Session Log

### 2026-04-27 — יצירת nano-banana-2 Skill ו-yuval Agent [shipped]

- **What was done:** נוצרו 5 קבצים: (1) `.claude/settings.json` עם MCP config, (2) `.claude/skills/nano-banana-2/SKILL.md` עם תיעוד מלא של tools/parameters/prompting guide, (3) `.claude/agents/yuval.md` עם זרימת עבודה מלאה בת 6 שלבים, (4) `reference/.gitkeep`, (5) `outputs/.gitkeep`.
- **Decisions:** MCP נבחר: `nano-banana-2-mcp` (npx) — הנגיש ביותר ללא התקנה גלובלית. יובל תמיד בודק reference/ לפני יצירה כדי לשמור על עקביות ויזואלית. שמירה תמיד ל-outputs/ עם שם תיאורי+תאריך.
- **Notes / Caveats:** ה-model הושק פברואר 2026 (לאחר knowledge cutoff) — יש לאמת שה-API key תקין ו-npx זמין לפני שימוש ראשון. reference/ ריקה כרגע — יובל יפעל ללא ניתוח סגנון עד שתמונות יוכנסו.
- **Related:** [[ceo-agent-prd]], [[project-file-documentation]], [[skill-creator-install]]

### 2026-04-27 — תיקון yuval — חסר Skill tool [shipped]

- **What was done:** התגלתה ותוקנה באג קריטי ב-`yuval.md` — ה-`Skill` tool לא היה ברשימת ה-tools של הסוכן, מה שמנע ממנו לקרוא לסקיל `nano-banana-2`.
- **Decisions:** הוסף `Skill` לרשימת tools בפרונטמאטר של yuval.md. ה-GEMINI_API_KEY אומת כמוגדר ב-settings.json וב-.env.
- **Notes / Caveats:** שאלה פתוחה — האם `nano-banana-2-mcp` npm package קיים בפועל? יש לבדוק בפעם הראשונה שמנסים ליצור תמונה.
- **Related:** [[nano-banana-2-yuval-setup]]

### 2026-04-27 — יצירת תמונת טלמון-בנימין ראשונה [shipped]

- **What was done:** יובל יצר תמונה פוטוריאליסטית של ישוב טלמון בהרי יהודה/שומרון (אזור בנימין). נשמרה ל-`outputs/talmon-binyamin-2026-04-27.png` (1.1MB). תיקיית reference/ ריקה — התמונה נוצרה ללא ניתוח סגנון קיים.
- **Decisions:** ה-MCP tool `mcp__nano-banana-2__generate_image` אינו זמין בסביבת Agent SDK הנוכחית. הפתרון: התקנת `google-genai` Python SDK (v1.73.1) ושימוש ב-`gemini-3.1-flash-image-preview` דרך `client.models.generate_content()` עם `response_modalities=['IMAGE', 'TEXT']`. המודל `imagen-3.0-generate-002` לא היה זמין עם ה-API key הנוכחי.
- **Notes / Caveats:** `google-genai` מותקן ב-user path (`C:/Users/shmulika/AppData/Roaming/Python/Python314/site-packages`) — יש להוסיף ל-sys.path בכל הפעלה. ה-GEMINI_API_KEY תקין ועובד.
- **Related:** [[nano-banana-2-yuval-setup]]
