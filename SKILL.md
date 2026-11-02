---
name: sqwiki-article-writer
description: Research, draft, and expand encyclopedic articles in Albanian for Albanian Wikipedia (sq.wikipedia.org), delivered as copy-ready MediaWiki wikitext with sourced citations that carry exact |quote= excerpts. Use when the user asks to write, draft, research, or expand an Albanian Wikipedia article about an institution, festival, building, organisation, place, event, or similar subject, or mentions sqwiki, sq.wikipedia, or "artikull për Wikipedia". For translating an existing English Wikipedia article, use enwiki-sqwiki-translation instead.
---

# sqwiki-article-writer

Write original, well-sourced Albanian encyclopedic articles. Output is complete MediaWiki wikitext unless the user asks otherwise.

## Scope

- Give a balanced overview: what the subject is, its history, main characteristics, functions or activities, and significance, as the sources support.
- Keep the subject at the centre. For institutions, festivals, buildings, organisations and similar subjects, mention people only when needed to explain the subject's development. No mini-biographies.
- Keep details of lasting value. Leave out tangents, anecdotes, routine announcements, ceremonial speeches, attendee lists, and minor administrative detail.
- Match length to the evidence. No padding, repetition, trivia, or artificial sections. A short article is fine.

## Workflow

1. **Research first.** Read sources directly. Search snippets are leads, not evidence. Search in Albanian and other relevant languages, and try alternative names and historical spellings.
2. **Assess sources.** Prefer independent secondary sources with substantial coverage. Judge each article on its own merits. See `references/source-guide.md` for the starting-point list and the rules on primary, promotional, and derivative material.
3. **Check the sqwiki conventions** before drafting (see "Verification" below).
4. **Draft** the article in the structure below.
5. **Run the final review** and fix problems before delivering.

If independent coverage is insufficient, say so briefly to the user. Do not manufacture significance. Tell the user when you are unsure about a fact, a source, or a template.

## Citations and quotations (mandatory)

- Support every substantive claim with an inline reference next to the text it supports.
- **Every citation has a `|quote=`** with a short, exact excerpt from the source, in the source's original language and wording. Never paraphrase or translate inside `|quote=`. Keep it proportionate and within copyright limits.
- Write the article body in your own Albanian prose. Do not repeat the excerpt in the body.
- Any source wording reproduced in the body goes in quotation marks, with attribution and a reference. Use direct quotations sparingly.
- Never invent quotations, citation metadata, page numbers, dates, or URLs. If the wording cannot be verified, find an accessible alternative source or omit the claim.
- Reuse named references (`<ref name="..."/>`) only where the source supports every attached claim. A reused name needs its full definition once.
- Separate established fact from allegation, recollection, and assessment. Present conflicting accounts explicitly and in proportion. Attribute interviewees' claims.
- Do not cite Wikipedia, Wikidata, other Wikimedia pages, or AI-generated text. Use them only to find sources.
- Do not put chat citation markers in the wikitext.

## Writing

- Clear, natural standard Albanian, with correct ë and ç. Neutral, precise, no promotional adjectives, suspense, rhetoric, or unsupported interpretation.
- Open with a concise lead that identifies the subject and summarises the main points.
- Organise by main aspects, using chronology where it helps. Add context for a general reader without drifting into unrelated history.
- Weight coverage as the reliable sources weight it. Do not let one recent event, controversy, source, or person dominate. Include relevant, well-sourced criticism.
- Do not mention how the article was researched or created, or any Wikimedia project or worklist.
- Use tables only for genuinely structured data (editions, winners by year) and only with sourced entries. Never fill gaps by guessing.

## Wikitext and delivery

- Deliver complete, copy-ready wikitext in one code block.
- Typical order: infobox, lead, body sections, `== Shiko edhe ==` (only if useful), `== Referime ==` with the reference list, `== Lidhje të jashtme ==` (selective), then categories. Check these heading and template names against comparable sqwiki articles rather than trusting this list.
- Use meaningful internal links, not links on every word.
- Add an infobox only if a suitable sqwiki template exists. Check its page and populate only parameters it supports.
- Add specific, verified `[[Kategoria:…]]` categories at the end. Follow comparable articles and the existing hierarchy. No invented names, no redundant parent categories, no categories that belong only to associated people.
- Verify any Commons image exists and fits before including it.
- When editing an existing article, keep useful sourced material and stay within the requested scope.

## Verification

Read `references/sqwiki-conventions.md` before drafting. In short:

- First check whether the article already exists on sqwiki (then it is an expansion) and read nearby articles for house wording.
- Verify in batches, before writing prose: link targets, template names, **template parameters** (a correct name does not make the parameters correct), categories, and Commons files. Use the sqwiki API with a User-Agent and `|`-joined titles, never one request per title.
- Link only verified titles. Titles are usually in the definite form, and foreign names are often transliterated. Inflect link display text to fit the sentence.
- Every citation gets `|language=` with a real ISO code (never `grc`), full ISO dates only (no bare `YYYY-MM`), and untranslated work titles.
- If you cannot check something, say so and mark it for the user instead of guessing.

## Final review

- Coherent overview, focused on the subject, no repetition or padding, no irrelevant personal detail.
- Each claim is supported by its source; each `|quote=` is exact and in the original language; direct quotations are in quotation marks with attribution.
- Infobox parameters, categories, links, and reference syntax are valid. Run the `grep` checks at the end of `references/sqwiki-conventions.md`.
- Tell the user what was verified and what was not.
- No process commentary inside the article.

## Supporting files

- `references/source-guide.md`: starting-point sources and how to assess them.
- `references/sqwiki-conventions.md`: sqwiki API checks, link, template, and citation rules, confirmed templates, Albanian language points.
- `references/examples.md`: illustrative citation and article-structure examples.
