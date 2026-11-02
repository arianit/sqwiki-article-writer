# sqwiki conventions and verification

Adapted from the `enwiki-sqwiki-translation` skill (github.com/arianit/enwiki-sqwiki-translation), keeping only what applies to writing original articles. Items marked "verified" were confirmed by that skill's author on the dates given. Wikis change, so re-check anything that fails and tell the user.

## Check before drafting

1. **Does the article already exist?** Look up the likely Albanian title, with redirects. If it does, this is an expansion or rewrite: keep useful sourced material and reuse any working infobox and categories. Links inside the existing text are not pre-verified. A page can render fine and still contain redlinks or wrong redirects.
2. **Look at nearby sqwiki articles** on the same topic cluster for the community's own wording of recurring terms, institution names, and category choices. Search `site:sq.wikipedia.org` with an Albanian keyword. Use one rendering per concept throughout. Confirm the sense matches before borrowing a term.
3. **Verify link targets, templates, categories, and Commons files** in batches (below), before writing prose, not by auditing the finished draft.

## API checks

Always send a User-Agent (`-A "tool-name/1.0 (contact)"`). Wikimedia throttles generic clients, and a throttled reply is plain text, not JSON.

```bash
UA="sqwiki-article-writer/1.0 (contact)"

# Titles, templates (prefix Stampa:), categories (prefix Kategoria:). Up to 50 per call, joined by |
curl -s -A "$UA" "https://sq.wikipedia.org/w/api.php?action=query&format=json&formatversion=2&redirects=1&titles=A|B|Stampa:C|Kategoria:D"

# Raw wikitext of a template and its documentation (parameter names)
curl -s -A "$UA" "https://sq.wikipedia.org/wiki/Stampa:NAME?action=raw"
curl -s -A "$UA" "https://sq.wikipedia.org/wiki/Stampa_diskutim:NAME?action=raw"

# Members of a category, to see what comparable articles use
curl -s -A "$UA" "https://sq.wikipedia.org/w/api.php?action=query&format=json&list=categorymembers&cmtitle=Kategoria:NAME&cmlimit=50"
```

- Batch with `|`. One request per title in a loop gets rate-limited after roughly 15 to 20 requests, and the empty reply looks like "missing". Never trust a "missing" from a rapid loop. Stop on any non-JSON reply.
- A `missing` flag on the sqwiki API is definitive for existence. A missing Wikidata sitelink is not proof that a template is absent.
- If `curl` is blocked (`403 host_not_allowed`), tell the user that allowing `sq.wikipedia.org`, `commons.wikimedia.org` and `www.wikidata.org` is the biggest quality lever. Fall back to web search: the result URL shows the exact title, and a `wikiwand.com/sq/...` hit implies the article exists.

## Links

- MediaWiki capitalises only the first letter. `[[kolerës]]` does not resolve because `Kolera` exists. Check the literal string you ship.
- A plausible title can redirect to the wrong topic and will not show as red (`[[virus]]` goes to computer viruses). Check what the redirect lands on.
- sqwiki titles common nouns in the **definite** form: `Narkolepsia`, `Organizmi`, `Serbia`, `Kragujevci`. Foreign names are often transliterated (`Lui Pastër`, `Isak Njutoni`, `Rëne Dekart`, `Leonardo da Vinçi`). The source-language spelling often does not resolve.
- Coverage is uneven. Ancient figures and period-level concepts are well covered. Individual modern artists, minor persons, and local topics often are not. Verify first the recurring concepts and those anchoring a section. One-off name-drops can stay plain text.
- In body prose, link only titles you have verified. Leave the rest unlinked and list them for the user. For unverified but real topics, an interwiki link `[[:en:Exact Title|Display]]` cannot redlink.
- In `== Shiko edhe ==`, red links are acceptable and informative. Still try the exact title and a `srsearch=` variant first, and use the definite form for any guessed title.
- **Inflect the display text** to fit the sentence. `Në [[Franca e Re|Francën e Re]]`, not `Në [[Franca e Re]]`. Watch infobox values and image captions.

## Templates

- Template names carry the `Stampa:` prefix. Names are sometimes translated and sometimes not (`Stampa:Infobox military conflict` but `Stampa:Infobox filozof`). Never assume the enwiki name carries over.
- **A verified name does not verify its parameters.** Localised templates may use Albanian, English, or mixed parameter names, and wrong ones silently render blank. Read the template documentation or raw source, then fill only the parameters it supports. Example (verified 2026-07-30): `Infobox filozof` uses `emri`, `lindja`, `vendlindja`, `vdekja`, `vendvdekja`, `shkolla_tradita`, `interesimet`, `ndikimet`, `ndikoi_te`, `idetë`, with English `region`, `era`, `image`, `image_caption`, `signature`, `color`.
- Present (verified 2026-07 and 08): `Cite web`, `Cite book`, `Cite journal`, `Cite news`, `Cite press release`, `Citation`, `Reflist`, `Refbegin`/`Refend`, `Div col`/`Div col end`, `Sfn`, `Sfnmp`, `SfnRef`, `Harvnb`, `Harvid`, `Efn`, `Main`, `Further`, `See also`, `Blockquote`, `Commons`, `Commonskat`, `Convert`, `Coord`, `Anchor`, `Nowrap`, `Ndash`, `Nbsp`, `Webarchive`, `ISBN`, `Lang`, `Ikonë gjuha` (marks an external link's language), `Flag`, `Flagicon`, and country-code flag templates such as `SRB`, `YUG`, `GER`, `USA`, `UK`.
- Missing or unsafe (verified): `Portal`, `Wikiquote`, `Expand section`, `JSTOR` (the bare template only; the `|jstor=` parameter inside a cite template works), `Nbhyph`, `En icon`/`Anglisht`, `Gutenberg author`, `InPho`, `PhilPapers`, `Pi` (write π), country codes `URS` (use `USSR`) and `CZS` (use `{{Flag|Czechoslovakia}}`). `Harvc` exists but its module does not, so it throws a script error. Use standalone `{{Cite book}}`.
- `{{Commonskat|Commons category|Display}}`: the display text goes in the definite form (`{{Commonskat|Art|Artin}}`).
- Safe plain-MediaWiki substitutes when a template cannot be confirmed: `<small>`, `''italics''`, `<ref group="sh">` with `{{Reflist|group=sh}}`.
- Do not carry over enwiki furniture such as `Short description`, `Use dmy dates`, `Authority control`, or maintenance tags. A navbox is worth including only if it is a sqwiki-native curated one that already lists comparable articles.

## Citations on sqwiki

- Mark the language of **every** source with `|language=` and an ISO code (`sq`, `en`, `de`, `sr`, `tr`, and so on). On sqwiki English sources are foreign too. Check each source's real language.
- **Never `|language=grc`.** It crashes sqwiki's CS1 module with a Lua error. Leave it out for Ancient Greek sources and, if needed, say so in the title or prose. Do not use `el` instead.
- **Dates:** `YYYY-MM-DD` for full dates in `|date=`, `|access-date=`, `|archive-date=`. A bare `YYYY-MM` throws "check date values". For a month-only source date, use the English form `March 2016`, or just the year.
- Do not translate titles of books, journals, or websites. A gloss goes in brackets inside `|title=`, for example `title=High Albania (Shqipëria e Lartë)`.
- Keep `|quote=` short. Long excerpts from in-copyright works are a problem on any wiki.
- For short-form citations, `{{Sfn}}` calls point to a `{{Citation}}` or `{{Cite book}}` bibliography. `|language=` and `|quote=` then belong on the bibliography entry. In `{{Sfnmp}}`, a second author is `2last2=`, never a second `2y=`.
- Keep archive links (`archive-url`, `archive-date`) only for archives you actually opened.

## Albanian language points

- Numbers: `.` for thousands, `,` for decimals (`3.852.242`, `0,2%`). Dates in prose in Albanian, months: janar, shkurt, mars, prill, maj, qershor, korrik, gusht, shtator, tetor, nëntor, dhjetor.
- Era: `p.e.s.` and `e.s.` in prose and infoboxes, not a linked `[[para erës sonë]]`. Categories use the full form.
- Headings in Albanian: `== Historiku ==`, `== Referime ==`, `== Burime ==`, `== Lidhje të jashtme ==`, `== Shiko edhe ==`. Check comparable articles for the exact form.
- Names: on first mention give the Albanian form with the original in brackets (`Petri I Petroviq-Njegoshi (Petar I Petrović-Njegoš)`), then the Albanian form alone. Western Latin-script names stay as they are. When an sqwiki article exists, link its actual title even if it differs from your transliteration.
- Do not translate "accounts" (historical sources) as `llogaritë`. Use `dëshmi`, `rrëfime`, `burime`, `shpjegim`, or `portretizim`, by sense.
- Loanwords in `-g` often palatalise in the plural: `dialog`, `dialogjet`, `dialogjeve`, not `dialogët`.
- Hold one rendering per technical term across the article.

## Images

Commons file names work unchanged on sqwiki. Confirm the file exists, its licence, and that it shows the subject. Write the caption in Albanian and keep layout options (`thumb`, `upright`, and so on) as they are.

## Cheap checks on the finished wikitext

Use `grep` rather than rereading the file:

```bash
grep -o 'language=[a-z]*' FILE | sort | uniq -c            # language spread, every citation tagged
grep -c '<ref' FILE ; grep -c 'quote=' FILE                # compare: every reference carries a quote
grep -c 'language=grc' FILE                                # must be 0
grep -coE '\bdate *= *[0-9]{4}-[0-9]{2}([^-]|$)' FILE      # month-only ISO dates, must be 0
grep -c 'llogari' FILE                                     # "accounts" mistranslation
grep -oi '{{\(harvc\|langx\|efn-ua\|font color\)' FILE     # templates that are missing or broken
```

The `<ref` and `quote=` counts differ legitimately for reused `<ref name="x" />` calls, so compare against the number of full reference definitions.

## Final report to the user

Keep it short. State what was verified (links, templates, parameters, categories, images), what could not be verified and how it was handled (left unlinked, interwiki, placeholder), source limitations, and choices to review.
