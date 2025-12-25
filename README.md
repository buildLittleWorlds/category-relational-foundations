# Relational Foundations: Categories and Morphisms

**Course 1 of the Category Theory & LLMs Series**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/buildLittleWorlds/category-relational-foundations/blob/main/notebooks/tutorial_01_passage_diagrams.ipynb)

> *"Tell me how everything passes through it, and I will tell you what it is."*
> — Tessery Vold, Year 892

---

## What Is This Course?

You are a research assistant at the Western Archive. The Capital Philosophical Society has asked you to evaluate the work of Scholar Tessery Vold—a natural philosopher who, in Year 892, proposed a radical hypothesis: that *relationships* are more fundamental than objects themselves, and that any entity can be fully characterized by how other entities interact with it.

Your task: **Map the patterns of passage using modern categorical methods and determine whether Vold's relational framework explains how classification systems, creature behaviors, and institutional structures actually work.**

Along the way, you will learn:
- **Categories** as mathematical structures (objects, morphisms, composition, identity)
- **Pre-orders as categories** — how hierarchies encode categorical structure
- **Functors** as structure-preserving maps between systems
- **Natural transformations** — coherent ways to shift between representations
- **The Yoneda perspective** — understanding objects through their relationships
- How categorical thinking applies to classification, language, and data science

---

## The Data

| Dataset | Rows | Description |
|---------|------|-------------|
| `passage_diagrams.csv` | 50 | Creature movements, document flows, lifecycle transitions—objects and morphisms |
| `archive_classifications.csv` | 50 | Hierarchical classification records—pre-order structure |
| `regional_translations.csv` | 50 | Translation between classification systems—functors in action |

---

## The Tutorials

### Core Tutorials (1-6)

| # | Title | Description | Category Theory Concept |
|---|-------|-------------|------------------------|
| 1 | Passage Diagrams | Load data, understand Vold's framework, explore object-morphism structure | Categories, morphisms |
| 2 | The Classification Hierarchy | Analyze Archive classifications as a pre-order category | Pre-orders as categories |
| 3 | Composition and Identity | Trace composite passages, verify identity morphisms | Composition, identity laws |
| 4 | The Preservation Principle | Map translations between regional systems | Functors |
| 5 | The Probing Pattern | Analyze objects by what passes through them | Hom functor, representables |
| 6 | Coherent Shifts | Transform between passage patterns consistently | Natural transformations |

### Extended Tutorials (7-9)

| # | Title | Description | Key Concepts |
|---|-------|-------------|--------------|
| 7 | The Probing Theorem | Vold's key result—objects determined by incoming morphisms | Yoneda Lemma |
| 8 | The Language of Dens | Apply categorical structure to linguistic analysis | Language category, substring relations |
| 9 | Weighted Passages | Add probabilities to morphisms | Enriched categories |

---

## Who Was Tessery Vold?

**Tessery Vold** (Year 856–938) was an Archivist at the Western Archive who spent decades developing a framework that unified seemingly unrelated classification systems across Densworld.

In Year 892, Vold encountered a cataloging paradox: the same creature—the stakdur—was classified differently in Capital records, Western Archive logs, and Quarry naturalist reports. Yet all three classifications captured something true about the creature. How could the same entity have multiple valid identities?

The Capital taxonomists explained this as error or regional variation. Vold found this explanation unsatisfying. The classifications weren't wrong—they were *perspectives*.

Vold began asking a different question: *What if an entity's identity isn't intrinsic, but emerges from its relationships?*

Over the next five years, Vold developed the **Relational Framework**:

> *"Consider the stakdur. You need not describe its claws, its coloring, its size. Simply tell me: what creatures flee when it approaches? What territories does it traverse? What prey does it consume? The stakdur is not a thing. The stakdur is a pattern of passages."*

Her key concepts:
- **Passage Diagrams**: Visual representations of objects and the morphisms between them
- **The Preservation Principle**: Structure-preserving maps reveal deep connections
- **Coherent Shifts**: Transformations that respect underlying structure
- **The Probing Theorem**: Objects are fully determined by how they're probed

---

## The Vold-Pol-Krell Debate

Vold's most significant intellectual engagement was the Year 895 three-way debate with Erris Pol (Form Library) and Marden Krell (Capital critic).

**Erris Pol** argued that Forms exist prior to their manifestation—that the stakdur reads its form from a universal Library.

**Tessery Vold** countered that Forms are epiphenomenal—what we call "the stakdur form" is simply the stable pattern of passages that the stakdur enacts.

**Marden Krell** objected to both: Vold's framework was circular (you can't define objects by relationships if relationships require objects), and Pol's was unfalsifiable (how do you locate the Library?).

The debate was published as "On Forms and Passages" and remains unresolved:

> **Pol:** "The Form precedes the passage. Without the Form, there is nothing to pass."
>
> **Vold:** "The passage precedes the Form. Without passages, how would you know a Form existed?"
>
> **Krell:** "You're both building castles on clouds. Show me the stakdur, and I'll show you its properties."

---

## Prerequisites

- Basic Python (variables, functions, loops)
- Familiarity with pandas DataFrames
- Some matplotlib/visualization experience helpful but not required
- No prior knowledge of category theory (you'll learn it here)

---

## How to Use This Course

**Recommended:** Click the Colab badge for any tutorial. Everything runs in your browser—no installation needed.

**Local setup** (optional):
```bash
git clone https://github.com/buildLittleWorlds/category-relational-foundations.git
cd category-relational-foundations
pip install pandas numpy matplotlib seaborn networkx
jupyter notebook
```

---

## Series Navigation

This is **Course 1** in the Category Theory & LLMs series:

1. **Passage Diagrams** (Tessery Vold) — Categories and morphisms ← *You are here*
2. **Weighted Passages** (Merrit Vance) — Enriched categories and attention
3. **Document Functors** (Lorren Dray) — Presheaves and document representations
4. **Natural Transformations** (Gellen Tross) — Coherent shifts between representations
5. **The Probing Lemma** (Pelleth Strand) — The Yoneda perspective on embeddings
6. **Linguistic Categories** (Corren Moll) — Language structure as category
7. **Attention and Enrichment** (Brennet Kell) — Full transformer architecture

---

## Connections to Other Densworld Courses

| Related Course | Connection |
|----------------|------------|
| **The Form Library** (Erris Pol) | Pol's Forms are objects; Vold asks how they relate |
| **Hierarchy of Minds** (Pell Anster) | Anster's hierarchies are pre-order categories |
| **Basin Topology** (Vornis Keth) | Keth's flows are morphisms; basins are objects |
| **Constellation Theory** (Pemlik Tross) | Tross's graphs have categorical structure |

---

## About Densworld Courses

Densworld courses teach real technical skills using data from a fictional universe. You can't copy answers because no one else has analyzed this data. The skills transfer; the context is unique.

**Learn more:** [buildLittleWorlds](https://github.com/buildLittleWorlds)

---

> *"The creature did not invent its relationships. It discovered them. The question is: where do relationships come from? I say: from other relationships. It is passages all the way down."*
> — Tessery Vold, "Patterns of Passage," Year 893
