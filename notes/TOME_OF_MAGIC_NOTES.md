# Tome of Magic – review

## How the three systems are implemented
- **Shadow magic**: the 70 mysteries are spell objects (`Shadow Mystery ~ …`, type Shadow Magic, with school and
  subschool); characters receive them through path abilities (Apprentice/Initiate/Master path and Fundamentals
  categories – 24, 21, 18 and 9 entries).
- **Binding**: the 32 vestiges are spell objects (`Bind Vestige ~ …`, type Vestige) plus a Vestige ability category
  (32 entries) and Pact Augmentation (12).
- **Truenaming**: the utterances are **not implemented** – the truenamer's 9 class features exist, but no utterance
  does. Needs the book.

## Changed
- `tm_spells.lst` in the Player's Handbook's spell structure and value forms, like every other spell file:
  definitions, description `.MOD` lines (199), class levels in the new `tm_spells_class.lst` (the 2 entries with
  class levels), durations as formulas (41), the PCC loads the class file.
- Verified in PCGen (book set with Tome of Magic): the same 1,752 spell objects including all 102 mysteries and
  vestiges, 0 unexpected differences, identical load messages.

## Checked and in order
- Loads without messages; every Tome of Magic selection list is populated (vestiges 32, pact augmentations 12, the
  mystery paths, shadowcaster feats 46, every class's features).
- Mysteries and vestiges have no components or casting time in the data – expected (supernatural/spell-like, as for
  maneuvers); the converter's notes list them (`review_tools`).

## Needs the book
- Truenaming utterances (not implemented).
- The binder's bonus feat list: the "Binder Feat" selection is empty – the feats exist (Improved Binding, Skilled Pact
  Making, Practiced Binder, …) but none is marked as a binder bonus feat; which ones belong to the list needs the book.
- The 32 vestiges have an empty source page ("P.").
