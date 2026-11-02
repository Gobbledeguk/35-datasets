# Sovereign Press Dragonlance packs – review

Age of Mortals (2003) and Legends of the Twins (2007), from the Gobbledeguk/35-datasets repository
(`data/35e/sovereign_press/dragonlance/`). Tool: `review_tools/dl_packs_fix.py`, then the standard spell and equipment
converters.

## Before
The packs were written in generic PCGen syntax, not in this data set's conventions. Loaded in PCGen (35e mode, with the
core books, the Dragonlance Campaign Setting and Races of Ansalon) they produced **340 load messages**; in Bahamut35e
they did not appear at all.
- Every line of both class-feature files was ignored: the per-class categories ("Spellfilch Class Feature" …) were
  used but never defined, so no class granted any feature.
- Base saves `BONUS:SAVE|Fort` (no such check), `PREBAB` (no such token), `FAVCLASS:Any`, a deprecated `PREFEAT`,
  the proficiency "Bastard Sword", the spell "Tenser's Transformation" by name (the PHB keys it `Transformation`),
  two keys with a % sign, unescaped % in seven descriptions.

## Changed (following the Player's Handbook / DMG)
- PCCs: `GAMEMODE:35e|Bahamut35e`; require the 3.5 core and the Dragonlance Campaign Setting (as Races of Ansalon
  does); new `aom_abilitycategories.lst` / `lott_abilitycategories.lst` (15 class-feature categories in the PHB's
  form: views of Special Ability by type); year-only `SOURCEDATE` commented out – Bahamut35e needs year and month
  (add the month from the copyright page).
- Class features: `CATEGORY:Special Ability`, `TYPE:Class Feature.<Class> Class Feature.…` (PHB form).
- Classes: base attack in the PHB's form (standard progression plus the fractional-BAB variable for ¾ and ½
  progressions), base saves `BASE.Fortitude/Reflex/Will` with `classlevel("APPLIEDAS=NONEPIC")`, `PREBAB` →
  `PRETOTALAB` (Legion Scout, Rogue Knight, Knight of the Divine Hammer).
- Keys "War Mage ~ Armored Spellcasting -5%/-10%" → "… -5 Percent/-10 Percent" (names unchanged).
- `FAVCLASS:Any` → `HIGHESTLEVELCLASS`; `PREFEAT` → `PREABILITY`; `Sword (Bastard)`; `Transformation`; `%` → `%%`.
- Spells (47, none defined elsewhere): PHB structure (definitions, description `.MOD`s, `*_spells_class.lst`) and value
  forms; Second Life's "One day/level" → `(CASTERLEVEL) days`.
- Equipment: PHB token order; Belaying Pin `CRITRANGE:1` (its "x2" critical means 20/x2, as the club).

## Verified
- No load messages from either pack, in 35e and in Bahamut35e.
- A 3rd-level Mariner gets Sailor Lore, Seamanship and its bonus feat on the sheet.
- Spells: PCGen's model before/after the conversion – 753 spells, 0 unexpected differences.
- Equipment: 3,408 objects before/after – 0 differences.
- Feat audit: no findings.

## Needs the books
- Only 7 of 37 feats and traits have prerequisite tags, and none mentions a prerequisite in its text – the text was
  condensed from the book, so printed prerequisites may be missing. Checking needs the book (the PDFs have no text
  layer; page images can be read).
- Publication months for `SOURCEDATE`.
- The book's own contradictions listed in the packs' README stay as the pack author decided.
