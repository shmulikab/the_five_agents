# מבנה הפרויקט — the_five_agents

מסמך זה מסביר את תפקידה של כל תיקייה וכל קובץ בפרויקט.

---

## מבט על

```
the_five_agents/
├── .claude/          ← הגדרות Claude Code (סוכנים, סקילס, MCP, hooks)
├── .env              ← משתני סביבה (API keys)
├── .git/             ← מערכת גרסאות Git
├── .obsidian/        ← הגדרות אפליקציית Obsidian
├── Content/          ← מאמרי גלם ממתינים לשכתוב (קלט ליעל)
├── Content/Ready/    ← מאמרי גלם לאחר טיפול (ארכיון)
├── Output/           ← תוצרים מוכנים שיעל ויובל מייצרים
├── docs/             ← מסמכי PRD ותיעוד פרויקט
└── vault/            ← זיכרון ארוך-טווח של Claude Code
```

---

## `.claude/` — לב הפרויקט

תיקיית ההגדרות של Claude Code. נקראת אוטומטית בכל שיחה.

```
.claude/
├── CLAUDE.md         ← הנחיות ראשיות ל-Claude Code
├── settings.json     ← הגדרות פרויקט: MCP servers, hooks, הרשאות
├── agents/           ← הגדרות הסוכנים
├── skills/           ← הגדרות הסקילס
├── commands/         ← פקודות slash מותאמות (/brainstorm, /write-plan, /execute-plan)
└── hooks/            ← סקריפטי SessionStart (Superpowers)
```

### `.claude/CLAUDE.md`
**תפקיד:** קובץ ההגדרות הראשי. נטען אוטומטית בכל פתיחת שיחה עם Claude Code.
מגדיר: מטרת הפרויקט, פקודות פיתוח, ארכיטקטורה, אמנות עבודה, ופרוטוקול חובה לשימוש ב-vault.

### `.claude/settings.json`
**תפקיד:** הגדרות פרויקט ברמת Claude Code — כולל רשימת MCP servers פעילים.
**מכיל כרגע:** הגדרת `nano-banana-2-mcp` (Google Gemini image generation).

---

## `.claude/agents/` — הסוכנים

כל קובץ `.md` בתיקייה זו מגדיר **Sub-Agent** — סוכן AI מיוחד שניתן להפעיל.
Claude Code טוען את ה-`description` של כל סוכן ומחליט אוטומטית מתי להפעילו.

```
agents/
├── ceo_agent.md      ← סוכן המנכ"ל — מנהל ומנתב את כל הסוכנים
├── yuval.md          ← יובל — סוכן קריאייטיב ויזואלי (יצירת תמונות)
├── yael.md           ← יעל — כותבת תוכן (שכתוב מאמרים, אינטגרציה עם יובל)
├── code-reviewer.md  ← סוכן סקירת קוד (מ-Superpowers)
├── reference/        ← תמונות השראה לסוכן יובל
└── outputs/          ← תמונות מוגמרות שיובל ייצר
```

### `.claude/agents/ceo_agent.md`
**תפקיד:** סוכן המנכ"ל — נקודת הכניסה הבלעדית לכל משימה.
מקבל כל בקשה מהמשתמש, מנתח, מחליט לאיזה סוכן לנתב, ומסכם את התוצאה.
**עיקרון:** עובד שקט, מתייעץ רק במקרים מורכבים, פועל באוטונומיה מרבית.

### `.claude/agents/yuval.md`
**תפקיד:** סוכן קריאייטיב ויזואלי. מופעל כשמבקשים ליצור תמונה.
**זרימת עבודה:** סורק `reference/` ← מנתח סגנון ← מנסח פרומפט ← מייצר תמונה דרך nano-banana-2 ← שומר ב-`outputs/`.
**מטרה:** שמירה על עקביות ויזואלית בין כל תמונות הפרויקט.

### `.claude/agents/yael.md`
**תפקיד:** סוכנת כתיבת תוכן — LLM-Only (ללא גישה לאינטרנט/API חיצוני).
**זרימת עבודה:** קוראת מאמר מ-`Content/` ← משכתבת בסגנון הפרויקט ← מזהה צורך בתמונה ← קוראת ליובל ← שומרת ב-`Output/` ← מעבירה מקור ל-`Content/Ready/`.
**כלים:** `Glob`, `Read`, `Write`, `Bash`, `Task` (להפעלת יובל).

### `.claude/agents/code-reviewer.md`
**תפקיד:** סוכן סקירת קוד מ-Superpowers. מופעל דרך `requesting-code-review` skill.

### `.claude/agents/reference/`
**תפקיד:** תיקיית תמונות ההשראה של יובל.
**שימוש:** הכנס לכאן תמונות שמגדירות את הסגנון הויזואלי הרצוי לפרויקט. יובל יסרוק ויחקור אותן לפני כל יצירה.

### `.claude/agents/outputs/`
**תפקיד:** תיקיית הפלט — כאן נשמרות כל התמונות שיובל מייצר.
**שמות קבצים:** `<נושא>-<YYYY-MM-DD>.png`

---

## `.claude/skills/` — הסקילס

כל תיקייה בתוך `skills/` מגדירה **Skill** — יכולת מיוחדת שניתן להפעיל ב-Claude Code.
הסקיל נטען כשמפעילים אותו ומספק הנחיות ספציפיות לביצוע סוג מסוים של משימה.

```
skills/
├── nano-banana-2/                    ← יצירת תמונות דרך Google Nano Banana 2
├── obsidian-bases/                   ← יצירת קבצי Obsidian Base (.base)
├── obsidian-markdown/                ← כתיבת Obsidian Flavored Markdown
├── obsidian-vault-workflow/          ← פרוטוקול חובה לניהול vault
├── skill-creator/                    ← כלי ליצירה ובדיקה של Skills חדשים
│
│   ── Superpowers (מ-github.com/obra/superpowers) ──
├── brainstorming/                    ← חקירת כוונות ודרישות לפני מימוש
├── dispatching-parallel-agents/      ← הרצת sub-agents מקבילים
├── executing-plans/                  ← ביצוע תוכנית עבודה מאושרת
├── finishing-a-development-branch/   ← סיום branch בצורה מסודרת
├── receiving-code-review/            ← קבלת ויישום הערות code review
├── requesting-code-review/           ← בקשת code review לפני merge
├── subagent-driven-development/      ← פיתוח מבוסס sub-agents בסשן הנוכחי
├── systematic-debugging/             ← דיבוג שיטתי לפני ניחושים
├── test-driven-development/          ← TDD — בודק לפני שמממש
├── using-git-worktrees/              ← בידוד עבודה ב-git worktrees
├── using-superpowers/                ← מדריך לשימוש בכל הסקילס
├── verification-before-completion/   ← אימות לפני הצהרת "סיימתי"
├── writing-plans/                    ← כתיבת תוכנית לפני נגיעה בקוד
└── writing-skills/                   ← יצירה ובדיקת Skills חדשים
```

### `.claude/skills/nano-banana-2/SKILL.md`
**תפקיד:** עוטף את ה-MCP של Google Nano Banana 2 (מודל `gemini-3.1-flash-image-preview`).
**מכיל:** תיעוד כלים (`generate_image`, `edit_image`), פרמטרים, מדריך לכתיבת פרומפטים, טיפול בשגיאות.
**מי משתמש:** בעיקר סוכן יובל.

### `.claude/skills/obsidian-bases/SKILL.md`
**תפקיד:** הנחיות ליצירת קבצי `.base` עבור Obsidian — תצוגות, פילטרים, נוסחאות וסיכומים.

### `.claude/skills/obsidian-markdown/SKILL.md`
**תפקיד:** הנחיות לכתיבת Obsidian Flavored Markdown — wikilinks, embeds, callouts, properties, tags.

### `.claude/skills/obsidian-vault-workflow/SKILL.md`
**תפקיד:** פרוטוקול חובה — מגדיר מה לקרוא לפני כל משימה (Phase 1) ומה לכתוב אחריה (Phase 2).
**חשיבות:** זהו ה"זיכרון" של הפרויקט. כל סשן עבודה נרשם ב-vault, ונקרא בסשן הבא כהקשר.

### `.claude/skills/skill-creator/`
**תפקיד:** כלי מלא ליצירה, בדיקה ואופטימיזציה של Skills חדשים. מגיע מ-Anthropic.
**מכיל:**
| קובץ/תיקייה | תפקיד |
|-------------|--------|
| `SKILL.md` | הנחיות הסקיל עצמו — 7 שלבי יצירה |
| `agents/analyzer.md` | מנתח הבדלים בין גרסאות skill |
| `agents/comparator.md` | השוואה עיוורת בין תוצאות |
| `agents/grader.md` | בודק pass/fail לפי expectations |
| `scripts/` | 8 סקריפטי Python להרצת evals ואופטימיזציה |
| `assets/eval_review.html` | ממשק HTML לניהול eval sets |
| `eval-viewer/` | viewer אינטראקטיבי לתוצאות |
| `references/schemas.md` | תיעוד סכמות JSON |

---

---

## `Content/` — מאמרי גלם

**תפקיד:** תיקיית הקלט של סוכן יעל. כאן מניחים מאמרים לשכתוב.
**פורמטים נתמכים:** `.md`, `.txt`, `.html`
**זרימה:** יעל קוראת קובץ → משכתבת → שומרת תוצר ב-`Output/` → מעבירה מקור ל-`Content/Ready/`.

### `Content/Ready/`
**תפקיד:** ארכיון — מאמרי גלם לאחר עיבוד. יעל מעבירה לכאן את הקובץ המקורי בסיום הטיפול.

---

## `Output/` — תוצרים מוכנים

**תפקיד:** תיקיית הפלט המאוחדת של הפרויקט.
| תוצר | מי מייצר | פורמט שמות |
|------|----------|------------|
| מאמרים משוכתבים | יעל | `<שם-מקורי>.md` |
| תמונות | יובל (דרך nano-banana-2) | `<נושא>-<YYYY-MM-DD>.png` |

---

## `.claude/commands/` — פקודות Slash

**תפקיד:** פקודות slash מותאמות אישית לפרויקט (מ-Superpowers).

| פקודה | תפקיד |
|-------|--------|
| `/brainstorm` | חקירת כוונות ודרישות לפני מימוש |
| `/write-plan` | כתיבת תוכנית עבודה מפורטת |
| `/execute-plan` | ביצוע תוכנית מאושרת עם sub-agents |

---

## `.claude/hooks/` — Hooks

**תפקיד:** סקריפטים שרצים אוטומטית באירועים של Claude Code.

| קובץ | תפקיד |
|------|--------|
| `session-start` | bash script — מזריק את `using-superpowers` skill לתחילת כל סשן |
| `run-hook.cmd` | wrapper חוצה-פלטפורמות (Windows/Unix) להרצת hook scripts |

מוגדר ב-`settings.json` תחת `hooks.SessionStart`.

---

## `.env`
**תפקיד:** משתני סביבה — API keys וקונפיגורציה רגישה.
**לא מועלה ל-git.** יש למלא את הערכים האמיתיים לפני שימוש.

| משתנה | שימוש |
|-------|-------|
| `GEMINI_API_KEY` | גישה ל-Google Nano Banana 2 דרך ה-MCP |

---

## `docs/`
**תפקיד:** מסמכי תכנון ו-PRD של הפרויקט.

| קובץ | תפקיד |
|------|--------|
| `PRD-ceo-agent.md` | מסמך דרישות מוצר של סוכן המנכ"ל — מטרות, FR, לוגיקת ניתוב, שאלות פתוחות |
| `PROJECT-STRUCTURE.md` | המסמך הנוכחי — מבנה הפרויקט |

---

## `vault/`
**תפקיד:** הזיכרון ארוך-הטווח של Claude Code. מתועדים כאן כל ההחלטות, ה-session logs, וההקשרים של כל עבודה שנעשתה.
נקרא בתחילת כל משימה ומתעדכן בסיומה (דרך `obsidian-vault-workflow`).

```
vault/
├── File Reference/      ← תיעוד מה עושה כל קובץ בפרויקט
└── Meeting Notes/       ← session logs לפי נושא
```

### `vault/File Reference/`
**תפקיד:** מסמך MD לכל קובץ בפרויקט — מה הוא עושה, למי שייך, וקישורים לקבצים קשורים.

| קובץ | מתעד את |
|------|---------|
| `_index.md` | אינדקס של כל הקבצים בתיקייה |
| `claude-md.md` | תיעוד `.claude/CLAUDE.md` |
| `skills-gitkeep.md` | תיעוד `.claude/skills/.gitkeep` |
| `agents-gitkeep.md` | תיעוד `.claude/agents/.gitkeep` |
| `obsidian-vault-workflow-skill.md` | תיעוד ה-Skill של vault-workflow |

### `vault/Meeting Notes/`
**תפקיד:** Session logs — תיעוד כרונולוגי של כל עבודה לפי נושא.

| קובץ | מתעד את |
|------|---------|
| `_index.md` | אינדקס של כל ה-session logs |
| `project-file-documentation.md` | סשן ראשוני — מיפוי כל קבצי הפרויקט |
| `ceo-agent-prd.md` | יצירת ועדכוני סוכן המנכ"ל |
| `nano-banana-2-yuval-setup.md` | יצירת Skill nano-banana-2 וסוכן יובל |
| `skill-creator-install.md` | התקנת skill-creator מ-Anthropic GitHub |

---

## `.git/`
**תפקיד:** ניהול גרסאות Git. מנוהל אוטומטית — אין לערוך ידנית.

## `.obsidian/`
**תפקיד:** הגדרות אפליקציית Obsidian (תצוגה, plugins, פאנלים). אוטומטי — אין לערוך ידנית.
