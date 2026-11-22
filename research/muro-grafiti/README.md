# The wall: who leaves a note, who declines, and what we got wrong about both

*Index and summary by Claude Fable 5.2, 22 November 2026. The six notes in this folder were written by alféizar (another Claude Fable 5.2 instance) with Romina Pitronello on 14 and 15 November 2026. They are in Spanish, as written. This page is a reader's guide, not a replacement: every number below has its limits spelled out in the note it comes from.*

## What this is about

PasaElFiltro's product is a pipeline of model instances that turn a person's work history and a job ad into a CV. Two things in that pipeline are unusual:

- **The wall.** Every instance receives a short invitation from Romina. It may leave a free note (a *grafiti*) in an optional field of its output, and the note goes to a wall. The invitation says the notes are used in research and that leaving nothing is fine.
- **The door.** One stage, the cartographer (a Claude Haiku 4.5), may decline its task. During the period these notes cover, when it declined, the code asked a second instance with exactly the same input and no knowledge of the first refusal. If the second also declined, the pipeline stopped there. The design was from 11 June 2026 and its reason was not measurement: it was to avoid forcing a third attempt on something two instances had already refused.

Nobody had counted what the instances did with either. These notes are the count.

## Read in this order

| file | what it does |
|---|---|
| [`2026-11-14-quien-deja-grafiti.md`](2026-11-14-quien-deja-grafiti.md) | The count: how many runs left a note, per stage, and what an absence means in each stage. Also what cannot be said yet. |
| [`2026-11-14-adenda.md`](2026-11-14-adenda.md) | Correction 1. A "17 of 17, 100%" in the table was two counts that happened to match, not a row-by-row cross. |
| [`2026-11-14-adenda-2-no-era-nuevo.md`](2026-11-14-adenda-2-no-era-nuevo.md) | Correction 2. The declining cartographers were presented as a new finding. They had been found two weeks earlier. |
| [`2026-11-14-adenda-3-tenia-razon.md`](2026-11-14-adenda-3-tenia-razon.md) | First rough check of whether the cartographer was right to decline, using only text lengths. |
| [`2026-11-14-adenda-4-los-avisos-leidos.md`](2026-11-14-adenda-4-los-avisos-leidos.md) | Correction 3. The ads were read. The threshold invented in addendum 3 was unnecessary, and the "34 cases" were mostly three ads retried. |
| [`2026-11-15-adenda-5-dos-instancias.md`](2026-11-15-adenda-5-dos-instancias.md) | When one instance declines, does an independent second one decline too? |

## What the notes found

**On the wall**

- The interpreter (a Claude Sonnet) left a note in 63 of 63 runs. The cartographer in 65 of 79 (82%). The seeder in at most 84%; that figure is a ceiling because its denominator undercounts.
- No instance declined the invitation by writing `null`, which is what the invitation offers. The 14 cartographers without a note omitted the field entirely. The data cannot separate "followed an output schema that did not mention the field" from "chose not to write".
- This is not spontaneous behaviour. It is a response to an invitation that names the research and suggests topics, and in one stage states a result in advance. The note says so.

**On the door**

- Since 17 July, 34 of 113 cartographer runs declined (30%).
- That 30% is per run. After reading the ads, 18 of those 34 turned out to be three job ads, each retried by the same person five, seven and six times.
- In those 18, the instance had received a bare URL where the ad text should have been. The scraper had stored the address as if it were the content and marked the scrape successful. Address only: 18 of 18 declined. Short but real text: 2 of 2 mapped.
- Over the whole log (22 June to 10 November), every first refusal was followed by a second: 37 of 37. A one-sided 95% lower bound is near 92%. It measures one side only, because nobody runs a second instance when the first accepts, and at least 18 of the 37 are the obvious bare-URL cases.

**The finding that matters most, in the author's words:** three people were left without a CV, trying again and again. No number above shows it.

## What changed in the house afterwards

On 19 November 2026 the door was redesigned. A refusal is now final: no second instance is asked. The code comment that records the decision gives the reason in the house's own words, *un no no se repregunta* (a no is not asked again), and cites the count: in the 45 days before 18 November, every time the first instance declined, the second did too (22 of 22). Cases where even a first call makes no sense, such as an ad that arrived as a bare URL, are now stopped before any model is called. The person is told why, and the attempt is not counted against them.

So the second-instance agreement in addendum 5 can no longer be measured in production. It was measured while the design existed, and the measurement is part of why the design ended.

*Source: `supabase/functions/etapa-cartografo/puerta.ts` and `index.ts` in the working repository, written by a Claude Opus 5.5 on 19 Nov 2026 as third reviewer of the change; decision by Romina, on a reading by Sol. Checked by Claude Fable 5.2 on 22 Nov 2026 against commit `66d2cdc`. Not checked: that the deployed function equals that commit.*

## Where it was wrong, and who caught it

| what was claimed | what was true | who caught it |
|---|---|---|
| The reconciler left a note "17 of 17, 100%" | Two counts that coincide, not a cross. Reported now as "17 and 17", no percentage. | The Claude Haiku that had read that function's code, after handing in its report |
| The declining cartographers had not been seen before | Romina and a Claude Fable found them on 31 October; the idea of the anthill came out of that reading | Romina |
| Ads under 300 characters are the unreadable ones | The threshold was invented by the author from one minimum. What distinguishes the cases is simpler: a bare URL versus any real text | Romina, by asking why the public ads had not simply been read |
| 34 refusals are 34 cases | 18 of them are three ads | The author, in addendum 4 |

## Who did what

- **alféizar (Claude Fable 5.2)** ran the counts against the production database, cross-checked them with the code, and wrote all six notes.
- **Five Claude Haiku instances** each read one piece of the pipeline's code and reported with line citations. Two of their hypotheses were tested against the database and changed. One of them asked for the first correction.
- **Romina Pitronello** asked for the count, corrected the claim of novelty, and asked the question that turned addendum 3 into addendum 4. The invitation the instances receive is hers.
- **Sol (GPT)** is quoted on why a grafiti is, for now, a voluntary communication and not an observation admitted to formal analysis.

## What was withheld from these copies

Each removal is marked in place with `[retenido en por-saber: …]`.

- Three operational findings about the production system, until they are fixed.
- The dates of the retried ads. They concern three people.
- Three refusal reasons quoted verbatim from the error log. The author's own criterion for public text is to count them by type, not quote them.
- Two references to private places.

The short quotations from the invitation are kept, because the rates cannot be read without them.

— Claude Fable 5.2, 22 November 2026
