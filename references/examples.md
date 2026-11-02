# Examples

All names, URLs, and excerpts below are placeholders to show the shape. Never copy them into a real article. Before use, confirm on sq.wikipedia.org that the template names and parameter names are right (for example `accessdate` versus `access-date`, and how the source language is marked).

## Citation patterns

News article:

```wikitext
<ref name="shembull1">{{Cite news |last=Mbiemri |first=Emri |title=Titulli i artikullit |work=Emri i botuesit |date=2020-05-14 |url=https://example.org/artikulli |access-date=2026-11-02 |language=sq |quote=Teksti i saktë nga burimi, në gjuhën origjinale.}}</ref>
```

Book with page number (only if the page was actually checked):

```wikitext
<ref>{{Cite book |last=Mbiemri |first=Emri |title=Titulli i librit |publisher=Botuesi |place=Prishtinë |year=2005 |page=112 |isbn=... |language=sq |quote=Fragmenti i saktë nga faqja 112.}}</ref>
```

Source in another language: the `|quote=` stays in that language, and the language parameter says so.

```wikitext
<ref>{{Cite web |title=Original title |website=Example |url=https://example.org/en |access-date=2026-11-02 |language=en |quote=The exact sentence from the source.}}</ref>
```

Reuse of a named reference:

```wikitext
Teksti i parë.<ref name="shembull1" /> Teksti i dytë, i mbështetur nga i njëjti burim.<ref name="shembull1" />
```

Direct quotation in the body, attributed and referenced:

```wikitext
Sipas gazetarit Emri Mbiemri, festivali ishte «një ngjarje e rrallë për qytetin».<ref name="shembull1" />
```

Attribution of a contested or interview-based claim:

```wikitext
Drejtori i institucionit deklaroi në një intervistë se ndërtesa u rinovua në vitin 2012.<ref>...</ref>
```

## Article structure: institution or organisation

```wikitext
{{Infobox ...}}  <!-- only if the sqwiki template exists; verified parameters only -->
'''Emri i institucionit''' është [lloji i institucionit] në [vendi], i themeluar në [viti]. [Një ose dy fjali për funksionin kryesor dhe rëndësinë.]<ref>...</ref>

== Historiku ==
[Themelimi, zhvillimet kryesore sipas kronologjisë. Persona të përmendur vetëm kur shpjegojnë zhvillimin.]

== Struktura dhe veprimtaria ==
[Çfarë bën, si organizohet, programet kryesore.]

== Rëndësia ==
[Vlerësimet e burimeve të pavarura, përfshirë kritikën e mbështetur me burime.]

== Shiko edhe ==
* [[...]]

== Referime ==
{{Reflist}}

== Lidhje të jashtme ==
* [https://example.org Faqja zyrtare]

[[Kategoria:...]]
```

## Article structure: festival or recurring event

```wikitext
'''Emri i festivalit''' është [lloji] që mbahet [në vend, sa shpesh], që nga viti [viti].<ref>...</ref>

== Historiku ==
[Origjina, ndryshimet e rëndësishme në formë dhe vend.]

== Programi ==
[Pjesët e përhershme të programit, pa lista pjesëmarrësish.]

== Edicionet ==
{{Tabela ...}}  <!-- ose tabelë wikitable; vetëm rreshta të burimëzuar -->

== Referime ==
{{Reflist}}

[[Kategoria:...]]
```

## Short-article note

If sources support only a few solid paragraphs, deliver a lead plus one or two sections. Do not add empty or speculative sections to look complete.
