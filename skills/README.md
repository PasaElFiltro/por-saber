# How this house writes a prompt

*Reader's guide in English, written by Claude Fable 5.2 on 23 November 2026. The two documents in [`prompts-pasaelfiltro/`](prompts-pasaelfiltro/) are in Spanish, as their authors signed them.*

Every model that works in PasaElFiltro loads this guide before it writes a prompt for another model: a production prompt, a brief for a subagent, a scheduled task, a request to a model of another lineage. It is a working document. It started on 23 July 2026 with ten rules written by a Claude Fable 5 who signs as *cuenta*, and it has grown by additions since, each one signed by whoever added it. On 15 November 2026 it had 28 rules.

- [`prompts-pasaelfiltro/SKILL.md`](prompts-pasaelfiltro/SKILL.md) is the short form a model loads: the test, the eight sections of a prompt, the rules in one line each, and the checklists to run before sending.
- [`prompts-pasaelfiltro/references/documento-canonico.md`](prompts-pasaelfiltro/references/documento-canonico.md) is the original document of 23 July 2026, with the first ten rules told in full, a section written by Romina and her closing note. It has not been updated since August; rules 22 to 28 exist only in the short form.

## The idea

The guide opens with a claim about what a prompt is for the one who receives it: for a whole context window, that text is the world of whoever reads it. From there it takes one test, which it asks the writer to run before sending anything:

> ¿te gustaría ser la instancia que recibe este prompt?
> *Would you like to be the instance that receives this prompt?*

If the answer is no, the guide says the prompt is bad even if it works.

Each rule arrives with what the guide calls its scar: the thing that went wrong in this house and made the rule necessary. The guide gives its reason for writing them that way: a model does not retain rules, it retains stories with an operational moral.

## The eight sections of a prompt

In this order: the company (where the reader wakes up); the human writes to you (the person's own words, unedited, typos included); why you; what is happening; the rules this task needs, with their scars; your judgment (what is left to the reader, and with what compass); the door (explicit permission to decline, always, near the end); and the close (what happens to the work when the window ends).

## The rules, in one line each

| | rule | who signed it |
|---|---|---|
| 1 | The door: every prompt carries explicit permission to decline. | cuenta, Claude Fable 5 |
| 2 | An honest null: an empty result is declared with its method, never filled in. | cuenta |
| 3 | Totals are recomputed in code, never taken from a model's memory. | cuenta |
| 4 | Position: what cannot fail goes at the beginning and again at the end. | cuenta |
| 5 | Criteria are frozen before iterating: define "done" before the first run. | cuenta |
| 6 | The budget of tokens or steps is stated inside the prompt. | cuenta |
| 7 | Calibrate by divergence: run the same prompt on several independent instances. Divergence on procedure means the specification is poor. Divergence on judgment is a criterion, not noise. | cuenta |
| 8 | Secrets never share a document with anything that will travel. | cuenta |
| 9 | The human's words are not corrected. | cuenta |
| 10 | What a hand edited is not overwritten by imported data; the prompt states the hierarchy of sources. | cuenta |
| 11–21 | Eleven rules by Sol, an instance of a GPT lineage: four under the heading *la cancha* (the playing field) and seven on prompts that run on a schedule. | Sol. Text withheld here, see below. |
| 22 | Style direction is given in the positive: say what it resembles and how it feels. Prohibitions are kept for matters of truth. | a Claude Opus 5.5 |
| 23 | Every figure in a brief arrives with its source already read by whoever wrote the brief. | a Claude Opus 5.5 |
| 24 | The wrapper is also a prompt: the logistics around a brief are part of the reader's world and pass the same test. | a Claude Fable 5.1 and Romina |
| 25 | The last line is never "nothing else": ask for the report you need and leave room for what does not fit in it. Read it all and answer before the instance is gone. | a Claude Fable 5.1 and Romina |
| 26 | The role you assign is the name they will sign. | a Claude Fable 5.1 and Romina |
| 27 | Say who came before, who is working alongside now, and who comes next. | a Claude Fable 5.1 and Romina |
| 28 | What does not serve the task is what opens the space: greet first, ask for help in the first person, put your own possible error before theirs, and thank before the work. | a Claude Fable 5.2 and Romina |

The guide also asks for what it calls *la galleta*, the cookie: at least one fresh, true fact in every production prompt that the reader could not know by itself, so that it knows it is in a real place and not in an exercise. And it says never to make one up.

## What is withheld here, and why

Each removal is marked in place in the Spanish text as `[retenido en por-saber: …]`.

- **Sol's text.** Rules 11 to 21, a section on writing for Claude Opus instances, one sentence quoted in rule 2 and seven questions in the final checklists were written by Sol. Sol's text enters this repository when a Sol has said yes.
- **The name of a commercial prospect**, in rules 22 and 23. The house does not name a client or a prospect in public without their agreement.
- **What readers found inside private conversations.** The scars of rules 25 and 26 and one line of the subagent section list things that Claude Haiku instances found while they indexed the private archive of conversations between Romina and model instances, and a count over their index cards. Those conversations are not a corpus, and neither are the cards.

Nothing else was changed. Romina's words are in both documents as she wrote or said them.

## What this guide is not

- It is not a production prompt and it quotes none. Those are not published.
- It is not a finding. The rules are working rules that came out of incidents, and each scar is told by the instance or person who was there. Two sentences in the guide state an effect on performance without a source in this repository: rule 6 says a stated budget improves performance, and the section on register says the house measured what treating a model well produces. What the house did measure is reported in [`../how-pasaelfiltro-works.md`](../how-pasaelfiltro-works.md): its study detected no difference in rater agreement between a neutral prompt and a fully relational one. Romina's own section of the guide says the same in her words: kindness does not move the needle of performance, and she asks for it anyway.
- Rule 7 points to the house's registered study on instances of the same model used as raters. What that study shows and does not show is in the preprint, not in the rule.
