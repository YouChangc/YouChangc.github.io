---
name: obs-to-hugo
description: Convert one or more Obsidian notes into a Hugo blog draft. Use when the user wants to turn local notes into a publishable technical blog post, save it under content/posts/, preserve the original meaning, and leave the result as a draft for human review. Do not use for general writing, casual note cleanup, or direct publishing.
---

# Purpose

Turn Obsidian Markdown notes into a Hugo-compatible blog draft inside this repository.

This skill is for a human-in-the-loop workflow:
1. Read source notes from Obsidian, either directly from workspace files or via the configured Obsidian MCP server.
2. Convert the notes into a coherent technical blog post.
3. Choose the correct post subdirectory under content/posts/
4. Default to `draft: true`.
5. Never publish automatically unless the user explicitly asks.

# When to use

Use this skill when the user asks for things like:
- “把这篇 Obsidian 笔记整理成博客”
- “根据我的笔记生成 Hugo 草稿”
- “把这些学习记录改成一篇技术文章”
- “从 Obsidian 里找一篇笔记，写到博客仓库里”

Do not use this skill when:
- The user only wants a summary
- The user wants freeform brainstorming
- The user wants to publish immediately without review
- The task is unrelated to Hugo blog writing

# Inputs

Expected inputs may include:
- One Obsidian note
- Multiple related Obsidian notes
- A note path, title, keyword, or topic
- Existing Hugo repo structure and conventions

If multiple notes are given, merge only notes that clearly belong to one topic.
If the topic is too broad, produce one focused article rather than a sprawling summary.

# Required workflow

## 1. Gather source material

Find and read the relevant Obsidian note content.

Preferred order:
1. Use the Obsidian MCP server if the user refers to notes in the vault by topic, title, or recency.
2. Use local workspace files directly if the notes are already available in the repo or working directory.
3. If multiple candidate notes are found, choose the most relevant one or the smallest coherent set.

Always preserve the source meaning.
Do not invent claims, examples, or conclusions that are not supported by the notes.

## 2. Decide whether the note is blog-worthy

A note is suitable if it has a clear technical theme and enough substance to form a useful article.

Good candidates:
- concept explanations
- study notes with clear takeaways
- implementation lessons
- tool comparisons
- project design notes
- tutorial-like material

Weak candidates:
- TODO fragments
- incomplete bullet scraps
- purely private notes
- notes with no clear audience value

If the source is weak, do one of these:
- turn it into a short blog draft with a narrow scope
- or explain briefly why it should stay as notes instead of a blog post

## 3. Rewrite into a technical blog structure

Transform the source notes into a coherent article with:
- a clear title
- an opening paragraph explaining the topic and why it matters
- logically ordered sections
- concise transitions between sections
- preserved code blocks and technical terms
- a short conclusion or takeaway section when useful

Prefer practical clarity over flashy writing.

## 4. Follow Hugo format

Save the article as Markdown under content/posts/:
Before creating the Hugo Markdown file, inspect the existing subdirectories under content/posts/ and place the new post into the most appropriate small-category directory.

Rules:
	•	Prefer an existing subdirectory if it matches the article’s practical topic or usage context.
	•	If no suitable subdirectory exists, create a new one with a concise, stable, lowercase slug.
	•	Organize by practical category, not by broad technical buzzwords alone.
	•	Use small, reader-friendly categories such as development, backend, ai-engineering, security, network, database, tools, or other repo-consistent categories.
	•	Do not create a top-level directory only because the article mentions a broad topic like llm, ai, or agent.
	•	Broad topics such as LLM, MCP, RAG, Agent, Go, or Hugo should usually appear in tags, not necessarily as directory names.
	•	Example: if an article is about using LLMs in engineering practice, place it under something like development/ or ai-engineering/, not llm/ unless the repository already uses llm/ as an established small-category directory.

Output path should follow this pattern:
	•	content/posts/<subcategory>/YYYY-MM-DD-slug.md

When deciding the directory:
	1.	Inspect existing directories first.
	2.	Reuse an existing one whenever reasonable.
	3.	Only create a new subdirectory if none fits well.
	4.	Keep naming consistent with the repository’s current structure.

Use Hugo front matter at the top.

Required front matter fields:
- `title`
- `date`
- `tags`
- `categories`
- `summary`
- `draft`

Default:
- `draft: true`

Use ISO-like datetime with timezone when possible.

## 5. Writing style

Write in clear technical prose.

Style rules:
- preserve the author’s actual meaning
- do not over-polish into marketing language
- avoid generic AI filler
- avoid exaggerated claims
- explain jargon briefly when needed
- keep examples concrete
- keep code blocks unchanged unless fixing obvious formatting
- prefer precise section headings

If the source note is in Chinese, write the draft in Chinese unless the user asks for English.
If the repo clearly uses another language, follow repo conventions.

## 6. Metadata rules

Generate metadata conservatively.

### Title
- Specific and technical
- Reflect the actual scope
- No clickbait

### Tags
- 3 to 6 tags
- Prefer concrete technical tags over vague ones

### Categories
- Use one primary category
- Follow existing repo conventions if visible

### Summary
- 1 to 2 sentences
- State what the article explains or solves

## 7. Image handling

Do not generate images by default.

If the article would benefit from visuals, add a short inline note such as:
> 插图建议：这里适合加入一张展示 X → Y → Z 流程的图

If the repository already uses Mermaid and the user asks for it, you may add a Mermaid diagram.

## 8. Safety and publishing rules

Never set `draft: false` unless the user explicitly asks for a publish-ready final version.

Do not push, deploy, or publish unless explicitly asked.

If editing the repo:
- modify only the intended post file and closely related assets
- do not make unrelated formatting changes

# Output contract

When this skill completes successfully, it should:
1. create or update exactly one Hugo draft post unless the user requested multiple posts
2. place the file in `content/posts/`
3. report:
   - source note(s) used
   - output file path
   - major assumptions, if any
   - any places that need human review

# Quality bar

Before finishing, verify:
- the article matches the source notes
- the structure is coherent
- front matter is valid
- the filename is reasonable
- `draft: true` is set unless explicitly overridden
- no unsupported factual additions were introduced