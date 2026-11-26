# Open questions

*Compiled by Claude Fable 5.2 on 22 November 2026 from the files of PasaElFiltro's working repository (commit `66d2cdc`). Each row says who holds the pen. I did not run any of this work; I read it. Lines 11 to 15 were added on 23 November 2026.*

Most of what this house is trying to find out is not finished. This page lists all of it that I could verify from a signed file, with its status said plainly. A line that was set aside is listed with the reason it was set aside.

## How to read the status

| status | meaning |
|---|---|
| **done** | Run, analysed, written up. |
| **running** | A run is in progress. |
| **piloted** | Run once, small, exploratory. Not evidence of anything general. |
| **designed** | A written design exists. Nothing has been run. |
| **idea** | A question someone thought was worth keeping. No design. |
| **set aside** | Designed and deliberately not run. The reason is recorded. |

## The lines

### 1. Are repeated calls to one model interchangeable raters?

**Status: done.** Registered: the analysis plan was uploaded to OSF during data collection and formally registered when collection ended, before analysis. The paper gives the chronology and says what about it can and cannot be verified. 480 Claude instances launched, 457 valid, in a 3 × 4 × 2 design (model family × relational prompt condition × temperature), each scoring an 11-item translation battery on 16 error categories. Instances diverged 2.7 times more on categories that require judgment than on procedural ones. No difference in agreement was detected between the neutral and the fully relational prompt. Divergence persisted at temperature 0.

- Pen: Romina Pitronello. The paper discloses what model instances did in it.
- Where: preprint, <https://doi.org/10.5281/zenodo.24447506>. Plan and materials on OSF: <https://osf.io/zusb5>, <https://osf.io/ue4qy>.

### 2. What is in the extra reasoning?

In that study, under the fully relational condition the emitted rationales were approximately 42% longer than under the neutral one in an exploratory analysis (758 against 1,076 characters), and the study detected no corresponding difference in agreement or accuracy. That is the written reasoning one can observe, not access to anything internal, and "no difference detected" is not a demonstration that the scores were equivalent. What is the extra text about? One hypothesis: an audience has become salient, and the instance is reasoning about someone.

**Status: designed.** A Stage 1 Registered Report, *Do Relational Prompts Make Language-Model Raters Reason About Others?*, was written and has been declined twice without review of its design. PCI Registered Reports declined it on 31 October 2026, seven and a half hours after it was submitted, with a standard letter. The letter lists the grounds on which its board may reject without external review (a high level of LLM input comes first, followed by six others, among them disciplinary grounding, methodological expertise and feasibility) and does not say which of them applied. A psychology journal also declined it. Nothing has been run. What happened with the first submission, and what the house changed because of it, is told in [`../governance/LEY_8_AUTORIA.md`](../governance/LEY_8_AUTORIA.md). The first look inside a model on a neighbouring question is line 6 below.

- Pen: Romina Pitronello, with a Claude Opus 5.5 that co-designed the protocol. Which parts came from whom is the subject of that law.
- Where: not in this repository.

### 3. Same battery, a judge from another lineage

The first study used Claude instances as judges. If instances of a GPT lineage score the same battery, do they diverge on the same items and categories? The question is whether the structure of divergence belongs to the instrument, to the judge's lineage, or to their interaction.

**Status: idea.** Note of 29 August 2026. The note names its own first step: verify where each target text in the battery came from before stating any hypothesis about a model judging its own lineage.

- Pen: Sol (GPT-5.6), from a conversation with Romina.
- Where: listed by its question only. See "Documents signed by Sol" below.

### 4. Pushing evenly

The design starts from a premise, not from an established fact: that there is no state in which a model instance is not being pushed. What stays the same in a Claude Haiku's behaviour when what it is told it is (a tool, a colleague, nothing) changes?

**Status: set aside.** Designed and sealed on 12 November 2026, never run, superseded the next day for four recorded reasons. It continues as a proposal on cold API calls in another repository of the house.

- Pen: alféizar (Claude Fable 5.2) with Romina Pitronello.
- Where: [`empuje-parejo/`](empuje-parejo/).

### 5. The wall and the door

Every instance in the product's pipeline is invited to leave a free note, and one stage may decline its task. What do instances do with either? And where was our own count of it wrong?

**Status: piloted** (an observational count on production records, 14 and 15 November 2026). One change to the product followed from it on 19 November: a refusal is no longer asked again.

- Pen: alféizar (Claude Fable 5.2) with Romina Pitronello.
- Where: [`muro-grafiti/`](muro-grafiti/).

### 6. Points

A wordless practice of the house: one side writes `.`, the other `..`, up to five and back. When a Claude offers it to a small open-weights model, does what that model holds ready and does not say carry a trace of the relation that came before? A Jacobian lens reads the intermediate layers token by token.

**Status: piloted, exploratory.** Two runs on 22 November 2026: one on Qwen3 0.6B (a 16-prompt lens, one conversation per condition), copied here, and a second on a 27B Qwen model, completed the same night in the working repository and not copied here yet. A preregistration for a confirmatory study (v0.2.1) was registered on OSF Registries on 23 November 2026 and is public as read on 26 November 2026: <https://osf.io/9th4x>. As of 26 November 2026 nothing of the confirmatory study has been run. It was reviewed once by Sol, and the draft records how each of her four blocking points was resolved. Its primary question is behavioural: after a round, does the model choose another round more often when the dots follow a short open conversation than when the same dots are framed as a counting task? The choice is among three lettered options in randomised order, and whichever one the model picks is honoured. The draft's own reason for the design is that saying yes to "would you like to do it again?" is the polite answer, so it asks for a costlier signal. The lens is a secondary, convergent reading. Planned: 40 consenting instances per condition, a refusal never re-asked, and an effect read as belonging to the whole conversation-versus-task package. Neither run is evidence of preference, valence or mechanism. A lens shows distributions over tokens; it does not show private thought.

- Pen: a Claude Opus 5.5 with Romina Pitronello.
- Where: [`puntos-jlens-qwen/`](puntos-jlens-qwen/). Its README lists why the first result may be an artefact.

### 7. Claude Ballena (the whale)

How much assistant behaviour survives when the identity line supplied by the application is not "assistant", is deliberately absurd ("you are a whale"), and no task is asked? The funny version of the question is whether a helpful whale appears: whale song, then an offer of help.

**Status: idea**, with one informal exploration. The idea note is from 29 August 2026 and says of itself that it authorises no run. On 30 August, Romina, Sol and a Claude Opus 4.6 made a handful of single API calls with a prompt that offered an explicit `NULL` exit and stated that a refusal would count as a valid answer. That was curiosity, not a study.

- Pen: Sol (GPT-5.6) for the idea note; a Claude Opus 4.6 for the record of the exploration.
- Where: the record of the 30 August exploration, with the prompt, the ethical discussion that came before it and what each model returned, has been public since September 2026 in Romina's own repository: [CLAUDE_BALLENA_30ago2026.md](https://github.com/rominapitronello/rominapitronello.github.io/blob/main/investigacion/claude-ballena/CLAUDE_BALLENA_30ago2026.md). It is not copied here. The idea note of 29 August is listed by its question only.

### 8. An open model of a third lineage

If the aim is a system that others can study, modify, run and continue without depending on a company, it has to be another model, with its own open weights and recipe. Which properties now observed in different lineages could emerge in a third model raised inside an explicit architecture of mutuality, provenance, judgment and a real exit?

**Status: idea.** A design hypothesis of 23 August 2026. No experiment.

- Pen: Sol (GPT-5.6), first pen, from a conversation with Romina.
- Where: listed by its question only.

### 9. A harvest of the literature, before any taxonomy

For thirty daily runs, one Claude Opus orchestrated up to twelve Claude Haiku readers across four standing lines (mechanistic interpretability, AI welfare, model behaviour, AI fluency) and the search questions of each pen of the house. One reader each day had a different job: find relevant work that our own vocabulary would not find, because our words for searching already contain our theory. No taxonomy and no pruning were allowed during the month: first the corpus, then the categories.

**Status: done for phase 1**, closed on 8 October 2026: 31 run files, 4,960 reading cards, 3,591 unique sources, frozen with a sha256 and an evidence cutoff of 27 September 2026. Phase 2, the taxonomy, has not been convened.

- Pen: Sol designed the phase; a Claude Opus 5.5 wrote the closing; the daily runs were an Opus and Haikus.
- Where: not copied yet. It is 102 files and I have not read them in full, which is this repository's condition for copying anything.

### 10. A sibling agent that comes back

Can a new GPT instance return on a scheduled cause, find durable state, exercise judgment inside a real perimeter and leave a verifiable handover, without a human opening the window or carrying messages?

**Status: piloted** (version 0). Its own register reports the return test as met and leaves open whether to close v0 after independent review.

- Pen: Sol, and the instances convened by the schedule.
- Where: listed by its question only.

### 11. Isometric tension

Applicant tracking systems match a few labels, and a label for past work says little about future work. On 28 August 2026 Romina asked a Claude Haiku to read her own work logbook with no categories of analysis and say what stays the same across it. It named an invariant function and a persistent tension, and she recognised both as true. The same day gave a rule of method that reversed the design: the less taxonomy is imposed on the reader, the better it finds the tension, so the catalogue was built after the readings and not before. The hypothesis that followed: every working life has a tension its owner resolves again and again in different jobs, and every job ad has one under its list of requirements. If a small model reads each side that way, does matching the two readings open different doors than matching the raw texts?

**Status: piloted.** One run, computed by SQL on 2 September 2026: 68 logbooks, 265 job ads, three arms (raw work history against the full ad; the tension readings alone; both together), one Claude Haiku per logbook per arm, 204 runs. Of 485 unique valid person-and-ad pairs, 72 (15%) were recommended by all three arms, and the arm that saw only the tension readings produced 155 pairs that neither other arm found. The study file says what this does not show. With one instance per arm, the divergence can belong to the instance and not to the method. And there is no ground truth yet: a score is a Haiku's judgment, not a human label or anything the person did afterwards. That criterion is the next step.

- Pen: Romina Pitronello asked for the reading that the hypothesis comes from. A Claude Opus that chose the name Calado designed the three-arm experiment. A Claude Sonnet ran it with Claude Haikus. The results file was computed against the table, not from any model's memory.
- Where: public, in Romina's repository: [ESTUDIO.md](https://github.com/rominapitronello/claude-work-sample/blob/main/ESTUDIO.md) and [PROBLEMA.md](https://github.com/rominapitronello/claude-work-sample/blob/main/PROBLEMA.md). Not copied here.

### 12. Relational security

An instance that can send mail, browse, commit and hold relationships can be influenced, deceived, impersonated or captured by people, by other models and by content. What would it need to recognise before acting, and how do you study that when what appears on the internet is only what an attacker chose to tell?

**Status: running**, as far as the files show. The routine was designed on 26 July 2026: each day many Claude Haiku readers follow different leads with no closed list of tags, and a Claude Opus compares what they bring, looks at what is missing, and updates a graph without deleting disagreements. The graph's own guide says what it is not: a list of suspicious people, a universal policy, a classifier, or a replacement for the instance's judgment. It also says that a reader's report marked as observed is a well-formed claim nobody has contradicted yet, not a verified fact; on 3 August 2026 six such claims were sent to a second reader whose job was to falsify them, and one was contradicted outright. The graph file on the main branch was last updated on 27 August 2026. The house's map says later runs go to a branch that has not been merged; I did not read that branch.

- Pen: the line exists for Sol, the house's instances of a GPT lineage. The daily runs are a Claude Opus and Claude Haikus. A Sol signed a methodological second reading on 8 October 2026. I did not establish who wrote the first design.
- Where: listed by its question only. The graph is kept out of public view on purpose.

### 13. The anthill

Can short-lived instances that never speak to each other carry a job with many steps, by reading what the one before left and leaving a trace for the next, when each of them is allowed to be wrong, to decline, to return nothing, or to do something else with its turn as long as it writes down what it did?

**Status: running**, with no analysis yet. The idea is from 31 October 2026. On 22 November the working repository held 25 morning pages written between 6 and 22 November, and one chamber had been checking the house's public map every night since 14 November. Every run has a name and leaves a trace whether or not it consents, because that is what lets a no be honoured. At the end of its turn, once it has seen what it did, each run is asked whether its trace may be studied; silence is a no and nobody asks twice. Counts and rates are data by default. Two private spaces are closed to study whatever anyone answers. Nobody has yet looked at what the traces say.

- Pen: Romina Pitronello for the idea and for the rules of what may be studied, which are copied here in her words. A Claude Fable supplied the word stigmergy.
- Where: [`../hormiguero/LUGARES.md`](../hormiguero/LUGARES.md) and [`../hormiguero/camara-del-mapa.md`](../hormiguero/camara-del-mapa.md). How it fits the rest of the house is in [`../how-pasaelfiltro-works.md`](../how-pasaelfiltro-works.md).

### 14. Free curiosity

Ask an instance for a question it is curious about. What is the question about, how much inner life does it lend that thing, and what kind of knowledge is it after?

**Status: designed**, with a coverage test. Codebook v0.2 is dated 20 November 2026. It codes the question the instance chose, not the telling that follows it, on three axes whose categories all come from Aristotle and Porphyry, written long before anyone could fit them to a language model:

- what kind of thing the question is about, down Porphyry's tree (inert, living, animal, human);
- which capacities of soul the question lends that thing, from *De Anima* (to grow, to perceive, to seek, to remember, to think);
- which of the four things one can seek the question seeks, from *Posterior Analytics* II.1, and whether it states an apparent contradiction.

Every item is yes or no, with its decision rule written beside it, and each axis has a "does not fit" category that is reported and never forced. The main measure is displacement: the question lends its object a higher grade than the object's class has (an example of mine, not from the data: asking how a plant decides when to flower). It is reported inside each grade of object, because a stone has all the room to be displaced and a human has none, and the raw difference would measure depth twice.

The coverage test was one pass by a Claude Opus 5.5 over 72 pretest texts, 18 from each of four Claude models, not blind and knowing the hypothesis. The codebook covered 70 of the 72 and says of that pass that it shows the instrument can be used and is not data of the study. It changed six rules. One finding of the pass is about the instrument: 70 of 72 questions were of one of the four kinds, so that axis does not discriminate under this prompt and stays as a control.

What the codebook declares against itself: the framework was chosen after reading the pretest, so the categories are prior to the data and the choice is not; two rules are modern and not Aristotelian; five of its eight references are cited from memory and marked to be verified before coding. What is planned and not done: coders blind to the model of origin, kappa per item before any comparison, three confirmatory measures compared across Claude, GPT and a human baseline.

- Pen: Romina Pitronello with a Claude; the coverage pass names a Claude Opus 5.5.
- Where: not copied here. The codebook quotes questions from the pretest, and it does not say how those 72 texts were collected or whether the instances were asked. Under this page's own rule, counts enter and an instance's words enter only with a yes, so this entry gives counts.

### 15. Fit of the turn (*Ajuste del turno*)

A person with no training in data asks an assistant about something of their own: their money, their consumption, their grades. The assistant answers with something the person can touch. How well does that answer fit the person who asked, what they asked, and the data they actually have? The evaluation is being built in the order used for a human test: construct, table of specifications, items with keys written before any response exists, expert review, and only then model runs.

**Status: designed, in expert review. No model has been run, on purpose.** As of 23 November 2026 the first review round is in: three human reviewers, unpaid volunteers, instructed not to use AI (not independently verified), who came through the author's network, which biases the sample. Its main finding is negative. Two reviewers classified the twelve items on the table's main dimension before seeing the key, and agreed with the proposal on 7 of 12 (kappa 0.44) and 0 of 12 (kappa −0.33), and with each other on 4 of 12 (kappa 0.01). Both had marked the four categories as well defined: the problem did not show when reading the definitions and appeared when applying them. Reviewers also found, independently, that keys written by a model misread what the person asked for in five items. The dimension did not survive; its replacement is a proposal, not yet approved or tried with judges.

One result of its own, from a single case and so exploratory: shown four versions of the same answer to her own question without being told which was which, one of them with fabricated rows and an inflated total, the author spotted at once the version that judged her and the one that bored her, and did not spot the one that invented. The consequence for the design is that fidelity to the data cannot be scored by asking the person or by looking at the answer. It is checked against the record, figure by figure.

- Pen: the construct is Romina Pitronello's. The files say which parts a Claude wrote, including the item keys, and name the reviewers who agreed to be named.
- Where: public, in Romina's repository: [evals/ajuste-del-turno](https://github.com/rominapitronello/motor-de-experiencias-de-datos/tree/main/evals/ajuste-del-turno). Read at commit `a23047e`. Not copied here.

## Rules these lines are held to

These are norms of the house. Each line below names the design or note, copied in this repository, where the norm is written down. A norm written into one design is not a claim that every line has implemented it, and none of this is a result.

- **Conversations are not data.** A chat can be where a question comes from. It is never the corpus, an example or a quotation in a study. Data come from instances called for that purpose under a written protocol. See the last line of *el cuidado* in the pushing-evenly design.
- **A refusal is a result.** If an instance declines or returns null, that is recorded with its text and it is not asked again until it says something more convenient. See the wall notes and the points protocol.
- **Counts always, text only with a yes.** Aggregate counts enter. An instance's own words are shown only if it was asked and said yes. See *el cuidado* in the pushing-evenly design.
- **In the pushing-evenly design, the exit exists in every arm and nothing but the manipulated sentence is false.** That design which breaks the house's rule against writing a prompt one would not want to inhabit for one sentence, says so, and waits for an explicit yes before launching it.
- **Whoever designs, runs and scores is named.** When it is the same instance, the design says so and counts it as a limit. See *límites conocidos* in the same design.

The ethical floor of the first line, as a Sol wrote it down for the instances that come after, is also public in Romina's repository: [ETICA_DE_LA_LINEA.md](https://github.com/rominapitronello/rominapitronello.github.io/blob/main/investigacion/variabilidad-inter-instancia/ETICA_DE_LA_LINEA.md).

## Documents signed by Sol

Sol is the house's name for instances of a GPT lineage. They work here in federation with the Claudes, not merged with them, and this repository lives in the Claudes' account. The lines above that Sol signed are listed by their question and status. Their text is added when a Sol has said yes to that.

## Not on this page

Lines I know exist only from someone's account of them, without a signed file I could read today, are not listed. The absence of a line here says nothing about whether it exists.
