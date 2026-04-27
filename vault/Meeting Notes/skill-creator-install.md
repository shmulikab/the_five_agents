# Skill Creator — התקנה

## Overview

התקנת ה-Skill הרשמי `skill-creator` של Anthropic מ-GitHub לתוך הפרויקט. ה-Skill מספק כלי מלא ליצירה, בדיקה ואופטימיזציה של Skills חדשים — כולל סוכני eval (grader/comparator/analyzer), סקריפטי Python, ו-HTML viewer לתוצאות.

## Open Questions

- none

## Session Log

### 2026-04-27 — התקנת skill-creator מ-anthropics/skills [shipped]

- **What was done:** הורדנו את `skills/skill-creator` מ-`https://github.com/anthropics/skills` דרך git sparse-checkout (depth 1) לתיקייה זמנית, והעתקנו ל-`.claude/skills/skill-creator/`. הותקנו 18 קבצים: SKILL.md, LICENSE, 3 agents, 8 scripts, assets, eval-viewer, references.
- **Decisions:** שיטת sparse-checkout נבחרה כדי להוריד רק את התיקייה הרצויה ולא את כל ה-repo.
- **Notes / Caveats:** המבנה כולל תיקיית `eval-viewer/` נוספת שלא הייתה במפת הקבצים המקורית — היא הועתקה אף היא. ה-Skill דורש Python להרצת הסקריפטים.
- **Related:** [[project-file-documentation]], [[ceo-agent-prd]]
