# Magic of Incarnum – review (and ability categories across all books)

## Magic of Incarnum
Incarnum is implemented entirely as abilities: soulmelds are special abilities (89 base soulmelds; per class and
chakra an "Applied" entry – 107 Incarnate, 70 Soulborn, 124 Totemist), organized by per-class ability categories
(`moi_abilitycategories.lst`). The book's spells, feats, equipment and classes were covered by the earlier reviews.

Checked: loads without any message; every soulmeld category offers exactly its class's soulmelds; every class-feature
category holds that class's features; every soulmeld with chakra entries also has its Unbound entry.

Fixed:
- **Lost Emotion** (the *lost* template's one choice) offered nothing: the category selected type "Lost Emotion",
  the four emotions (Bile of Hatred, Fury of Wrath, Mirror of Despair, Song of Misery) are typed "LostEmotion".
  Category type corrected – it now offers the four emotions.
- **Dissolving Spittle**: the Incarnate's two entries were named "Disolving Spittle (Throat/Unbound)". Names
  corrected; keys unchanged so saved characters keep their choice.

## Ability categories in all books – empty selection lists (to decide)
A category is a view on a parent category (Special Ability, FEAT, Internal, …) selecting abilities by type. 812
categories were checked in PCGen across 11 book sets; 49 had no member in any set that loads them.

**1. Abilities exist, but in another parent category – fixed (your decision):** the category's parent now matches
where its abilities are; each now offers them (checked in PCGen):
- DMG: Hierophant Align (a true-neutral hierophant's one choice) – Special Ability → Internal: offers LG, LE, CG, CE.
- Draconomicon: Dragon Familiar Advancement – Special Ability → Internal: offers its 3 steps.
- Ghostwalk: Great Rune – FEAT → Special Ability: offers the 10 great runes.
- Ravenloft (Player's Handbook): Studied Foe – Internal → Special Ability: offers 11 foe types.
- Book of Vile Darkness: Thrall of Orcus Bonus Feat – Special Ability → FEAT: offers the 2 Vile Deformity feats.

**Complete Champion church ranks (11) – completed from the book:** see `COMPLETE_CHAMPION_NOTES.md`.

**2. Abilities exist only in an unloaded file (10):** `the_mess.lst` (core folder) is not loaded by any PCC, so these
selections are empty: Dragonkith Resistance, Hidecarved Immunity / Increased Resistance / Resistance, Talon of Tiamat
Immunity (Draconomicon), Skill Mastery, Vile Spellcasting Type, Ghost Ability; plus Martial Study Stone Dragon
Maneuver (Tome of Battle) and Sacrificed Eyestalk (Monsters of Faerûn) – to be examined individually.

**3. No ability has the type (23):** 14 are not used anywhere (harmless leftovers): Cerebremancer, Fist of Zuoken,
Psychic Warrior, Pyrokineticist and Thrallherd Class Feature, Dead or Forgotten Gods, Dragon Age, Grant Cleric Spells
To?, Immediate Magic Selection, JoWW / KotFH / Samurai Bonus Feat, Rival Org Bonus, VampireLevel. **9 are used** and
offer an empty choice (need data): Aasimar Race Trait (7 uses), Artificer Feat, Binder Feat, Fangshield Ranger Weapon
Focus, Hierophant Ability, Human Paragon Stat, Shaman Feat, Spellfire Hierophant Feat, Tiefling Resistance Boost.
