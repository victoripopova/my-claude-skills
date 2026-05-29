---
name: publish-notion
description: Publishes any Markdown document to Notion — creating a new page or updating an existing one. Use this skill whenever the user wants to send, sync, push, upload, or update any .md document (PRD, spec, report, notes, changelog, brief, or any other document) to Notion. Trigger even for casual requests like "put this in Notion", "create a Notion page for this", "update the Notion doc", or "sync my doc". Applies Notion-native formatting (callouts, toggles, dividers, coloured headings) beyond basic Markdown to make the page look polished.
compatibility: Requires Notion MCP connected (notion-search, notion-update-page, notion-create-pages, notion-fetch)
---

# Notion Markdown Publisher

Takes any Markdown document — from a file path, an upload, or content already in context — and publishes it to Notion as a well-formatted page. Applies Notion-native styling beyond basic Markdown to produce polished output.

## Inputs

The user provides:
- **Document source** — one of:
  - A file path (e.g. `/mnt/user-data/outputs/my-doc.md` or an uploaded `.md` file)
  - Content already in the conversation context
- **Notion page name** — the title to search for or create. If not provided, derive from the document's `# Title` heading.
- **Parent page** (optional) — where to create the page if it doesn't exist yet. Ask if not provided and page doesn't exist.

## Steps

### 1. Read the document
- If a file path was given, read it with the `view` tool.
- If content is already in context (e.g. just created), use it directly.
- Extract the page title from the `# H1` heading, or ask the user if absent.

### 2. Clean the content
Strip elements Notion manages as page properties, not body content:
- The top-level `# Title` heading (Notion shows this automatically)
- Any metadata table at the top (Created / Tags / Status rows)

### 3. Find or create the Notion page

**Search first:**
Use `notion-search` with the page title as the query.

- **Single clear match** → proceed with that page ID
- **Multiple similar matches** → show the options to the user and ask which one to update
- **No match** → ask the user to confirm creating a new page, and under which parent (if not already provided). Then use `notion-create-pages`.

### 4. Apply Notion-native formatting

Before publishing, enrich the cleaned Markdown with Notion-specific formatting. Always fetch `notion://docs/enhanced-markdown-spec` first to get the exact syntax. Then apply the following rules:

#### Callouts
Wrap important notices, warnings, or key takeaways in callout blocks:
```
> [!NOTE] icon="💡"
> Key insight or important context here.
```
Use these for: hypotheses, open questions, risks, key decisions, or any standalone "important" sentence.

#### Dividers
Only use `---` dividers as an exception on very long pages where sections would otherwise blur together. Do not add dividers by default.

#### Toggles (collapsible blocks)
Use toggles for detail-heavy content that isn't needed at a glance:
```html
<details>
<summary>Section title</summary>
Content here
</details>
```
Good candidates: long lists of metrics, dev implementation details, post-launch notes.

#### Coloured section headings
Do not use coloured headings by default. Only apply colour to `##` headings as an exception — for example, when the user explicitly requests it or when the document type clearly benefits from colour-coded sections. If used, keep it consistent: 1 colour per section type throughout the document.

#### Standard Markdown (always applies)
- `## Heading` → H2
- `### Subheading` → H3
- `- bullet` → bulleted list
- `1. item` → numbered list
- `**bold**` → bold
- `` `code` `` → inline code
- ` ```code block``` ` → code block

### 5. Publish

**Updating an existing page:**
Use `notion-update-page` with `command: replace_content` and pass the formatted Markdown as `new_str`.

**Creating a new page:**
Use `notion-create-pages` with the formatted content and the page title under `properties.title`.

### 6. Confirm
Tell the user the page was published and provide the Notion URL.

## Error Handling

- **`replace_content` fails due to child pages** — show the affected child pages to the user and ask for confirmation before retrying with `allow_deleting_content: true`. Never assume deletion is OK.
- **File not found** — tell the user the path wasn't found and ask them to confirm the location or paste the content directly.
- **Ambiguous page match** — always ask the user to pick; never guess.

## Formatting Judgement

Not every document needs every Notion feature. Apply formatting proportionally:
- Short, simple docs (meeting notes, changelogs) → minimal callouts only
- Structured docs (PRDs, specs, briefs) → callouts for open questions + toggles for dev/metrics detail
- Reference docs (glossaries, runbooks) → toggles throughout for each entry
- Very long docs (any type) → dividers between sections, as an exception
- When explicitly requested or clearly warranted → coloured headings, applied consistently

The goal is a page that looks intentional and readable in Notion — not one that uses every feature available.
