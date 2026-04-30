---
name: course-master
description: Exam preparation from course PPT/PDF materials. Use when the user wants Codex to process one or more lecture slide decks or PDFs, summarize chapters or sections, identify core exam-relevant points and lower-priority content, create a review outline for user confirmation, expand the confirmed outline into clean HTML/Markdown study guide files, and generate multiple-choice plus true/false practice questions with answers and source page citations.
---

# CourseMaster

## Overview

Use CourseMaster to turn PPT/PDF course materials into an exam-ready study package. Work in two phases: first produce a review outline for user confirmation, then expand the approved outline into study-guide and practice-question files.

Use Chinese for user-facing conversation by default. Ask about language and subject before analysis, and switch to English only if the user explicitly chooses English output. Keep course-source content separate from AI-added learning support.

## Required Start Questions

Before processing files, ask concise questions in Chinese if the user has not already answered them:

1. 这门课的学科或专业方向是什么？
2. 课件的主要语言是什么？
3. 希望总结使用哪种语言？
   - 中文总结
   - 英文总结
   - 中文总结，但保留核心英文术语
4. 老师是否明确说过哪些内容重点考、不考或低优先级？
5. PPT/PDF 是否都在同一个文件夹里？是否通常一个文件对应一章？
6. 大纲确认后，学习手册希望使用哪种深度？
   - Concise Guide：重点清单 + 简短解释，适合入门、考前快速过，或拿着 guide 对照课件自学。
   - Standard Guide：对核心概念、分类、阶段、模型、公式和理论做适度深入解释。

If the user wants to proceed without answering every question, continue with reasonable assumptions and state them briefly in Chinese.

## Input Handling

Accept PPT, PPTX, and PDF files. Support a folder containing many course files.

Default chapter rule:

- Treat each file as one chapter or major section.
- Split a file into multiple sections only when headings, table of contents slides, section dividers, or page structure strongly indicate it.
- Merge files only when filenames, titles, or content clearly show they belong to the same chapter.
- Record the basis for any split or merge in the outline's judgment logic.

Preserve source traceability. When possible, attach claims, key points, examples, and question answers to `file name + page/slide number`.

## Workflow

### 1. Build a Course Map

Scan the file set and infer:

- File order and likely chapter order
- Chapter or section titles
- Page/slide ranges
- Content density and repeated themes
- Definitions, formulas, theories, examples, diagrams, and marked exam hints
- Explicit low-priority signals such as "not tested", "optional", "background", "for interest", or very small coverage

If extraction quality is poor, say so and ask for clearer files or permission to proceed with limited confidence.

### 2. Produce a Confirmable Outline

Output a Markdown outline in the conversation before creating full study files. Use the format in `references/output-formats.md`.

For each chapter or section, include:

- Core priorities: concise bullets for the most important material.
- Term translation: when a core priority contains an English technical term, keep the English term and add a concise Chinese translation in parentheses, such as `working memory (工作记忆)`.
- Priority logic summary: after listing core priorities, add a short logical summary that explains how the listed priorities connect to each other and what the chapter is fundamentally trying to teach.
- Lower-priority content: concise bullets or one-sentence notes.
- Judgment logic: brief reasons for the priority split.

Judge priority using both content signals and reasoning:

- Content share, page/slide count, and density
- Repetition across files or within a deck
- Heading level, summary slides, learning objectives, and review slides
- Definitions, formulas, models, theories, workflows, or named concepts
- Teacher/exam signals written in the source
- Subject-specific expectations based on the user's stated discipline

Keep the outline compact and easy to edit. After the outline, pause and ask the user in Chinese to reply with edits or type `expand into details` to continue.

### 3. Revise Until Confirmed

When the user gives edits, update the outline instead of expanding immediately. Preserve user corrections, especially teacher instructions about exam scope. Continue this loop until the user confirms or says `expand into details`.

### 4. Create the Study Package

After confirmation, create an output folder named `CourseMaster-output` unless the user specifies another location. Generate:

- `study-guide.html`
- `study-guide.md`
- `practice-questions.html`
- `practice-questions.md`

Use HTML as the primary polished reading version and Markdown as the editable backup. Follow `references/output-formats.md` for structure and visual conventions.

For HTML, use the default template in `references/output-formats.md` unless the user requests a different visual style. Do not redesign the page from scratch.

### 5. Expand Into a Study Guide

Before expansion, use the user's selected depth. If the user has not selected one, ask after the outline is confirmed. Default to Standard Guide only if the user wants to proceed without choosing.

Follow the confirmed outline. For priority content, explain concepts in a logical, learnable sequence. Include only a light amount of AI-added support so the guide does not become cognitively heavy.

Use `references/output-formats.md` as the single source of truth for guide depth rules, required guide sections, chapter structure, labels, Logic Summary style, and HTML visual template.

Mark any content that is not directly from the course material as `AI note`. Do not blend outside explanation with source material without labeling it.

Keep the layout clean:

- Prefer short sections, tables, callout boxes, and bullets over long paragraphs.
- Avoid decorative illustrations and excessive color.
- Use color only to distinguish learning roles such as concepts, formulas, examples, warnings, and AI notes.
- Avoid dense walls of text.

### 6. Generate Practice Questions

Create mostly multiple-choice questions plus some true/false questions. Cover the important knowledge points broadly, with more questions for higher-priority sections.

For each answer, include:

- Correct answer
- Brief explanation
- Tested point
- Source citation as `file name, page/slide number`

Do not invent source citations. If a citation cannot be determined, mark it as `source uncertain` and explain why.

## Reliability Rules

- Prefer source-grounded statements over broad textbook knowledge.
- Explicitly separate course content, inferred priority, and AI-added learning support.
- Do not claim that something will or will not be on an exam unless the source or user says so.
- If teacher instructions conflict with model judgment, prioritize teacher instructions and mention the conflict.
- Preserve uncertainty instead of filling gaps with confident guesses.

## Reference

Read `references/output-formats.md` when producing the confirmable outline, HTML/Markdown study guide, or practice questions.
