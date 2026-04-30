# CourseMaster Output Formats

Use these formats when the user asks CourseMaster to summarize PPT/PDF course materials for exam preparation. Unless the user explicitly chooses English output, user-facing headings, prompts, and explanatory text should be written in Chinese.

## Confirmable Outline

Produce the outline in the conversation. Keep it compact, structured, and easy for the user to edit.

Recommended structure:

```markdown
# CourseMaster Review Outline

## Assumptions
- Subject: ...
- Material language: ...
- Output language: ...
- File/chapter rule: ...

## File and Chapter Map
| Chapter | Source file | Page/slide range | AI structure judgment |
|---|---|---:|---|
| 1. ... | ... | ... | ... |

## Chapter 1: ...

### Core priorities
- **Point:** English technical term (中文翻译) ...
  - Why it matters: ...
  - Source: `file.pdf, pp. 3-8`

### Priority logic summary
In 2-4 concise sentences, summarize how the core priorities relate to each other and what learning logic the chapter follows.

### Lower-priority content
- ...

### Judgment logic
- ...
```

When the output language is Chinese and a core priority includes an English professional term, preserve the English term and add a Chinese translation in parentheses on first mention. If the Chinese translation is uncertain or discipline-specific, mark it as tentative, such as `priming (启动效应，译名待确认)`.

End with:

```markdown
请直接回复你想修改的地方，我会更新这份大纲；如果确认无误，请输入 `expand into details` 生成学习文件。
```

## Study Guide Markdown

The Markdown version should be readable without custom styling.

Use this required section order. Do not omit these sections unless the source files genuinely cannot support them:

1. Title
2. Notes / assumptions section: course subject, material language, output mode, file/chapter rule, teacher instructions, reliability notes, image-heavy or low-confidence extraction notes.
3. Course Map: a table mapping chapter number, topic, and source file/page range.
4. Study-guide depth: `Concise Guide` or `Standard Guide`.
5. Learning Objectives Overview: 5-9 bullets that synthesize what the whole guide should help the user master. These should be learning goals, not a file list.
6. Chapter sections following the confirmed outline.
7. Quick Review Table: a compact table with columns like `主题`, `最该掌握的问题`, and `关键词`.
8. Source Index: one bullet per source file summarizing what that file contributes.

Each chapter section must use this order:

1. `Core`
2. Learning-item blocks using labels such as `Concept:`, `Theory:`, `Example:`, `Formula:`, `Plain-language explanation:`, and `Common mistake:`
3. `Lower Priority`
4. `Logic Summary`

Use labels consistently and always include a colon:

- `Concept:`
- `Formula:`
- `Theory:`
- `Example:`
- `AI note:`
- `Common mistake:`
- `Plain-language explanation:`

Depth rules:

- Concise Guide: use priority lists plus brief explanations. Keep it suitable for first-pass understanding, quick exam review, or studying alongside the original course materials.
- Standard Guide: match or exceed the depth of a strong course review guide. For each important concept, classification, stage, model, formula, or theory, include what it means, what its main parts do, why it matters in the chapter, and how those parts connect. If this explanation is not directly available in the source material, put it under `AI note:` and keep it concise.

Logic Summary rules:

- Include a `Logic Summary` for the outline and for every chapter in the final guide.
- Write it as synthesis, not as a generic recap.
- Explain the relationship among the chapter's key points, such as mechanism, sequence, contrast, evidence chain, or central problem.
- End with a useful study frame, such as "复习时应按..." or "考试应优先掌握...".
- Prefer precise connective language: `因为`, `所以`, `这说明`, `核心区别是`, `后续章节可以看作`, `复习时应按`.
- Avoid vague summaries that only say the chapter is about a topic.

Good style example:

```text
视觉意识章节的核心是 dissociation（分离）。课件通过非注意盲、变化盲、掩蔽、两可图、双眼竞争和适应说明：stimulus、neural processing 和 subjective awareness 并不总是一一对应。复习时应按“现象是什么、说明了什么分离、如何用于研究意识”来整理。
```

Keep source-derived content and AI-added content visually separate. Put AI-added learning support in labeled notes only.

## Study Guide HTML

The HTML file is the polished reading version. Use embedded CSS so the file can be opened directly in a browser.

Use this default visual template unless the user requests another style. Keep the same quiet, academic reading feel:

- Light gray page background with a centered `main` column.
- A white `hero` panel at the top with the guide title, one muted subtitle, and a wrapped table-of-contents made of small rounded links.
- The table of contents must link to Notes/说明, Course Map, Learning Objectives Overview, every chapter, Quick Review Table, and Source Index.
- Include the required sections from the Markdown structure in the HTML too. Do not drop Notes/说明, Course Map, Learning Objectives Overview, per-chapter Logic Summary, Quick Review Table, or Source Index.
- Course map and review tables as white tables with subtle borders.
- Each learning item as a white `.block` with a subtle border and a 5px colored left border.
- Keep sources outside or immediately below the relevant block as plain `Source: <code>...</code>` text.
- Avoid large decorative cards, gradients, illustrations, heavy shadows, large badges, or dense dashboard-like layouts.

Use this CSS baseline, adapting only spacing or selectors when necessary:

```html
<style>
:root{--bg:#f7f8fb;--paper:#fff;--text:#172033;--muted:#5f6b7a;--line:#dfe5ee;--blue:#2f6fed;--teal:#087f8c;--green:#188038;--amber:#a05a00;--red:#b42318;--purple:#6941c6;--gray:#667085}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--text);font:16px/1.65 -apple-system,BlinkMacSystemFont,"Segoe UI",Arial,"Noto Sans CJK SC","PingFang SC",sans-serif}
main{max-width:1080px;margin:0 auto;padding:32px 20px 64px}
.hero{background:var(--paper);border:1px solid var(--line);border-radius:8px;padding:26px 28px;margin-bottom:18px;box-shadow:0 8px 24px rgba(16,24,40,.06)}
h1{font-size:30px;line-height:1.25;margin:0 0 10px}
h2{font-size:23px;line-height:1.35;margin:34px 0 12px;padding-top:10px;border-top:1px solid var(--line)}
h3{font-size:18px;margin:24px 0 10px}
p{margin:8px 0}
ul{padding-left:22px}
li{margin:6px 0}
code{background:#eef2f7;border:1px solid #dde3ec;border-radius:5px;padding:1px 5px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:.92em}
table{border-collapse:collapse;width:100%;margin:14px 0;background:var(--paper);border:1px solid var(--line);border-radius:8px;overflow:hidden;display:table}
th,td{border:1px solid var(--line);padding:9px 10px;vertical-align:top}
th{background:#eef4ff;text-align:left}
.toc{display:flex;flex-wrap:wrap;gap:8px;margin-top:14px}
.toc a{color:#1d4ed8;text-decoration:none;background:#eef4ff;border:1px solid #d7e4ff;border-radius:999px;padding:4px 10px}
.block{background:var(--paper);border:1px solid var(--line);border-left:5px solid var(--gray);border-radius:8px;padding:12px 14px;margin:12px 0}
.concept{border-left-color:var(--blue)}
.formula{border-left-color:var(--purple)}
.theory{border-left-color:var(--teal)}
.example{border-left-color:var(--green)}
.ai-note{border-left-color:var(--gray)}
.mistake{border-left-color:var(--amber)}
.plain{border-left-color:var(--red)}
.answer{background:#fbfcff;border:1px solid var(--line);border-radius:8px;padding:10px 12px;margin:8px 0 18px}
.q{background:var(--paper);border:1px solid var(--line);border-radius:8px;padding:14px 16px;margin:14px 0}
.muted{color:var(--muted)}
strong{font-weight:700}
@media(max-width:680px){main{padding:20px 12px 44px}.hero{padding:20px 16px}h1{font-size:25px}h2{font-size:20px}table{font-size:14px;display:block;overflow-x:auto}th,td{min-width:120px}}
</style>
```

Use this block structure for learning items:

```html
<div class="block concept">
  <p><strong>Concept:</strong> <strong>Visual perception（视觉知觉）</strong></p>
  <p>...</p>
</div>
<p>Source: <code>visual perception.pdf, pp. 4-5</code></p>
```

Role classes and colors:

- `concept`: blue left border
- `formula`: purple left border
- `theory`: teal left border
- `example`: green left border
- `mistake`: amber left border
- `plain`: red left border
- `ai-note`: gray left border

Always include the colon in the visible label, such as `Concept:`, `Example:`, and `AI note:`. Avoid making the page colorful for its own sake. Color should support scanning and reduce cognitive load.

HTML chapter skeleton:

```html
<h2 id="Chapter-1-...">Chapter 1: ...</h2>
<h3>Core</h3>
<div class="block concept">...</div>
<p>Source: <code>...</code></p>
<div class="block plain">...</div>
<div class="block mistake">...</div>
<h3>Lower Priority</h3>
<ul>...</ul>
<h3>Logic Summary</h3>
<p>...</p>
```

## Practice Questions

Create mostly multiple-choice questions and some true/false questions.

Recommended distribution:

- 80-90% multiple-choice
- 10-20% true/false

Question count should scale with source size and priority:

- Small deck or chapter: 8-12 questions
- Medium chapter: 12-20 questions
- Large or high-priority chapter: 20+ questions when useful

Multiple-choice format:

```markdown
### Q1. ...

A. ...
B. ...
C. ...
D. ...

**Answer:** B
**Explanation:** ...
**Tested point:** ...
**Source:** `file.pdf, p. 12`
```

True/false format:

```markdown
### Q9. True or false: ...

**Answer:** True
**Explanation:** ...
**Tested point:** ...
**Source:** `slides.pptx, slide 18`
```

Coverage rules:

- Cover all confirmed core priorities.
- Include some lower-priority content only when it is useful for discrimination or likely confusion.
- Avoid trick questions that depend on wording rather than understanding.
- Make distractors plausible but not misleading.
- Do not cite pages/slides that do not support the answer.
