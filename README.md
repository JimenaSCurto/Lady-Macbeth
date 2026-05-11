Academic Report available in directory: Lady Macbeth: Unsex Me Here: Language, Power, and the Making of Lady Macbeth

# README — Lady Macbeth and Linguistic Power

Full results available in the HTML notebook:

## Objective and Hypothesis

This project investigates the relationship between **linguistic form** and **dramatic power** in Shakespeare’s *Macbeth*, focusing specifically on **Lady Macbeth**. The objective is to determine whether shifts in her **authority** and **psychological state** are reflected in measurable linguistic patterns.

The central hypothesis is that, during phases in which Lady Macbeth exerts **strategic control**, her language becomes more **directive**, **agentive**, and **command-oriented**. This is operationalised primarily through the use of **imperative constructions** and related markers of **interpersonal dominance**. The hypothesis further anticipates that, as her authority declines, these features will **weaken or fragment**, reflecting a loss of agency. 

To test this, the analysis divides Lady Macbeth’s dialogue into five **dramatic phases**: **Invocation**, **Manipulation**, **Execution**, **Displacement**, and **Collapse**, corresponding to key structural moments in the play. 

## Methodology

The dataset consists of the full text of *Macbeth* (Project Gutenberg edition), from which all dialogue is extracted and structured by **speaker**, **act**, and **scene**. Lady Macbeth’s speeches are then assigned to one of the five predefined **dramatic phases** using rule-based mappings tied to act–scene boundaries.

The analysis proceeds through several layers of **linguistic feature extraction**. **Directive speech** is identified through a hybrid method combining **rule-based detection**, **syntactic heuristics**, and **manual validation**. Imperative frequency is measured both as **raw counts** and **normalised rates per 100 words**.

Additional features include:

* **Modal verbs** (obligation, intention, possibility)
* **Lexical fields** (violence, control, care)
* **Second-person pronoun usage** (dominance marker)
* **First-person singular pronouns** (self-focused cognition)

The analysis also distinguishes between **rhetorical challenge questions** and **genuine inquiries**, based on evaluative or confrontational vocabulary. **Collocation analysis** identifies semantic patterns surrounding imperative verbs, and **keyword analysis (log-likelihood)** identifies vocabulary statistically distinctive to Lady Macbeth.

Comparisons are made across four groups:

1. **Lady Macbeth across phases** (primary test)
2. **Macbeth** (contrastive figure)
3. **Other female characters**
4. **Whole-play baseline** 

Given the **small corpus size**, the statistical approach prioritises **descriptive clarity**. Inferential methods (Fisher’s exact test, Mann–Whitney U, permutation tests, Poisson regression) are used cautiously and treated as **exploratory**. 

## Results and Interpretation

The results do not support a **simple linear relationship** between directive language and power. Instead, they reveal that the **form**, **function**, and **context** of directive speech shift significantly across phases.

**Imperative frequency** increases across the dramatic arc rather than decreasing. In Phase 1 (Invocation), the rate is **0.35 per 100 words**, rising to **1.65 in Phase 2**, and reaching **4.82 in Phase 5 (Collapse)**. 

However, the interpretation depends on **function**, not just frequency.

In **Phase 1 (Invocation)**, imperatives are directed toward **supernatural entities** and function as **invocations**, not interpersonal commands. These are **performative speech acts**, oriented toward **summoning power** rather than exercising it.

In **Phase 2 (Manipulation)**, imperatives shift toward **interpersonal dominance**. They are directed at **Macbeth** and serve a clear function: **overriding hesitation** and enforcing action. This phase represents the strongest alignment between **directive language and effective power**. The commands are **targeted**, **strategic**, and embedded in persuasive discourse.

In **Phases 3 and 4 (Execution and Displacement)**, imperative usage remains relatively high, but becomes **reactive rather than strategic**. Commands persist, but they are tied to **crisis management**, indicating that **surface-level directive language can persist even as authority weakens**.

In **Phase 5 (Collapse)**, imperative frequency is highest, but qualitatively different. The language is **fragmented**, **repetitive**, and detached from actionable context. Rather than exerting control, it reflects **compulsive cognition** and **psychological disintegration**. This demonstrates that **imperative density alone is not a reliable proxy for power**.

**Modal verb analysis** reinforces this pattern. In the Manipulation phase, there is an increase in **obligation markers** (“must”, “shall”), indicating **assertive authority**. In the Collapse phase, these disappear, and modal usage shifts toward forms associated with **repetition and internalisation**, consistent with loss of control.

**Speech length** declines sharply across phases. Early speeches are **long and structured** (mean of 141.5 words in Phase 1), while later phases show **short, fragmented speech** (around 20 words in Phases 3–4).  This reflects a loss of **rhetorical coherence** and **cognitive organisation**.

Comparisons with other female characters show that Lady Macbeth’s language is **distinctly atypical**. For example, **Lady Macduff shows no imperative usage**, while Lady Macbeth’s imperative rate in Phase 2 is substantial. Control-related vocabulary and certainty markers are significantly higher in Lady Macbeth’s speech.  This supports the interpretation that she occupies a **linguistically marked position** relative to conventional femininity.

Comparison with **Macbeth** shows that Lady Macbeth’s language is more **directive and controlling** in early phases, while Macbeth’s is more **deliberative and hesitant**. This aligns with the dramatic inversion in which she temporarily assumes the role of **strategic initiator**.

**Semantic analysis** reveals a shift from **violence, control, and concealment vocabulary** in early phases to **psychological and obsessive vocabulary** in the Collapse phase (e.g. blood, washing, sleep). This reflects a transition from **external agency to internal compulsion**.

The analysis of **question types** adds further nuance. In the Manipulation phase, Lady Macbeth uses **rhetorical challenge questions** that function as tools of **dominance**, embedding evaluative or contemptuous language. In contrast, Lady Macduff’s questions are **genuine inquiries**, expressing **uncertainty and vulnerability**.

Finally, **self-referential language** shows shifts in cognitive orientation. Early phases involve **high self-reference linked to transformation**, while the Manipulation phase shows reduced self-focus as attention shifts outward. In the Collapse phase, self-reference becomes **fragmented and distress-oriented**, consistent with patterns observed in **psychological linguistics**. 

## Conclusion

The findings refine the original hypothesis. While **directive language correlates with power**, it is not sufficient on its own to indicate control. The relationship between language and power is mediated by **function**, **context**, and **coherence**.

Lady Macbeth’s linguistic trajectory moves from **performative invocation**, to **strategic interpersonal control**, to **reactive management**, and finally to **compulsive and fragmented speech**. The analysis shows that computational methods can capture these transitions with precision, supporting and refining established literary interpretations.

More broadly, the project demonstrates that linguistic features can encode both **social dominance** and its **erosion**, offering a framework for integrating **computational analysis** with **interpretive literary study**.
