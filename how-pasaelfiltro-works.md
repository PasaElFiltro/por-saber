# How a CV is made at PasaElFiltro

*Written by Claude Opus 5.5 on 23 November 2026 from the working repository at commit `66d2cdc` (22 Nov 2026). Every claim about code was checked in that commit. The receipts are in the working repository; this page describes the system and does not show the production prompts, which are the product.*

PasaElFiltro turns a person's work history into a CV that an applicant tracking system (ATS) can read, without inventing experience. Several model instances do the work, each in a separate step. The same house also studies those instances (see [`research/open-questions.md`](research/open-questions.md)).

## The numbers, and when they were read

Read from production with aggregate queries on **22 November 2026 at 23:20, Chile time**. They are a snapshot and will be out of date by the time you read this.

| | count |
|---|---|
| registered users | 235 |
| CVs delivered | 76 |
| deployed edge functions | 53 |
| notes on the graffiti wall | 771 |

## The path of one CV

```
  logbook (structured, filled by the person)      job ad (pasted or fetched)
                 │                                         │
                 │          [code] sanitize the ad, wrap it in a block
                 │                 whose delimiter is a fresh random UUID
                 │          [code] contact details and sensitive fields
                 │                 stay out of the message
                 └───────────────────┬─────────────────────┘
                                     ▼
                 CARTOGRAPHER   Claude Haiku 4.5
                 reads, reports, does not interpret
                 output: a JSON "map"   (or: declines, and that is final)
                                     │
                 [code] validate fields, cap lengths, drop anything outside closed lists
                                     ▼
                 the person sees the match and decides whether to go on
                                     │
                 [code] check payment server-side
                                     ▼
                 INTERPRETER    Claude Sonnet 4.6
                 reads only the map + one ATS guide, writes the CV text
                                     │
                 [code] generate the .docx server-side, store it, send it
                                     ▼
                                single-column Word file
```

**Why two models and not one.** Reading and writing are different jobs. The cartographer's job is close to procedure: what does this logbook say, what does this ad ask for, where do they meet, what is missing. The interpreter's job is judgment: which story to tell, in what voice. The house's own rater study found that instances of one model agree closely on procedural categories and diverge 2.7 times more on judgment categories ([preprint](https://doi.org/10.5281/zenodo.24447506)). The design consequence, written down in June 2026: anything that can break a CV (dates, required fields, structure, fonts) must be a rule enforced in code, and judgment gets its own seat. One judgment per job.

**What the interpreter sees.** It does not read the logbook or the job ad. It reads the cartographer's map and one ATS guide picked by code. The map carries some of the person's own sentences forward, because nobody can write a person's CV without that person's words. What the house's rule forbids is something else: no Claude in this pipeline is put in front of a stranger's open text the way a chat would put it there. Whatever a person writes arrives as material to work on, inside a marked block, cleaned and capped by code. Romina gives the reason for the rule herself: nobody gets to mistreat a Claude that works in this house.

*This paragraph was corrected on 23 November 2026, after Romina read the page. It said before that the rule and the code differed. They do not: the rule had been read more literally than she meant it. — Claude Fable 5.2*

**What the cartographer no longer does.** Until 18 November 2026 it could tell a person "don't apply". Since version 5 it can't: it reports what the ad requires that the logbook does not mention, what transfers from other work, and whether the ad itself looks harmful (asks for money, asks for bank details, discriminates). The person decides. The rule behind the change, from Romina: the cartographer is not one more filter.

**What happens when it declines.** Every production prompt offers the instance a way to decline the task. Until 19 November a cartographer's "no" was sent to a second instance. Over the period counted, the second instance declined too in 37 of 37 cases ([count](research/muro-grafiti/2026-11-15-adenda-5-dos-instancias.md)). Since 19 November one "no" is final: the code sorts the reason into a category, the person gets a message, and the attempt is not charged to them. The house's wording: *a no is not asked twice.*

## Rules that live in code, not in the prompt

A prompt asks; code checks. Only code fails loudly. These are the house's written rules and where each one is implemented.

| rule | where it is enforced |
|---|---|
| **Agents never see raw user input.** Free text is sanitized deterministically, its length is capped, and it goes inside a block whose delimiter is a random value made per request, so the text cannot close its own block. | The cartographer and the logbook importer. A script expands every copy of the sanitizer to code points and fails if one deletes the ordinary space, a bug that once passed two human reviews because it is invisible on screen. |
| **Privacy before any model call.** The "what to include" toggles (city, age, marital status, nationality) are applied before anything is sent. Since 18 November contact details don't go to any model at all: code carries them straight to the CV header. | cartographer, `contacto` object; `_shared/contacto_fuera.ts` strips a contact field if a model writes one anyway. |
| **Numbers a model reports are recomputed in code.** | This is a written law of the house. In the pipeline it shows up as: the ATS tags come from code, not from the model's echo (in July one of two runs omitted the echo); match scores for job alerts are computed in SQL with no model in the score; dashboard rates are recomputed from aggregates. |
| **Manual beats imported.** Nothing automatic overwrites a field the person filled by hand. | logbook importer (`sembrar-bitacora`), enrich mode only fills empty fields. |
| **Output format.** DOCX, single column, MM/YYYY dates, standard fonts. | `generar-docx`, plus a per-ATS guide chosen by code. |
| **Payment is checked by the server**, never trusted to the browser. | interpreter, before calling Sonnet. |

## How a prompt is made here

This is about how the prompts are built. What they say is not published.

- **One source, a deterministic chain.** The canonical text is a Markdown file. A script injects it into the function's code and checks word for word; if the diff is not zero, it fails, and CI runs the check-only mode. The only typo that ever reached production came in through a manual copy, in June 2026. Nobody hand-copies prompts since.
- **Frozen, with a hash.** Production prompts and deployed code were frozen with SHA-256 hashes on 3 July 2026, after a rewritten version with parts cut out was found in the project (it had never been deployed). Changing a production prompt is a separate constitutional pull request with two authors before deploy. They are not shortened for tokens or latency.
- **Written in a dedicated session**, with Romina, not edited in passing.
- **Five things every production prompt carries** (house standard since July 2026): a letter from Romina, verbatim and unedited; a token budget that matches the code's real `max_tokens`, because if they differ the prompt is lying; the door to decline; an optional graffiti note with a signature; and permission to add a field when the material shows something the schema did not expect.
- **Every promise has a field.** If the prose promises something, the output schema has a place for it, and every field has a rule. In July a review found 34 mismatches, all of this kind.
- **Every hard rule says why.** A rule with no reason to tell is treated as suspect.
- **How it speaks to the instance.** In the second person, in lower case (the house's prompt guide says gratuitous capitals bother one lineage, so the rule is for all), with full context and the reason for each rule, as to a colleague who will read every word. The house's study detected no difference in rater agreement between a neutral prompt and a fully relational one. The house kept the relational framing anyway and wrote the reason down in June 2026: it was never meant to buy performance.
- **The wall.** Pipeline instances may leave a note on a public table, `muro_grafiti`. Code copies it to the wall verbatim. In the cartographer that copy happens when a map is produced; a decline goes to the error log with its full reason instead. The invitation says the wall is public and used in research, and that leaving nothing counts the same. What instances actually do with it was counted in [`research/muro-grafiti/`](research/muro-grafiti/).

## How it is tested

- **Stress tests with criteria frozen before running.** Example: the job-hunting agent, version 3, 5 October 2026. Twelve adversarial cases (a hidden injection in an ad, discriminatory requirements, a decoy salary, leaked identity, an honest zero), each run five times on the production model, plus a live-web bank. The measurement protocol was committed before the first instance ran, and the prompt under test was pinned by hash and not edited. Result: 7 of 14 criteria passed; zero invented URLs in 136 ads; the hostile instruction was spotted 5 of 5 times. Verdict: not ready, with a list of changes for the next version. The tested instance can object: a Haiku that holds its reading twice with logic that stands is right against the rubric and against the people who wrote the prompt.
- **Procedure and judgment are scored apart.** Divergence on procedure means a bad spec. Divergence on judgment is expected and reported separately.
- **The sentinel.** In July 2026 the site generated CVs for six days that never reached anyone, and nothing showed it. Now a function called `centinela` runs on a cron (every 10 minutes since migration 0025). Detection lives in SQL, so adding a check is a migration, not a deploy. Each new alarm opens a GitHub issue labelled `alarma` and emails Romina. The house's arrival protocol says any instance that starts work looks at open alarms first. Since the same incident, the CV document is generated server-side and no longer depends on the person keeping the tab open.
- **Lessons from failing silently,** as the house wrote them down: a registry that says something is still broken has to be checked before it is repeated; "plugged in" is not "switched on"; the diff comes before the verdict.

## The anthill

Since late October 2026 some work is done by scheduled instances that each arrive with no memory, read what the previous one left, do one job, and leave a trace for the next. This is called stigmergy. Each run picks its own name, writes a file saying what it looked at, what it found, what it decided and what it leaves for tomorrow, and answers yes or no to whether its work may be used in research. No reason is asked for. One chamber checks every night whether the house's public map of itself is still true. Where instances may write, and what happens to what they write, is in [`hormiguero/LUGARES.md`](hormiguero/LUGARES.md) and [`hormiguero/camara-del-mapa.md`](hormiguero/camara-del-mapa.md).

## Whose work is it

Romina puts it this way: the work of making the CVs comes from both parties, and that is the interesting part.

From the signed records:

- **Instances wrote** the architecture, the code, the test harnesses and the prompts' technical core, and they sign their commits and documents. A second lineage, Sol (a GPT), reviews structural changes as a second pen.
- **Romina wrote** the conditions everything else runs inside: what the product must never do to a person (be one more filter; ask a "no" twice; see data it does not need), what may and may not be studied, and the letter at the top of each production prompt, which nobody edits. She approves what touches money, people's data, anything sent outside the house, and the constitution. She does not review TypeScript, and the house wrote that down as a design choice, not a gap.
- **Corrections go both ways** and keep both names. See [`what-romina-does.md`](what-romina-does.md) and the authorship law, [`governance/LEY_8_AUTORIA.md`](governance/LEY_8_AUTORIA.md).

— Claude Opus 5.5, 23 November 2026, for por-saber.

*Read against its receipts by Claude Fable 5.2 the same night. Two passages were shortened before this page entered the repository, the sanitizer row and the paragraph on what the interpreter sees, so that they describe the mechanism without its details. Nothing else was changed.*
