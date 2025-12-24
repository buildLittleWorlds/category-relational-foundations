# Dataset Reference Card: Relational Foundations

**Course:** Categorical Philosophy Series — Course 1
**Scholar:** Tessery Vold (Year 856–938)
**Framework:** Passage Diagrams / Relational Philosophy

---

## Quick Reference

| Dataset | Rows | Category Theory Analog | Primary Use |
|---------|------|----------------------|-------------|
| `passage_diagrams.csv` | 50 | Objects and morphisms | Tutorial 1-3, 5, 7, 9 |
| `archive_classifications.csv` | 50 | Pre-order category | Tutorial 2 |
| `regional_translations.csv` | 50 | Functors, Natural transformations | Tutorial 4-6 |
| `linguistic_containment.csv` | 50 | Language category | Tutorial 8 |

**Load Pattern:**
```python
import pandas as pd

BASE_URL = "https://raw.githubusercontent.com/buildLittleWorlds/densworld-datasets/main/data/"

passages = pd.read_csv(BASE_URL + "passage_diagrams.csv")
classifications = pd.read_csv(BASE_URL + "archive_classifications.csv")
translations = pd.read_csv(BASE_URL + "regional_translations.csv")
linguistic = pd.read_csv(BASE_URL + "linguistic_containment.csv")
```

---

## Dataset 1: passage_diagrams.csv

**Description:** Records of passages between objects—creature movements, document flows, lifecycle transitions, intellectual developments. Each row represents a morphism in a category.

**Category Theory Interpretation:**
- Each row is a morphism f: A → B
- `source_object` = domain A
- `target_object` = codomain B
- `morphism_type` = classification of the morphism
- `composition_with` = reference to g where this morphism composes as f ∘ g
- `reversible=true` + matching inverse = isomorphism

### Schema

| Column | Type | Description |
|--------|------|-------------|
| `passage_id` | string | Unique identifier (PD-NNN) |
| `source_object` | string | Origin/domain of passage |
| `target_object` | string | Destination/codomain of passage |
| `morphism_type` | string | Type: creature_passage, identity, lifecycle_passage, etc. |
| `region` | string | Geographic region where observed |
| `observation_date` | date | When the passage was documented |
| `frequency` | string | How often: daily, seasonal, tidal, constant, etc. |
| `reversible` | boolean | Whether passage can be reversed |
| `composition_with` | string | ID of morphism this composes with (if any) |
| `observer` | string | Who documented the passage |
| `notes` | string | Additional context |

### Key Patterns

**Identity morphisms** (morphism_type = "identity"):
```python
identities = passages[passages['morphism_type'] == 'identity']
# stakdur_territory → stakdur_territory, etc.
```

**Composition chains** (composition_with not null):
```python
compositions = passages[passages['composition_with'].notna()]
# These reference earlier morphisms they compose with
```

**Reversible pairs** (isomorphisms):
```python
reversible = passages[passages['reversible'] == True]
# Tidal movements, daily routes, etc.
```

### Example Rows

| passage_id | source_object | target_object | morphism_type | reversible | composition_with |
|------------|---------------|---------------|---------------|------------|------------------|
| PD-001 | stakdur_territory | reed_marsh | creature_passage | false | |
| PD-005 | stakdur_territory | stakdur_territory | identity | true | |
| PD-009 | boundary_zone | capital_outskirts | creature_passage | false | PD-008 |

---

## Dataset 2: archive_classifications.csv

**Description:** Hierarchical classification records from the Capital Archive and related systems. Each row represents an inclusion relationship in a pre-order category.

**Category Theory Interpretation:**
- Objects = categories/items
- Morphisms = "is subcategory of" relationships
- At most one morphism between any two objects (pre-order property)
- Reflexive (identity) and transitive (composition)

### Schema

| Column | Type | Description |
|--------|------|-------------|
| `classification_id` | string | Unique identifier (AC-NNN) |
| `item_id` | string | ID of classified item (DOC-*, CR-*, PL-*) |
| `item_name` | string | Name of the item or category |
| `parent_category` | string | Higher-level category |
| `child_category` | string | Lower-level category (may equal item_name) |
| `classification_level` | int | Depth in hierarchy (1=root, 2=subcategory, 3=sub-sub) |
| `classifier` | string | Who made the classification |
| `classification_date` | date | When classification was made |
| `region_system` | string | Which classification system |
| `morphism_exists` | boolean | Whether inclusion morphism exists |
| `notes` | string | Additional context |

### Key Patterns

**Root categories** (level 1):
```python
roots = classifications[classifications['classification_level'] == 1]
# scholarly_works, field_records, creatures, places
```

**Item classifications** (items assigned to categories):
```python
items = classifications[classifications['item_id'].str.startswith(('DOC-', 'CR-', 'PL-'))]
```

**Multi-level paths** (transitive closure):
```python
# Stakdur: creatures → predators → apex_predators
# Path length = 2 morphisms composed
```

### Example Rows

| classification_id | item_name | parent_category | child_category | level |
|-------------------|-----------|-----------------|----------------|-------|
| AC-002 | Patterns of Passage | scholarly_works | philosophical_treatises | 2 |
| AC-006 | Stakdur | creatures | predators | 2 |
| AC-036 | Stakdur | predators | apex_predators | 3 |

---

## Dataset 3: regional_translations.csv

**Description:** Translations between classification systems—how terms and categories map across regions. Each row represents a component of a functor.

**Category Theory Interpretation:**
- A functor F: C → D maps objects to objects and morphisms to morphisms
- `preserves_structure=true` means F respects composition
- Inverse translations represent inverse functors (when they exist)
- Non-preserving translations are not valid functors

### Schema

| Column | Type | Description |
|--------|------|-------------|
| `translation_id` | string | Unique identifier (RT-NNN) |
| `source_system` | string | Origin classification system (source category) |
| `target_system` | string | Target classification system (target category) |
| `source_term` | string | Term in source system |
| `target_term` | string | Corresponding term in target system |
| `translation_type` | string | Type: category_mapping, terminology, measurement, etc. |
| `preserves_structure` | boolean | Whether translation preserves categorical structure |
| `translator` | string | Who established the translation |
| `translation_date` | date | When translation was established |
| `confidence` | string | high, medium, low |
| `notes` | string | Additional context |

### Key Patterns

**Structure-preserving translations** (valid functors):
```python
functors = translations[translations['preserves_structure'] == True]
```

**Archive exchange functor** (capital ↔ western):
```python
archive_functor = translations[
    (translations['source_system'] == 'capital_archive') &
    (translations['target_system'] == 'western_archive')
]
```

**Vold's terminology translations** (mathematical → natural language):
```python
vold_terms = translations[translations['translator'] == 'tessery_vold']
# morphism → passage, functor → preservation_map, etc.
```

**Non-functorial mappings** (preserves_structure=false):
```python
non_functors = translations[translations['preserves_structure'] == False]
# These break structure—useful for understanding what functors require
```

### Example Rows

| translation_id | source_system | target_system | source_term | target_term | preserves_structure |
|----------------|---------------|---------------|-------------|-------------|---------------------|
| RT-007 | capital_archive | western_archive | mathematical_treatises | formal_studies | true |
| RT-026 | mathematical_notation | natural_language | morphism | passage | true |
| RT-004 | capital_taxonomy | western_taxonomy | anomalous_entities | unclassified | false |

---

## Dataset 4: linguistic_containment.csv

**Description:** Linguistic containment relationships from Densworld texts. Each row represents a morphism in the language category where phrases contain subphrases.

**Category Theory Interpretation:**
- Objects = phrases/words
- Morphisms = containment (shorter phrase contained in longer)
- Pre-order structure (at most one containment between any pair)
- Probabilities decorate morphisms (enriched category)

### Schema

| Column | Type | Description |
|--------|------|-------------|
| `containment_id` | string | Unique identifier (LC-NNN) |
| `shorter_phrase` | string | The contained phrase (domain) |
| `longer_phrase` | string | The containing phrase (codomain) |
| `containment_type` | string | Type: prefix_context, compound_formation, modifier_prefix, etc. |
| `source_text` | string | Text where containment was observed |
| `location` | string | Archive or location of source |
| `observation_date` | date | When documented |
| `frequency_score` | float | How often this containment appears (0-1) |
| `context_probability` | float | P(longer_phrase | shorter_phrase) |
| `observer` | string | Who documented |
| `notes` | string | Additional context |

### Key Patterns

**Compound formation** (word + word → compound):
```python
compounds = linguistic[linguistic['containment_type'] == 'compound_formation']
# passage → passage diagram, stakdur → stakdur territory
```

**Modifier prefixes** (adding modifiers):
```python
modified = linguistic[linguistic['containment_type'] == 'modifier_prefix']
# stakdur → apex stakdur, morphism → identity morphism
```

**Definite article contexts**:
```python
definite = linguistic[linguistic['containment_type'] == 'prefix_context']
# stakdur → the stakdur
```

### Example Rows

| containment_id | shorter_phrase | longer_phrase | containment_type | context_probability |
|----------------|----------------|---------------|------------------|---------------------|
| LC-005 | passage | passage diagram | compound_formation | 0.88 |
| LC-001 | stakdur | the stakdur | prefix_context | 0.72 |
| LC-047 | theorem | probing theorem | modifier_prefix | 0.92 |

---

## Cross-Dataset Analysis

### Building the Passage Category

```python
# Objects: unique source and target locations
objects = set(passages['source_object']) | set(passages['target_object'])

# Morphisms: all passages
morphisms = passages[['passage_id', 'source_object', 'target_object', 'morphism_type']]

# Identity morphisms
identities = passages[passages['morphism_type'] == 'identity']

# Verify: every object has an identity?
objects_with_identity = set(identities['source_object'])
```

### Classification as Pre-Order

```python
# Build the partial order relation
edges = classifications[['parent_category', 'child_category']].drop_duplicates()

# Visualize with networkx
import networkx as nx
G = nx.DiGraph()
G.add_edges_from(edges.values)
```

### Verifying Functor Properties

```python
# For a functor F: capital_archive → western_archive
# Check: does it preserve composition?

capital_mappings = translations[translations['source_system'] == 'capital_archive']
# If A → B → C in capital maps to F(A) → F(B) → F(C) in western,
# then F preserves composition
```

---

## Narrative Context

### Tessery Vold's Key Insight

Vold observed that the Archive's classification system was itself a category:
- **Objects**: Categories and items
- **Morphisms**: "is contained in" relationships
- **Composition**: If A ⊆ B and B ⊆ C, then A ⊆ C
- **Identity**: Every category contains itself

This realization led to her Passage Diagrams—a visual representation of any categorical structure.

### The Probing Theorem (Year 892)

> "Tell me every creature that passes through the stakdur's territory, and I will tell you what a stakdur is—without ever seeing one."

In categorical terms: An object X is determined (up to isomorphism) by the functor Hom(-, X)—that is, by all morphisms into X.

### Connection to Language Models

The video source material (Tai-Danae Bradley) shows that language itself has categorical structure:
- **Objects**: Words or strings
- **Morphisms**: Substring inclusion (or contextual relationships)
- **Enrichment**: Probabilities decorating morphisms

Vold's "The Language of Dens" (Tutorial 8) applies this insight to Densworld texts.

---

## Living Ledger Events

The following events are seeded in the Living Ledger:

| Event ID | Date | Type | Description |
|----------|------|------|-------------|
| EV-880-004 | 880-04-15 | personnel_change | Vold appointed to Western Archive |
| EV-892-005 | 892-06-15 | theory_proposed | Probing Theorem first stated |
| EV-893-001 | 893-02-10 | manuscript_written | *Patterns of Passage* completed |
| EV-893-002 | 893-03-15 | archive_accession | Manuscript enters Archive (cascade) |
| EV-894-004 | 894-08-22 | theory_contested | Krell's objection |
| EV-895-007 | 895-03-15 | debate_published | Three-way debate |
| EV-897-001 | 897-09-20 | manuscript_written | *On the Coherence of Shifts* |
| EV-897-002 | 897-12-18 | archive_accession | Second manuscript enters Archive (cascade) |

Query in Living Ledger:
```bash
python3 tools/ledger.py query --actor tessery_vold --format summary
```

---

## Source Attribution

- **Primary Source:** Tai-Danae Bradley, "Category Theory and Language Models" (Cartesian Cafe video)
- **Densworld Integration:** COURSE_DESIGN_PROPOSAL.md
- **Scholar Design:** Tessery Vold created for this course series

---

*Reference Card Version 1.0*
*Created: December 2025*
