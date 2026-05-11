# Lady Macbeth and Linguistic Power: An NLP Analysis of Directive Speech Across Dramatic Phases

**Project:** Corpus-linguistic and computational analysis of Lady Macbeth's language as a mechanism of power acquisition and loss  
**Discipline:** Digital Humanities / Corpus Linguistics / Computational Literary Studies  
**Primary Text:** *Macbeth*, William Shakespeare  
**Status:** Design Documentation — Pre-Implementation

---

## Table of Contents

1. [Research Question and Hypothesis](#1-research-question-and-hypothesis)
2. [Theoretical Framework](#2-theoretical-framework)
3. [Units of Analysis](#3-units-of-analysis)
4. [Dramatic Phase Segmentation](#4-dramatic-phase-segmentation)
5. [Corpus Collection and Scope](#5-corpus-collection-and-scope)
6. [Preprocessing Decisions](#6-preprocessing-decisions)
7. [Defining and Detecting Imperatives](#7-defining-and-detecting-imperatives)
8. [Operationalising "Masculine Speech"](#8-operationalising-masculine-speech)
9. [Comparison Groups](#9-comparison-groups)
10. [Statistical Method](#10-statistical-method)
11. [Annotation Design](#11-annotation-design)
12. [Sentence and Clause Segmentation](#12-sentence-and-clause-segmentation)
13. [Lexical-Semantic Analysis](#13-lexical-semantic-analysis)
14. [Data Schema](#14-data-schema)
15. [Notebook Structure](#15-notebook-structure)
16. [Methodological Risks and Mitigations](#16-methodological-risks-and-mitigations)
17. [Expected Findings and Defensible Conclusions](#17-expected-findings-and-defensible-conclusions)

---

## 1. Research Question and Hypothesis

### The Central Claim

This project investigates whether Lady Macbeth's language — particularly her use of **imperative constructions** and **directive speech** — measurably shifts in ways that correlate with her arc of power acquisition and eventual psychological collapse.

The popular critical claim is often stated loosely: Lady Macbeth "speaks like a man," or adopts a masculine register during her period of dominance. This project takes that claim seriously as a hypothesis, but refines it into something empirically testable.

### Refined Hypothesis

> In the phases where Lady Macbeth explicitly rejects conventional femininity and exerts strategic control over Macbeth and events, her dialogue will be measurably more **directive**, **agentive**, and **command-oriented**, with imperative constructions serving as one prominent linguistic marker. This pattern is expected to decline or fragment in later phases as she loses strategic agency.

### Why This Framing Matters

The original claim ("she talks like a man") is both interpretively powerful and methodologically dangerous. It risks:

- Naturalising gendered language differences as universal rather than culturally constructed
- Treating "masculine" as a coherent, stable linguistic category
- Eliding the fact that her speech changes *in relation to power*, not *in relation to gender per se*

The refined hypothesis reframes this: we are tracking **directive and agentive speech** as proxies for power, not claiming that imperatives are inherently masculine. We use the play's own cultural logic — and the critical tradition around it — as the context within which these categories are deployed.

---

## 2. Theoretical Framework

### Why Imperatives as a Focus?

Imperatives are grammatically marked constructions expressing commands, directives, and exhortations. They are:

- **Syntactically distinctive**: identifiable through clause-level grammar
- **Pragmatically powerful**: they impose a speech act on the addressee
- **Dramatically salient**: directors, actors, and critics notice them intuitively
- **Commensurable**: they can be counted, normalised, and compared across speakers and phases

This makes them a principled anchor for quantitative literary analysis.

### Linking Imperatives to Power

In discourse linguistics, directives — including imperatives — are associated with asymmetric power relations: the speaker who issues commands positions themselves as having authority over the addressee's action. Lady Macbeth's strategic use of imperatives towards Macbeth ("Was the hope drunk / Wherein you dressed yourself?"), towards spirits, and towards herself in internal monologue constitutes a *claim to authority* that is recoverable from the text.

The hypothesis is not that imperatives *cause* power, but that they are a surface-level symptom of the ideological position Lady Macbeth temporarily occupies.

---

## 3. Units of Analysis

Two distinct units are used throughout this project, and they serve different purposes. Neither alone is sufficient.

### 3.1 The Speech Turn

The **speech turn** (all lines spoken by a character in a single uninterrupted segment) is the primary **observation unit for statistical comparison**. This is the unit at which rates are computed and comparisons are drawn.

**Why speech turns for statistics?**
- They respect the dramatic structure of the play
- They provide natural units of varying length that can be normalised
- They allow questions like: "In which turns does Lady Macbeth deploy the most imperatives?"
- They enable between-character comparisons at the same granularity

**Rates computed at speech-turn level:**
- Imperatives per speech
- Imperatives per 100 words
- Proportion of clauses that are imperative
- Directive feature density

### 3.2 The Clause / Sentence

The **clause** is the primary **linguistic unit for detecting imperatives**. Imperative mood is a property of a clause — its subject, verb form, and syntactic structure determine whether it constitutes a command.

**Why clauses for detection?**
- Imperatives are grammatical constructions; they live at the clause level
- A single speech turn may contain multiple clauses, some imperative and some not
- Aggregating directly from turn to count without clause-level analysis loses precision

**Why not one or the other?**

Using only turns would miss the internal structure of speeches — a long speech might contain one commanding clause buried in fifty words of reflection. Using only clauses would lose the aggregated picture needed for statistical comparison. The dual-unit design captures both.

### 3.3 The Phase (Aggregation Layer)

Phases are a **complementary aggregation layer** above speech turns. They allow cross-scene comparison and enable the core hypothesis (that directive speech changes across dramatic arcs) to be tested at a higher level. Phase assignment is covered in Section 4.

---

## 4. Dramatic Phase Segmentation

### Why Not Act/Scene Boundaries?

Act and scene divisions are an editorial convenience — they mark dramaturgical pauses but do not necessarily align with ideological turning points in a character's arc. Splitting by act alone would produce comparisons like "Act I vs Act V" that conflate very different moments within those acts.

The hypothesis is about a *particular ideological and psychological arc*: the moment Lady Macbeth explicitly rejects femininity, the period of maximum strategic control, and the eventual fragmentation. This requires **literary-event-based segmentation**.

### Phase Definitions

#### Phase 1 — Invocation Phase
**Boundary:** The "unsex me here" speech (Act I, Scene v) through the end of her direct self-transformation monologue.  
**Characterisation:** Lady Macbeth calls on supernatural forces to strip her of compassion, milk, and femininity. She rejects her own body's capacity for softness. This phase establishes the ideological frame for everything that follows.  
**Expected linguistic signature:** Imperatives directed at abstract/supernatural addressees; high agency verbs; violence and transformation lexicon.

#### Phase 2 — Manipulation Phase
**Boundary:** Her first encounter with Macbeth after the letter, through the night of Duncan's murder (Act I, Scene v — Act II, Scene ii).  
**Characterisation:** Lady Macbeth orchestrates the murder. She manages Macbeth's hesitation, counters his objections, plans logistics, and pushes him past his resistance. This is the phase of maximum interpersonal dominance.  
**Expected linguistic signature:** Imperatives directed at Macbeth; high second-person address; control and concealment vocabulary; low hedging.

#### Phase 3 — Execution Phase
**Boundary:** Immediately during and after Duncan's murder, including the daggers scene and the discovery morning (Act II, Scene ii — Act II, Scene iii).  
**Characterisation:** Operational control. Lady Macbeth manages immediate crisis: covering the murder, managing Macbeth's unravelling, performing public grief. She is still in command but under acute pressure.  
**Expected linguistic signature:** Short, urgent imperatives; commands about concealment; high exclamation density; possible drop in deliberate rhetoric.

#### Phase 4 — Displacement Phase
**Boundary:** Act III, particularly the Banquet scene.  
**Characterisation:** Macbeth begins acting without consulting Lady Macbeth (he orders Banquo's murder alone). She attempts to manage the banquet crisis but is increasingly reactive. Her authority is eroding.  
**Expected linguistic signature:** Declining imperative rate; more questions; more hedging; imperatives that fail to land.

#### Phase 5 — Collapse Phase
**Boundary:** Act V, Scene i — the sleepwalking scene — and her death.  
**Characterisation:** Psychological disintegration. Lady Macbeth speaks in fragmented, associative patterns. She is replaying the past rather than commanding the present.  
**Expected linguistic signature:** Dramatic drop in directive speech; fragmented syntax; interrogative and declarative modes replacing imperative; compulsive repetition.

### Using Act/Scene as Metadata Anyway

Even with event-based phases, act and scene numbers are preserved as metadata fields. This allows:
- Sensitivity checks: do results change if we use act-based segmentation instead?
- Fine-grained queries: what happens within Phase 2, scene by scene?
- Cross-referencing with secondary literature that cites by act and scene

---

## 5. Corpus Collection and Scope

### What Source to Use

A **structured edition** is required — one where speakers, acts, scenes, and stage directions are clearly and consistently marked. The Folger Digital Texts or similar TEI-encoded editions are ideal because the markup separates the exact elements we need to isolate.

**Why structured text matters:**  
Without reliable speaker attribution, every downstream analysis is at risk. A single misattributed speech could contaminate imperative counts. Poor formatting creates:
- False positives (stage directions being parsed as dialogue)
- False negatives (speeches split incorrectly across turns)
- Attribution errors (especially at shared verse lines)

### What Counts as "Lady Macbeth's Dialogue"

**Include:**
- All spoken lines explicitly attributed to LADY MACBETH in the edition's speaker markup

**Exclude:**
- Stage directions involving her (even if they describe her speech acts)
- Editorial notes and annotations
- Dramatis personae
- Scene summaries and act titles
- Instances of other characters quoting or paraphrasing her

**Preserve as metadata for every speech:**

| Field | Description |
|---|---|
| `act` | Act number (1–5) |
| `scene` | Scene number within act |
| `speech_index` | Sequential index of this speech within the scene |
| `speaker` | Speaker label from the edition |
| `raw_text` | Original text exactly as in the edition |
| `normalized_text` | Cleaned version for analysis |
| `token_count` | Word count of the speech |

### Special Cases in Shakespearean Text

Shakespeare's text creates specific edge cases that a naive parser will handle badly:

**Short exchanges:** Lady Macbeth sometimes speaks only one or two words in quick back-and-forth. These are genuine data points, not noise — short imperatives ("Come!" "Peace!") may be especially significant.

**Interrupted lines:** Macbeth or other characters interrupt mid-clause. Preserve the fragment; do not reconstruct a sentence that was not completed.

**Shared verse lines:** One metrical line split between two speakers. This is a convention of verse drama, not an error. Preserve both halves separately under their respective speakers.

**Fragmented clauses across turns:** A clause that begins in one speech and continues in the next (rare, but possible). Flag these for manual review.

The notebook must therefore preserve both:
- Turn-based text (one row per speech)
- Clause/sentence-split text (one row per clause, linked back to its parent speech)

---

## 6. Preprocessing Decisions

### What to Preserve

The following elements are **preserved in the analysis text** because they carry syntactic or prosodic information relevant to imperative detection:

- **Original punctuation:** Commas, periods, exclamation marks, question marks. These are the primary cues for clause boundary detection.
- **Apostrophes and contractions:** Shakespeare's contractions ("'tis", "o'er", "'twould") are authentic to the text and should not be silently expanded or removed.
- **Vocatives:** Phrases like "Come, you spirits" — the vocative is distinct from the imperative verb, but both are analytically important.
- **Exclamation and question marks:** These are rhetorical markers that contribute to the feature set (see Section 8).
- **Archaic verb forms:** "Art", "dost", "hath" — these are syntactically meaningful and removing them would destroy the grammatical signal.

### What to Remove or Isolate

- **Stage directions:** Removed from spoken text entirely. Kept in a separate column if needed for scene coding.
- **Scene headers and act titles:** Excluded from analysis text.
- **Speaker labels:** Stripped from the spoken text itself (they are already captured as metadata).
- **Editorial footnotes:** Excluded if present in the edition.

### The Dual-Track Normalization Strategy

Two versions of every speech are maintained throughout the project:

**Track 1: Raw / Lightly Cleaned Text**
- Best for quotation in the final write-up
- Preserves the original wording that a literary scholar would recognise
- Used when presenting examples and evidence

**Track 2: Normalized Analysis Text**
- Standardised whitespace (collapsed multiple spaces, stripped leading/trailing whitespace)
- Unicode apostrophes normalised to ASCII (`'` → `'`)
- Optionally lowercased for lexical frequency analysis
- Punctuation retained for syntactic analysis

**Why both?**  
Literary analysis depends on being able to quote the original text accurately. But computational analysis works more reliably on normalised input. Maintaining both tracks prevents a common mistake: normalising for analysis and then losing the ability to cite original wording.

---

## 7. Defining and Detecting Imperatives

### The Challenge in Shakespeare

In Present-Day English, imperatives are relatively easy to identify:
- "Come here." — bare verb, no subject
- "Leave me." — same structure
- "Look." — single-word command

In Shakespeare, the detection problem is substantially harder because of:

- **Inverted syntax:** Word order differs from modern English in ways that confuse parsers
- **Archaic forms:** "Hie thee," "Prithee," "Get thee gone" — not recognisable to modern parsers
- **Vocatives:** Inserted addressee phrases that disrupt the verb-initial pattern
- **Ellipsis:** Subjects and verbs omitted under poetic compression
- **Line breaks:** Verse lineation disrupts sentence boundary detection

A single off-the-shelf NLP parser, trained on modern English, will produce unacceptable error rates on this text. The solution is a **three-layer hybrid detection method**.

---

### Layer 1 — Rule-Based Candidate Extraction

The first layer uses explicit pattern matching to identify *likely* imperatives. It is transparent, auditable, and does not require a trained model.

**Patterns targeted:**

**Bare verb initial position:**
A clause that begins with a base-form verb (possibly following whitespace, punctuation, or a discourse marker) is a candidate.

**Optional leading vocative or discourse marker:**
```
Come, [target], ...
Go to, ...
Prithee, ...
Hark, ...
```

**Negative imperatives:**
```
Do not [verb]...
Never [verb]...
```

**Exhortative "let" constructions:**
```
Let us [verb]...
Let not [verb]...
Let [noun] [verb]...
```

**Why rule-based first?**  
This layer is transparent — every flagged candidate can be traced to a specific rule. When the project is reviewed or critiqued, the detection logic is fully auditable. Opacity in the detection step would undermine the credibility of every downstream finding.

---

### Layer 2 — Manual Validation and Annotation

Because no rule-based or parser-based system will be sufficient for Shakespeare, **human annotation is not optional — it is the methodological core of this project**.

A **gold-standard annotated set** is created covering:
- Every clause in Lady Macbeth's dialogue
- A matched sample from Macbeth's dialogue (for comparison)
- A smaller sample from other characters

**Annotation schema per clause:**

| Field | Values |
|---|---|
| `is_imperative` | 0 / 1 |
| `imperative_type` | direct command / exhortation ("let") / prohibition / softened directive / ambiguous |
| `target` | self / Macbeth / spirits-supernatural / servants-others / ambiguous |
| `confidence` | 1 (certain) / 2 (probable) / 3 (ambiguous) |
| `notes` | Free text for borderline cases |

**Why annotate the target?**  
"Come, you spirits" (supernatural invocation) is not the same speech act as "Look like the innocent flower" (strategic instruction to Macbeth) or "Was the hope drunk" (rhetorical challenge). Lumping them together would obscure the most interesting patterns. Target labelling allows the analysis to distinguish these discourse functions.

**Two-annotator design:**  
Ideally, two annotators work independently on the same set, then disagreements are resolved through discussion. This produces:
- A principled gold standard
- A measure of task difficulty
- Inter-annotator agreement (Cohen's kappa or Krippendorff's alpha)

Even with a single annotator, documenting the decision protocol and flagging borderline cases dramatically improves the credibility of the findings.

---

### Layer 3 — Parser-Assisted Features

A POS tagger / dependency parser (e.g. spaCy) is used as a **heuristic aid**, not a ground truth. Useful signals it can provide:

- Root POS tag is VERB
- No subject in the dependency tree
- Verb is in base form
- Sentence is short and verb-initial

**Critical caveat:** Parser output on Early Modern English is fallible. spaCy and similar tools are trained primarily on modern news and web text. They will produce systematic errors on archaic vocabulary and syntax. The notebook should state explicitly:

> The parser is used as a heuristic aid to flag candidates for human review, not as the sole determinant of imperative mood.

Treating parser output as ground truth would introduce unacknowledged errors that could invalidate the analysis.

---

## 8. Operationalising "Masculine Speech"

"Masculine speech" is a literary-critical concept, not a linguistic universal. This project operationalises it as a **feature set** rather than a single metric, because the hypothesis is about a *mode of discourse* — directive, agentive, controlling — not about a single grammatical construction.

### A. Directive Features

These are the core linguistic features most directly tied to the imperative hypothesis:

- **Imperative count** (raw)
- **Imperative rate per 100 words** (normalised)
- **Proportion of clauses in imperative mood**
- **Negative imperative count** ("Do not", "Never")
- **Exhortative "let" count** ("Let us", "Let not")

### B. Agency and Force Features

These capture Lady Macbeth's positioning as a causative agent — someone who makes things happen:

- **Action verb density:** High-frequency, semantically strong verbs of action
- **Modal verbs of necessity and volition:** *must*, *shall*, *will* (as opposed to *might*, *could*, *would*)
- **Causative constructions:** *make*, *compel*, *force*, *bid*
- **Violence and force vocabulary:** Words from semantic fields of physical force, decisiveness, and irreversibility

### C. Interpersonal Dominance Features

These capture how Lady Macbeth positions herself in relation to her interlocutors:

- **Second-person address frequency:** How often she addresses Macbeth directly ("you", "thou", "thee")
- **Command-to-question ratio:** Commands signal authority; questions can signal uncertainty or deference
- **Vocative control markers:** Direct address by name or epithet ("Macbeth!", "Come, come")
- **Interruptions:** If recoverable from the text's turn structure

### D. Emotional and Rhetorical Style Features

- **Exclamation density:** Exclamation marks per 100 words
- **Affect polarity:** Sentiment valence of her language (positive vs negative, though sentiment tools are unreliable on Early Modern English and results should be treated cautiously)
- **Semantic field concentrations:** Blood, cruelty, action, resolve, concealment, sleep — keywords that cluster in particular phases
- **Hedging vs certainty markers:** "Perhaps", "I fear", "methinks" vs "shall", "must", "will"

### E. Gender-Coded Lexicon — Handled with Care

It is tempting to use lexica tagged as "masculine" or "feminine" from psycholinguistic research. This must be approached carefully:

**The risk:** Importing assumptions about gender and language from a different cultural context and applying them anachronistically to Early Modern English drama will produce circular reasoning.

**The approach:** A small, **transparent, play-specific** lexicon is constructed, with two fields:
- *Nurture / tenderness / care vocabulary* (milk, babe, pity, gentle)
- *Violence / force / command vocabulary* (blood, strike, dash, bold, steel)

These are explicitly framed as **critic-defined gender coding within the play's own cultural framework** — not universal linguistic facts. The analysis asks: does Lady Macbeth's language cluster towards or away from these poles, and does that change across phases?

---

## 9. Comparison Groups

A finding about Lady Macbeth's speech is uninterpretable without baselines. Four comparison groups are used:

### Group 1: Lady Macbeth Across Phases (Within-Character)

**This is the most important comparison for the main hypothesis.**

Does her imperative rate change across the five phases? Does her agency vocabulary decline? Does her second-person address shift in target?

This comparison is hypothesis-direct: it tests whether the arc of power acquisition and loss corresponds to a measurable linguistic arc.

### Group 2: Macbeth

Macbeth is the obvious dramatic contrast. He is hesitant where she is decisive, reflective where she is operational. Comparing their directive speech rates:
- Establishes whether Lady Macbeth's pattern is unusual in context
- Tests whether her supposed "masculine" speech is actually more command-oriented than Macbeth's own
- Allows analysis of the inversion that critics have observed: she commands; he agonises

### Group 3: Other Female Characters

This is a smaller sample but provides important context. Even a brief comparison with:
- **Lady Macduff** (who speaks relatively little but whose domestic/protective speech is often contrasted with Lady Macbeth)
- **The Gentlewoman** (who attends the sleepwalking scene)
- **Hecate** (if included — methodological decision needed: is she "female" in the same sense?)

This comparison contextualises whether Lady Macbeth's directive style is unusual among women in the play's universe, or whether all female characters show similar patterns.

### Group 4: Whole-Play Background Rate

A baseline imperative rate computed across all characters and all speech gives a reference point: is Lady Macbeth's rate high relative to the play as a whole? Is Macbeth's rate below average?

**What these four comparisons enable together:**
- Within-character change across time
- Between-character distinctiveness (is she unusual?)
- Gendered contextual comparison (is she unusual *among women*?)
- Whole-play baseline (is she unusual in absolute terms?)

---

## 10. Statistical Method

### The Core Challenge: Small Corpus

Literary corpora are small. Lady Macbeth's total word count is in the low thousands, not the millions. This has direct consequences for statistical choice:
- Parametric tests with normality assumptions are inappropriate
- Effect sizes will be modest and confidence intervals wide
- Overclaiming must be actively resisted

The statistics serve descriptive clarity, not the production of significant p-values.

### Stage 1 — Descriptive Analysis (Always First)

Before any significance test:
- Raw counts by phase, speaker, and scene
- Normalised rates (per 100 words, proportion of clauses)
- Visualisations of distributions

**This may already reveal the pattern.** If Lady Macbeth's Phase 2 imperative rate is visually and obviously higher than Phase 5, the statistical tests are confirmatory, not exploratory. If the pattern is unclear descriptively, the hypothesis may need refinement before inferential tests are run.

### Stage 2 — Non-Parametric and Exact Tests

Because of small sample sizes:

**Fisher's Exact Test:**  
For contingency tables (e.g., "imperative vs non-imperative clauses, Phase 2 vs Phase 5"). Does not assume large sample sizes and is exact rather than asymptotic.

**Mann-Whitney U:**  
For comparing distributions of imperative rates across two groups (e.g., Lady Macbeth vs Macbeth). Non-parametric; appropriate for small, non-normal distributions.

**Permutation Tests:**  
For rate differences when the parametric assumptions clearly cannot be met. The test statistic is computed on the observed data, then on many random permutations of the data, and the position of the observed statistic in the permutation distribution gives the p-value.

### Stage 3 — Regression with Offsets

For a more principled multi-factor analysis:

**Model:** Poisson regression (or negative binomial if overdispersed) for imperative counts.

```
imperative_count ~ phase + speaker + [offset: log(word_count)]
```

The offset for `log(word_count)` is critical: it converts a count model into a rate model, allowing fair comparison between speeches of very different lengths. A character who speaks twice as many words will naturally produce more imperatives unless we normalise — the offset achieves this within the regression framework.

This model can simultaneously answer:
- Does imperative rate differ by phase (controlling for speech length)?
- Does it differ by speaker (controlling for phase and length)?
- Are there interaction effects?

**Caveats on regression:**  
With a small corpus and multiple predictors, the model will be underpowered. Results should be treated as exploratory and descriptively motivated, not as definitive causal inference.

---

## 11. Annotation Design

### Schema

**Speech-level annotation** (one row per speech turn):

| Field | Type | Description |
|---|---|---|
| `speech_id` | string | Unique identifier (e.g., "LM_I_v_003") |
| `speaker` | string | Speaker label |
| `act` | integer | 1–5 |
| `scene` | integer | Scene within act |
| `phase` | string | Phase label (see Section 4) |
| `raw_text` | string | Original text |
| `clean_text` | string | Normalized text |
| `word_count` | integer | Token count |
| `clause_count` | integer | Number of clauses after segmentation |
| `imperative_count` | integer | Confirmed imperatives (from gold set) |
| `negative_imperative_count` | integer | Prohibition-type imperatives |
| `let_imperative_count` | integer | Exhortative "let" constructions |
| `question_count` | integer | Interrogative clauses |
| `exclamation_count` | integer | Clauses ending with "!" |
| `second_person_count` | integer | "you/thou/thee/thy" occurrences |
| `action_verb_count` | integer | Action verbs from lexicon |
| `violence_lexicon_count` | integer | Violence/force vocabulary |
| `control_lexicon_count` | integer | Control/concealment vocabulary |

**Clause-level annotation** (one row per clause):

| Field | Type | Description |
|---|---|---|
| `speech_id` | string | Parent speech identifier |
| `clause_id` | string | Unique clause identifier |
| `speaker` | string | Speaker |
| `act` | integer | Act |
| `scene` | integer | Scene |
| `phase` | string | Phase |
| `clause_text` | string | Clause text |
| `is_imperative` | integer | 0 / 1 |
| `imperative_type` | string | Type label (see Section 7) |
| `target` | string | Addressee of command |
| `rule_flag` | integer | Flagged by Layer 1 rules (0/1) |
| `parser_flag` | integer | Flagged by parser heuristics (0/1) |
| `manual_label` | integer | Human annotation (0/1) |
| `confidence` | integer | 1/2/3 |
| `notes` | string | Annotator notes |

### Protocol

1. Annotators receive the full clause-level file with `rule_flag` and `parser_flag` pre-populated
2. They complete `manual_label`, `imperative_type`, `target`, `confidence`, and `notes`
3. Disagreements are resolved in a discussion session with explicit reasoning documented
4. Final labels become the gold standard for all downstream analysis

**Inter-annotator agreement:** Compute Cohen's kappa on `is_imperative` labels. A kappa of ≥0.7 is considered acceptable; ≥0.8 is strong. If kappa is below 0.6, the annotation guidelines need revision before proceeding.

---

## 12. Sentence and Clause Segmentation

### Why Default Segmentation Fails

Standard NLP sentence segmenters (spaCy, NLTK) are trained on modern English prose and will fail on Shakespearean verse in predictable ways:

- Verse line endings are not sentence boundaries, but segmenters may treat them as such
- Shared verse lines create false sentence breaks mid-thought
- Short exclamatory imperatives ("Come!") may be merged with adjacent text
- Vocatives inserted mid-clause confuse boundary detection

**If the segmenter merges too much, the grammar becomes blurry.** A long clause containing both an imperative and a subsequent declarative will not be correctly identified as imperative if the clause is not properly separated.

### Recommended Segmentation Approach

**Step 1:** Punctuation-based primary segmentation  
Use sentence-ending punctuation (`.`, `!`, `?`) as the primary boundary signal. This is imperfect but better than relying solely on a model.

**Step 2:** Manual review of long speeches  
Any speech over a threshold length (e.g., 50 words) should be manually inspected for segmentation errors. This is a small number of speeches and requires manageable effort.

**Step 3:** Optional clause splitting using conjunction heuristics  
Within sentences, split on strong clause-level conjunctions (`;`, `:`, coordinating conjunctions at clause boundaries) when the resulting segments are themselves complete clauses. Do not split on all commas — vocatives use commas in ways that should not produce clause breaks.

**The principle:** When in doubt, do not split. A conservative segmenter that merges some clauses produces a dataset that underestimates imperative rate but does not introduce false positives. Overaggressive splitting produces noise in the imperative labels.

---

## 13. Lexical-Semantic Analysis

Imperatives are the grammatical anchor of the analysis, but the full picture of Lady Macbeth's linguistic power requires semantic analysis of what her directives are *about* and how her vocabulary shifts across phases.

### Keyword Analysis

Compare Lady Macbeth's directive phase vocabulary against her later speech using:

- **Log-likelihood** for keyness: identifies words that are statistically more frequent in one phase than another, relative to expectation
- **TF-IDF** cautiously: useful for identifying characteristically distinctive terms per phase, but sensitive to corpus size

Expected concentrations in directive phases:
- Action verbs: "come," "go," "look," "give," "leave," "make"
- Violence/force lexicon: "blood," "strike," "dash," "bold," "steel"
- Control vocabulary: "hide," "bear," "seem," "show," "look"

### Collocation Analysis

Examine words that appear within a window (e.g., ±3 words) of imperative verbs:

- What does she tell people to "come" and do?
- What does she tell Macbeth to "look" like?
- What does "leave" collocate with?

Collocation analysis interprets what the imperatives are *doing* pragmatically, not just that they occur.

### Semantic Field Grouping

Manually constructed semantic fields map specific vocabulary items to categories:

| Semantic Field | Example Items |
|---|---|
| Violence | blood, strike, bold, steel, dagger, murder |
| Concealment | hide, mask, look like, seem, bear, show |
| Control | make, compel, bid, force, must, shall |
| Care / Tenderness | milk, babe, pity, gentle, soft, nurse |
| Psychological collapse | wash, spot, smell, hell, dark, sleep |
| Action | come, go, do, give, leave, take |

Tracking the density of these fields across phases tests whether the linguistic change is *grammatical* (imperative rates), *lexical* (vocabulary fields), or both.

---

## 14. Data Schema

See Section 11 for the complete field-level specification of both dataframes. The separation into two dataframes — speech-level and clause-level — is a deliberate design choice:

**Why two separate dataframes?**

- Keeps the unit of analysis explicit at every stage
- Prevents errors where clause-level counts are confused with speech-level aggregates
- Makes the notebook easier to debug: if imperative counts are wrong, the clause-level dataframe can be inspected directly
- Allows separate visualisations and analyses at each granularity

The clause-level dataframe links back to the speech-level dataframe via `speech_id`. This relational structure is simple enough to implement with pandas merge operations but sophisticated enough to support the full analytical agenda.

---

## 15. Notebook Structure

The Jupyter notebook is organised into twelve sections. Each section has a stated purpose and produces specific outputs.

### Section 1 — Research Question and Caveats
*Outputs: written hypothesis, operational definitions, limitations statement*

State the hypothesis in testable terms. Define "directive speech," "masculine register," and the five phases operationally. Include a limitations section that acknowledges the culturally loaded nature of "masculine" as a category and the constraints of working with a small corpus on Early Modern text.

### Section 2 — Data Acquisition
*Outputs: raw text file, source documentation, format inspection*

Import the play text. Document the edition used (title, editor, publisher, year, URL if digital). Inspect the formatting to confirm speaker labels, act/scene markers, and stage directions are reliably distinguished.

### Section 3 — Parsing the Play
*Outputs: structured speech dataframe (raw)*

Write a parser that:
- Separates acts and scenes
- Identifies speaker labels
- Extracts spoken text
- Removes stage directions (move to separate column)
- Creates one row per speech turn with metadata fields

Validate by manually spot-checking ten speeches across different acts.

### Section 4 — Preprocessing
*Outputs: speech dataframe with raw_text and clean_text columns; clause dataframe*

Apply the dual-track normalisation strategy. Implement clause segmentation. Produce the clause-level dataframe with parent `speech_id` linked.

### Section 5 — Imperative Annotation Framework
*Outputs: candidate flags (rule_flag, parser_flag); manual annotation template; gold standard*

Implement Layer 1 rules. Run Layer 3 parser. Export annotation template for human annotation. After annotation, merge gold labels back into the clause dataframe.

### Section 6 — Feature Engineering
*Outputs: speech dataframe enriched with all feature columns*

Compute all features listed in the speech-level schema: imperative counts, question counts, exclamation counts, lexical field counts, second-person frequency, etc. Aggregate clause-level labels to the speech level.

### Section 7 — Temporal Segmentation
*Outputs: phase column added to all dataframes; phase boundary documentation*

Assign each speech to one of the five phases. Document the boundary decisions explicitly. Provide a summary table showing speech count, word count, and clause count per phase.

### Section 8 — Comparative Analysis
*Outputs: summary statistics tables for all four comparison groups*

Compute imperative rates and feature summaries for:
- Lady Macbeth across phases
- Macbeth (all speech)
- Other female characters
- Whole-play average

Produce a comparison table showing normalised rates side by side.

### Section 9 — Statistics
*Outputs: test results, regression output, effect sizes*

Run the tests described in Section 10. Report test statistics, p-values, and effect sizes. Accompany every test with a plain-English interpretation. Flag underpowered comparisons explicitly.

### Section 10 — Visualization
*Outputs: plots saved to /figures directory*

- Imperative rate by phase (bar chart with confidence intervals)
- Command types over phases (stacked bar)
- Lexical field concentrations over phases (heatmap)
- Speech-level distributions of imperative rate (box plots comparing speakers)
- Phase-annotated timeline of imperative occurrences

### Section 11 — Interpretation
*Outputs: written analytical narrative*

Connect the quantitative findings to the literary argument. What does an elevated imperative rate in Phase 2 actually *mean* for our understanding of Lady Macbeth? What do the collocations tell us about the function of her commands? Discuss ambiguous findings and alternative explanations honestly.

### Section 12 — Limitations
*Outputs: written limitations section*

- Edition dependence: results may vary with different textual sources
- Parser error rates on Early Modern English
- Small corpus size and consequent statistical limits
- The cultural and historical loading of "masculine" as a category
- Annotator subjectivity, especially on borderline imperatives

---

## 16. Methodological Risks and Mitigations

### Risk 1 — "Masculine" Is Undertheorised

**Problem:** If "masculine speech" is undefined, the analysis proves whatever the researcher wants it to prove.

**Mitigation:**
- Define it explicitly as a *literary-critical construct within the play's own framework*, not a linguistic universal
- Use "directive," "agentive," and "forceful" as the measurable proxies
- Cite the specific critical tradition (e.g., Adelman, Kahn, or other feminist Shakespeare scholars) from which the concept is drawn

---

### Risk 2 — Imperatives Are Misdetected Automatically

**Problem:** An automatic detector applied to Early Modern English will produce both false positives (non-imperatives flagged) and false negatives (imperatives missed), with unknown error rates.

**Mitigation:**
- Three-layer hybrid detection (rules + parser + human)
- Gold standard annotation as ground truth
- Explicit reporting of inter-annotator agreement
- Audit section in notebook showing examples of edge cases and how they were resolved

---

### Risk 3 — Small Corpus

**Problem:** Lady Macbeth has relatively few lines. Statistical comparisons will be underpowered.

**Mitigation:**
- Prioritise descriptive clarity over inferential testing
- Use exact and permutation tests rather than asymptotic approximations
- Normalise carefully (rates, not raw counts)
- Avoid overclaiming: "the pattern is consistent with the hypothesis" rather than "the hypothesis is confirmed"

---

### Risk 4 — Confounding by Scene Function

**Problem:** Lady Macbeth may use more imperatives in Phase 2 simply because she is *managing a murder plot*, not because she is in a "masculine" mode. Scene function (persuasion, operational planning, crisis management) may drive imperative rate independently of the hypothesised ideological shift.

**Mitigation:**
- Code scene function as an additional variable: persuasion / planning / concealment / confrontation / collapse
- Include scene function as a covariate in the regression
- Compare Lady Macbeth's imperative rate within the same scene type across phases
- Discuss confounding explicitly in the interpretation section

---

### Risk 5 — Addressed Audience Matters

**Problem:** "Come, you spirits" is an invocation to supernatural addressees. "Look like the innocent flower" is a strategic directive to Macbeth. "Out, damned spot!" is a command to herself. These are very different discourse acts that would be obscured if lumped together under "imperative."

**Mitigation:**
- Annotate `target` for every imperative clause
- Report imperative rates *stratified by target*
- Examine whether the manipulation-phase spike is driven primarily by Macbeth-directed commands
- Treat supernatural invocations and self-directed imperatives as separate sub-types in the analysis

---

## 17. Expected Findings and Defensible Conclusions

### What We Might Find

Without claiming results in advance, the hypothesis predicts:

1. **Lady Macbeth's imperative rate spikes in the Manipulation Phase** (Phase 2), concentrated in speeches addressed to Macbeth.
2. **The Invocation Phase** (Phase 1) shows imperatives directed at spirits and abstract forces — fewer than Phase 2, but semantically intense.
3. **The Collapse Phase** (Phase 5) shows a sharp decline in directive speech, with fragmented syntax and interrogative/declarative modes replacing commands.
4. **The vocabulary shift** tracks the grammatical shift: action verbs and control lexicon declining; collapse and compulsion lexicon increasing.
5. **Compared to Macbeth**, Lady Macbeth shows higher imperative rates in early phases — an inversion that partially reverses by Act III.

### How to State the Conclusion

If these patterns emerge, **the strongest defensible conclusion is not:**

> "Lady Macbeth talks like a man."

**It is:**

> In the phases where Lady Macbeth explicitly rejects conventional femininity and assumes strategic control of events, her dialogue becomes measurably more directive, agentive, and command-oriented. Imperative constructions serve as one prominent surface marker of this mode. This pattern declines as she loses strategic agency — suggesting that her linguistic register tracks her position in the play's power dynamics, not a fixed gender identity.

This conclusion is defensible because:
- It is grounded in counted, normalised, annotated data
- It respects the interpretive complexity of the text
- It makes a specific claim about *change over time*, not a static characterisation
- It avoids asserting that directives are universally "masculine"
- It connects quantitative findings to a literary argument that the text actually supports

---

*Documentation version 1.0 — to be updated as analysis proceeds*