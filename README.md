# CourseMaster Skill

## 中文版本介绍

CourseMaster 是一个 Codex skill，用于将课程 PPT/PDF 材料转换成适合考试复习的**学习指南**和**练习题**。

**它适用于这样的工作流：学生上传一份或多份课程文件，先查看生成的大纲并按需要修改大纲，然后让 Codex 将确认后的大纲展开成排版清晰的学习文件。**

## 🧩功能

- 读取 PPT/PPTX/PDF 课程材料，支持中英双语

- 创建用于确认的 Markdown 复习大纲，**支持用户修改大纲**

- **区分核心重点和低优先级内容**，并**解释重点判断背后的逻辑**

- 📖生成学习指南 `study-guide.html` 和 `study-guide.md`，内容包括：

  > - 📝**说明 / Notes**
  >   课程学科、课件语言、输出语言、文件划分规则、老师给出的考试范围说明，以及可靠性说明
  > - 🗺️**Course Map**
  >   课程地图，用表格列出每一章/文件对应的主题、来源文件和页码范围。
  > - 🪄**Learning Objectives Overview**
  >   学习目标总览，用几条要点概括整份指南希望你掌握什么。
  > - 🗂️**Chapter Sections**
  >   每章的详细复习内容，通常包括：
  >   - Core：*核心概念、理论、公式、例子、易错点、AI note、通俗解释*
  >     - 📑***标注式学习块**：核心内容会用不同标签区分*
  >   - Lower Priority：相对低优先级内容，以及为什么可以降低优先级
  >   - Logic Summary：总结本章重点之间的关系、主线逻辑和复习框架
  > - 📒**Quick Review Table**
  >   快速复习表，通常包括主题、最该掌握的问题和关键词，方便考前快速过一遍。
  > - 📍**Source Index**
  >   来源索引，按文件列出每份课件主要贡献了哪些知识点。

- ✍️生成模拟试题 `practice-questions.html` 和 `practice-questions.md`

  - 题型为**选择题**与少量**判断题**

- 将 AI 添加的学习辅助内容与课件来源内容分开标注

- 在可用时使用文件名和页码/幻灯片编号添加来源引用

## 🔗项目结构

```text
course-master-skill/
├── README.md
└── course-master/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        └── output-formats.md
```

## 🕹️安装

将 `course-master/` 文件夹复制到本地 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -R course-master ~/.codex/skills/
```

复制完成后，重启 Codex 或打开一个新对话，让 Codex 发现这个 skill。

## 🌟演示

```text
Use $course-master to summarize the PPT/PDF files in this folder for my exam.
```

CourseMaster 会先询问学科、材料语言、输出语言，以及老师是否对考试范围有特别说明。之后它会创建一份复习大纲。你**<u>修改或确认大纲</u>**后，输入：

```text
expand into details
```

Codex 默认会在 `CourseMaster-output` 文件夹中生成学习包。



## English Version Introduction

CourseMaster is a Codex skill for turning course PPT/PDF materials into exam-ready **study guides** and **practice questions**.

**It is designed for workflows where a student uploads one or more course files, reviews the generated outline and edits it as needed, then asks Codex to expand the confirmed outline into polished study files.**

## 🧩Features

- Reads PPT/PPTX/PDF course materials, with support for Chinese and English

- Creates a Markdown review outline for confirmation, **with support for user edits to the outline**

- **Separates core priorities from lower-priority content**, and **explains the judgment logic behind priority decisions**

- 📖Generates study guides `study-guide.html` and `study-guide.md`, including:

  > - 📝**Notes**
  >   Course subject, material language, output language, file/chapter rule, teacher instructions about exam scope, and reliability notes
  > - 🗺️**Course Map**
  >   A course map that uses a table to list the topic, source file, and page range for each chapter/file.
  > - 🪄**Learning Objectives Overview**
  >   A learning-objectives overview that summarizes what the full guide is meant to help you master.
  > - 🗂️**Chapter Sections**
  >   Detailed review content for each chapter, usually including:
  >   - Core: *core concepts, theories, formulas, examples, common mistakes, AI notes, and plain-language explanations*
  >     - 📑***Labeled learning blocks**: core content is distinguished with different labels*
  >   - Lower Priority: relatively lower-priority content and why it can be deprioritized
  >   - Logic Summary: a synthesis of the relationships among key points, the chapter's main logic, and the review frame
  > - 📒**Quick Review Table**
  >   A quick review table, usually including topics, the most important questions to master, and keywords for fast exam review.
  > - 📍**Source Index**
  >   A source index that lists what each course file mainly contributes.

- ✍️Generates practice questions `practice-questions.html` and `practice-questions.md`

  - Question types are mainly **multiple-choice questions**, with a small number of **true/false questions**

- Marks AI-added learning support separately from source material

- Adds source citations using file name and page/slide number when available

## 🔗Repository Structure

```text
course-master-skill/
├── README.md
└── course-master/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        └── output-formats.md
```

## 🕹️Installation

Copy the `course-master/` folder into your local Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R course-master ~/.codex/skills/
```

After copying, restart Codex or open a new conversation so the skill can be discovered.

## 🌟Example Use

```text
Use $course-master to summarize the PPT/PDF files in this folder for my exam.
```

CourseMaster will first ask about the subject, material language, output language, and any teacher instructions about exam scope. It will then create a review outline. After you **<u>revise or confirm the outline</u>**, type:

```text
expand into details
```

Codex will then generate the study package in a `CourseMaster-output` folder by default.
