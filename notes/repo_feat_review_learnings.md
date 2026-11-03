# Repo feat review – method notes, improvements and learnings

How the per-book review works, and what each book taught us. Updated as the review goes on.

## Per-book routine (current)
0. **Load errors** – list the book's own LSTERROR/SEVERE messages first (they reveal legacy syntax and broken class/ability data outside the feats).
1. **Collect** the book's feats and `.MOD` lines; count placeholders and text prerequisites.
2. **Reference check** – every feat, ability, ability type, skill, skill type and race named in a prerequisite must exist in the repo (in the right category).
3. **First-level checks** – `PRELEVEL:MAX=1`, "1st level" in text or in BENEFIT/DESC, non-standard `FirstLevel` type, `LevelOneFeatOnly` feats that are not hidden.
4. **Text vs tags** – for text requirements that tags claim to cover: same kind of check (spell level vs class level) and same numbers.
5. **Rule review** – every feat against the book's rules, including feats with no prerequisites at all.
6. **Fix** – on top of the audit's verified conversions; repo forms only; old names kept as KEY when renaming.
7. **File check** – only prerequisite tags (plus intended TYPE/VISIBLE/BONUS changes) differ; references resolve.
8. **PCGen** – per-feat qualification tests on characters that should and should not qualify, original vs updated; per-prerequisite diagnostic when a result is unexpected; load messages compared.
9. **Deliver** a complete merged copy of each changed file, with repo paths.

## Learnings
- **Text audits miss what is not written.** Missing requirements with no text at all (Improved Familiar, Multiattack, Rapid Reload) only show up in a rule-by-rule review.
- **"Covered" is not "correct".** A tag can cover a text requirement with the wrong kind of check (Complete Mage: caster class level instead of spell level) or the wrong number.
- **Valid names can still never match.** A type can exist somewhere but not on the abilities meant ("WildShape" vs "Wild Shape"); `TYPE.Shield` is valid syntax but never matches a proficiency. Only a PCGen test per prerequisite reveals these.
- **PCGen is sometimes more forgiving than an exact-name check.** "Maneuverability (Good)" matched "Maneuverability(Good)" as a choice; a dead alternative next to a valid one changes nothing in play. Report such fixes as cosmetic.
- **Compound types work**: `TYPE.Desert Wind Maneuver.Strike` requires both types (verified with a strike vs a boost).
- **Wildcards do not** work in ability or class checks: `Smite%` in PREABILITY and `Ranger%=8` in PRECLASS never match (Champions of Valor, Champions of Ruin). They do work in PRERACE (`Orc%`), a documented feature.
- **First-level feats – the rule (confirmed by you; replaces my earlier convention):**
  - **Non-regional** feats available only at 1st level: `PREPCLEVEL:MAX=1` – the default, with the feat visible in the normal list. *Not* `LevelOneFeatOnly`.
  - **Regional** feats: `TYPE:Regional.LevelOneFeatOnly` (+ `VISIBLE:EXPORT`, chosen through "Select First Level Feat", + the one-regional-feat PREMULT) **and** `PREPCLEVEL:MAX=1`.
  - `PREPCLEVEL` counts only character class levels; `PRELEVEL` counts total levels including monster levels, so `PRELEVEL:MAX=1` is wrong for this; `PRELEVELMAX` is the legacy form.
  - Races of the Dragon / Races of Destiny additionally use the Universal Rules first-level counters (`FirstLevelFeatTaken`/`FirstLevelFeatAllowed`).
  - **Correction applied repo-wide (Oct 2026):** I had converted non-regional 1st-level feats to `LevelOneFeatOnly` + `VISIBLE:EXPORT` from the Expanded Psionics Handbook onward. Now: 57 non-regional feats → `PREPCLEVEL:MAX=1` (Kalamar 13, Ghostwalk 3, Eberron 3, Complete Arcane 2, Hidden Talent, Psiforged Body, Spellfire Wielder, Beauty's Bounty, Book of Erotic Fantasy 2, Monster Manual III 2, Ravenloft 2, Spellcasting Prodigy, Dragon Magazine Compendium 25); 90 regional feats gained `PREPCLEVEL:MAX=1` (Player's Guide to Faerûn 45, Races of Faerûn 28, Shining South 10, Unapproachable East 5, Dragon Magazine Compendium 2). Verified: non-regional feats offered at 1st level and refused at 3rd; a regional feat passes at 1st (hidden, first-level selection) and fails at 3rd.
- **Abilities keyed per class/race** (slippery mind, death attack, lay on hands, rock throwing, stability, energy vulnerability) have no shared type; a check must list the keys.
- **Malformed data**: missing tabs (garbled tags), missing parentheses, glued names ("Craft WandCraft Staff", "PsychicPsychic Healing"), counts in the wrong place (`PREABILITY:7,...,Intimidate` for "Intimidate 7 ranks"), wrong categories (`CATEGORY=ABILITY`; Stunning Fist checked as an ability).
- **Settings without regions** (Eberron, Kalamar, Ghostwalk): region requirements stay text, because nothing sets a region.
- **Self-referencing prerequisites**: a feat that requires itself (Champions of Ruin's Node Store) can never be taken – check every feat's prerequisites for its own name. (A *negative* self-reference, `!PREABILITY:...,<itself>`, is a legitimate "only once" pattern – PHB II's Weapon Supremacy.) A repo-wide scan found Node Store as the only real case.
- **Typos in alignment lists**: a repeated code silently drops another alignment (CE,NE,CE instead of LE,NE,CE) – compare against the sibling feats' patterns.
- **Bonus-embedded prerequisites** (`BONUS:VAR|...|PREABILITY:...|PRECLASS:...`) are valid; the reference checker must stop a key at `|`.
- **Mixed-case class types** (`PRECLASS:1,Spellcaster=7`) are accepted by PCGen – verified rather than "fixed".
- **Malformed bonuses can fail silently**: `BONUS:VAR|EssentiaPool|1 Special: ...` (rule text glued onto the value) gave no load error but added nothing (Magic of Incarnum's Azure Toughness, Midnight Dodge). Check bonus values for stray text.
- **Misspelled feat names break the feats that require them** (Lords of Madness: "Focused Antimatic", "Thickent Mucus"). When renaming with the old name kept as KEY, every reference must point at that KEY – PCGen matches prerequisites by key, not by display name.
- **Same name, different KEY is a deliberate variant, not a duplicate** (Empower/Quicken/Violate Spell-Like Ability: one version chooses an innate spell, the other a spell-like ability; Complete Mage's Metamagic School Focus: selector + effect; XPH Power Specialization `KEY:Fix`: alternative Weapon Focus form). The duplicate check now compares keys.
- **Correction:** the five Complete Champion feats I earlier called "defined twice" are cross-book copies (each once in Complete Champion and once in Champions of Valor); with both books loaded PCGen keeps one. Both copies are now tagged.
- **Bonuses to variables nothing reads are inert**: Dungeonscape's `TrailOfHazeUses` / `UmbralFistUses` are never defined or used by any ability, spell or output sheet, so a correct condition still changes nothing visible. Check that a bonus target is defined and read before counting a fix as effective.
- **Class progression variables answer rules questions**: Tome of Magic's `ShadowMysteryTierLVL` (1 apprentice, 2 initiate at 7th, 3 master at 13th) expresses "apprentice mysteries become supernatural" as `PREVARGTEQ:ShadowMysteryTierLVL,3` – resolved an open question from Dungeonscape.
- **"Living creature" must allow living constructs**: warforged are type Construct with subtype Living Construct – use `!PRERACE:1,RACETYPE=Undead` + `PREMULT:1,[!PRERACE:1,RACETYPE=Construct],[PRERACE:1,RACESUBTYPE=Living Construct]` (Heroes of Horror, Font of Life). Test both directions (warforged qualifies, an undead does not).
- **The converter misread feat names as regions** when a requirement was a bare capitalised name (Dreamcasting, Supernatural Ability) – check "region" proposals against the feat index.
- **Implausible values are evidence**: a prerequisite of Dex 5 (Wolfpack) is meaningless – with the text saying Dex 15, the tag is a typo.
- **A feat's own benefit can be evidence**: Eternal Strength adds 3rd-level cleric spells, which only a 5th-level cleric casts – confirming its text (cleric 5) over its tag (cleric 3).
- **Reprints in other books are evidence**: the same feat in another book (Evil Brand in the Book of Vile Darkness) can show a missing requirement – but only copy a requirement whose references exist without that book (an alignment yes; Cityscape's mystery abilities no).
- **Requirements can be enforced through a feat chain**: Champions of Ruin's knight feats lack the evil check themselves but require feats that have it.
- **Sibling feats are evidence for conflicts**: when a tag disagrees with its text, the same family of feats (Dragon Magic's four Dragonfire feats) can show which value is the typo – resolved Dragonfire Assault's Cha 13 → 11 without the book.
- **Check which path a fix actually changes**: Dragonfire Strike's broken "Sudden Strike" type only blocked ninjas – rogues and scouts already passed through the valid alternatives. Test every alternative of a "one of" check.
- **Class features tracked as variables** (sneak attack, sudden strike, skirmish dice) are more reliable than ability types for "has class feature X" checks.
- **Books can contain another book's feats**: Dungeonscape's file carries all 32 Cityscape feats; such copies drift apart (different prerequisites, same typos). Fix shared feats in both copies, and compare them – one copy may be evidence for the other.
- **A reference that exists only in another book makes a feat unobtainable when that book is not loaded** – Cityscape's mystery abilities do not exist in a Dungeonscape-only setup. Test each book on its own, with only its required books.
- **Invalid category `ABILITY`** appeared again (Magic of Eberron, Improved Homunculus) after Ghostwalk – the correct category is `Special Ability`.
- **One concept, several representations**: aquatic elves exist as a core Internal subrace, an Unearthed Arcana variant and a Forgotten Realms template – a check must cover all of them.
- **Type gaps in core class features ripple across books**: the blackguard's command undead lacked the shared `Rebuke Undead` ability (and its uses per day), silently excluding blackguards from 19 feats and 3 prestige classes. Fixed at the source in the DMG by mirroring the paladin's turn ability – one change instead of 19. Prefer source fixes for class features; test feats with each class that should qualify.
- **The SRD (d20srd.org) is an authoritative reference** for core classes and rules – use it to confirm class-feature behaviour before changing core data.
- **Partial race lists are not tagged**: when only some of the races in an "A or B" requirement exist in the repo (Underdark: chitine, slyth, Deep Imaskari missing), a race check would lock out the missing ones – keep the text.
- **Reprinted feats should match**: Underdark's node feats now use Champions of Ruin's form (`PRESPELLTYPE:1,ANY=1`).
- **Doubtful audit readings are reverted, not kept**: Fiendish Codex II's "devil" had been read as the Unearthed Arcana devil bloodline – when the meaning is uncertain, keep the text and ask.
- **Class features checked as feats**: "Rage" written as `CATEGORY=FEAT,Rage` (Unapproachable East, 6 feats) never matches – rage is a class feature (`TYPE.Rage`).
- **`PRELEVELMAX:1`** is accepted by PCGen and behaves like `PRELEVEL:MAX=1`; it is right on starting kits but suspicious on feats – and impossible next to a high-level requirement (Craft Contingent Spell: max level 1 plus spellcaster 11).
- **Commented-out lines** contain the same patterns – skip lines starting with `#` when fixing.
- **"[Not Implemented]" labels can be stale**: Unearthed Arcana's 17 weapon-group feats were fully implemented through internal abilities – verify the mechanics (here: actual weapon proficiencies before and after) before implementing anything.
- **Duplicate keys across books are resolved silently** (no load message): PCGen keeps one definition, depending on load order – Oriental Adventures' ancestor *Artist* vanished whenever the Player's Guide's regional *Artist* was loaded. Same-name *different* feats need distinct keys (`Ancestor ~ <Name>`); reprints of the *same* feat can share the key.
- **A literal "%" in DESC/BENEFIT must be written `%%`** (repo convention, 579 uses); a bare "%" is read as a parameter and logs "The % without a number in the description".
- **OCR scans need proofreading**: decorative headings were misread or scrambled, a table was spliced into a feat's text, and "50%" came out as "so%" – the page images settled each case.
- **Placeholder books** (Oriental Adventures, part of Kalamar, most of Unearthed Arcana): "[Not Implemented]" feats need the book text, not tag fixes.

## Errors in my own earlier audit (found during per-book review)
- **"1st level only" text converted to `PRELEVEL:MAX=1`**: the audit converter added this tag to 5 feats in delivered books – Eberron (Education, Adamantine Body, Mithral Body), Races of the Dragon (Dragon Tail, Dragonwrought) and Magic of Eberron (Psiforged Body – also not hidden and typed "Levelonefeatonly" in the original). PCGen confirms the harm: with that tag a 3rd-level warforged *fails* Adamantine Body's prerequisites. Corrected: Adamantine/Mithral Body already used the PHB convention (tag removed), Education converted to the PHB convention, Dragon Tail/Dragonwrought restored (they use the Universal Rules counters). Eberron re-delivered.
- **"A, B, or C" lists split at commas**: the audit converter split alternatives at their commas and turned the first item into a *required* check, leaving "...; or C" as text. Found in Magic of Incarnum (Indigo Strike, Share Soulmeld), Savage Species (Final Strike, already delivered – now corrected) Fiendish Codex II (Undo Resistance: "sneak attack, sudden strike, or skirmish" had become sneak attack required – confirmed against the original) and Magic of Eberron (Heroic Companion: "animal companion, familiar, special mount, or homunculus" had become familiar AND special mount – confirmed against the original line). A scan of the earlier repo-wide patch flagged 4 more in books still ahead: Heroic Companion (Magic of Eberron), Gnome Tunnel Acrobatics and Undermountain Tactics (Dungeonscape), Undo Resistance (Fiendish Codex II). **Correction (Dungeonscape):** the two Dungeonscape feats were *not* affected – the repo already tags them correctly as alternatives and their *original* text contains "; or". A leftover "or" is only an error when the audit added a required tag from the list – always compare with the original line. **The earlier repo-wide patch / Git branch contains these errors; the per-book files supersede it.** Routine: flag leftover text starting with "or" / containing "; or" and compare with the original wording.

## Modern syntax (legacy tokens)
- **`PRELEVELMAX:n` → `PREPCLEVEL:MAX=n`, not `PRELEVEL:MAX=n`.** PCGen's documentation: `PRELEVELMAX` and `PREPCLEVEL` count only character class levels; `PRELEVEL` counts *total* levels including monster (racial) levels. Verified: a gnoll fighter 1 (2 monster levels) passes `PRELEVELMAX:1` and `PREPCLEVEL:MAX=1` but fails `PRELEVEL:MAX=1` – a blind conversion would have locked gnolls out of their own Unapproachable East starting kits. All 63 uses (6 files: Races of Faerûn and Unapproachable East kits, Unapproachable East / Magic of Faerûn / Fey Feature / Book of Erotic Fantasy feats) converted; behaviour and load messages identical. Delivered in prepclevel_modernization.zip.
- **`PRESA` (legacy special-ability prerequisite) never matched** the repo's ability-based special abilities: Complete Arcane's Guardian Spirit refused even a wu jen with Watchful Spirit. Modern `PREABILITY:1,CATEGORY=Special Ability,Wu Jen ~ Watchful Spirit` works.
- **`PRERACETYPE` is current** – a class-file tag tying monster classes to races (all 90 uses are in class files), not a legacy prerequisite.
- **`BONUS:COMBAT|BAB` was removed from PCGen** ("unusual behavior around epic class levels") – the modern token is `BONUS:COMBAT|BASEAB`. The Book of Erotic Fantasy's 15 class BAB lines were rejected at load, so 17 prestige classes had **no base attack bonus at all** (Kundala 4: BAB 0 → 3). `BONUS:CHECKS` → `BONUS:SAVE`. Both legacy forms were used only in that book.
- **Class-name wildcards are not PCGen syntax**: `PRECLASS` has no `%` wildcard (documentation lists names, `TYPE.x`, `SPELLCASTER`, `ANY`). `Paladin%=4` / `Ranger%=4` / `Bard%=9` never matched – a paladin 4 and a ranger 4 failed. 73 such checks in 7 books (62 in Champions of Valor's Initiate feats) expanded to explicit lists: Paladin + Paladin of Freedom/Slaughter/Tyranny, Ranger + Planar/Urban Ranger, Bard + Bardic Sage (the Unearthed Arcana paladin variants have no `Paladin` type, so `TYPE.` would not cover them). Verified: paladin, ranger and Paladin of Freedom now pass. The different idioms `!PRECLASS:1,%=1` ("no class levels") and `PRERACE:1,%` ("any race") were left unchanged.
- **Undefined variables fail silently**: `TotalManifesterLVL` is never defined or set (always 0), so every check against it failed – The Mind's Eye's Drilbu and Complete Scoundrel's Psithief and Psychic Luck were unobtainable (missed in the Complete Scoundrel review because no check validated variable names). The repo's form is `Caster_Level_Highest__Psionic` (verified: 5 on a psion 5). A variable-name typo did the same in Lords of Madness (`TopazGuardialLVL` in the class vs `TopazGuardianLVL` in its equipment).
- **`PRECLASS:1,CASTERLEVEL=n` is not valid** (Dragon Magazine #338): a wizard 5 failed it; the PHB form is `PRECLASS:1,SPELLCASTER.Arcane=n,SPELLCASTER.Divine=n`. (`CASTERLEVEL=` inside `SPELLS:` tokens is a valid parameter.)
- **Follow-up for the routine**: a variable check needs PCGen's built-in and game-mode variables (`TL`, `CL`, `Caster_Level_…`, the `DisableSpell…` options, `ENCUMBERANCE`…) – a plain DEFINE/BONUS scan flags 635 names, mostly false alarms.
- **`PREVISION`** warns only for values without `=1`/`=ANY`; all repo uses already have them. `PREFEAT`, bare `PRELEVEL:n`/`PREHD:n` are not used.
- The routine now flags legacy tokens (`PRELEVELMAX`, `PRESA`, `PREFEAT`).
- **Correction:** I first reported that the 45 Player's Guide to Faerûn regional feats "have no level limit" – wrong: I had searched only for level *tags*. They (and all 83 regional feats in the repo) are 1st-level only via the `LevelOneFeatOnly` type. When checking for a rule, search for every mechanism that can express it (level tags, `LevelOneFeatOnly`, Universal Rules counters).
- **Regional feats are 1st level only** (rule confirmed) – see the first-level rule above.
- Data authors' comments can carry rule evidence (Unapproachable East: `PRELEVELMAX:1` marked 3.0 regional feats as 1st-level only).

## Full re-audit learnings (Oct 2026)
- **`PREMULT:N` (N ≥ 2) with a `PRESPELLTYPE` part can pass on the spell part alone**: PCGen counts spell-type matches, so a wizard with cantrips satisfied `PREMULT:2,[PRESPELLCAST:MEMORIZE=N],[PRESPELLTYPE:1,Arcane=0]`; wrapping the part in `[PREMULT:1,[…]]` does not help. When all parts are required, use separate top-level tokens (they are always ANDed). `PREMULT:1` (one of) is safe.
- **`%` in PRECLASS never matches** (not `Paladin%`, not a bare `%`): PRECLASS documents `ANY` for "any class"; PRERACE documents `%` as its wildcard and `PRERACE:1,%` for "any race". A negated non-matching check (`!PRECLASS:1,%=1`) is always true.
- **Same-name feats across books need a key check even when one book requires the other**: Dragon Magic's Draconic Knowledge always replaces the Draconomicon's.
- **Commented-out definitions do not exist**: `#Urdunnir Dwarf … KEY:Dwarf (Urdunnir)` – a grep finds the key, PCGen does not. Reference checks must skip `#` lines (the audit index does).
- **Race checks match keys, not display names**: "Fey'ri" never matches the race keyed `Planetouched (Tiefling Fey'ri)`; race wildcards (`Planetouched%`) work.
- **Variable names need checking like any other reference**: typos (`KiStrikeAdaman`) and undefined variables (`Heads`, `TotalManifesterLVL`) silently block feats – the audit now checks every PREVAR variable against DEFINE/BONUS:VAR in data and game mode, plus PCGen built-ins.
- **Tokens joined by a space** (`BONUS:SAVE|… BONUS:SAVE|…`) lose the second token silently – the audit flags embedded `PRE`/`BONUS` tokens.
- **Region rule scope**: the 1st-level rule for regional feats comes from the Forgotten Realms; Greyhawk regional feats (Dragon Magazine) are not 1st-level feats (5-rank prerequisites).
- **Tooling now lives in `review_tools/`** (audit.py, the Java harnesses, the test character template, `setup_test_env.sh`) so a workspace reset costs minutes.

## Dark Sun learnings
- **A missing ability granted with AUTOMATIC makes characters unloadable** ("Ability Reference … has not been resolved"): the gladiator class granted `Martial Weapon Proficiency Output`. A load test of one character per class catches this; the feat routine alone does not.
- **`!PREABILITY:1,CATEGORY=FEAT,TYPE=Regional` alone disqualifies the feat once taken** – always the self-exception form `PREMULT:1,[!PREABILITY…TYPE=Regional],[PREABILITY…<itself>]`.
- **Book requirements (`PRECAMPAIGN` in a PCC) are enforced by the Source tab**, not when a character file is loaded headless – verify them by checking the campaign's prerequisite list (`review_tools/CampReq.java`).
- **Regional feats are not 1st-level only outside the Forgotten Realms** (Greyhawk, Dark Sun – your decisions); the audit applies the FR rule to FR books only.
- **Shield proficiency checks use shield types** (`TYPE.Heavy`), never 3.0 names like "Large Shield".

## Spell conversion learnings
- **Moving tokens from a definition into a `.MOD` is not neutral**: a `.MOD` applies to whichever definition of the key survives (PCGen silently keeps one of several – the other's inline tokens are discarded, but its `.MOD`s are not); copies (`.COPY`) are made before `.MOD`s apply; and `CLASSES:.CLEARALL` depends on the order of `.MOD`s. Such spells keep their tokens inline.
- **PCGen keys are case-insensitive** ("Fins To Feet" in Savage Species is the same spell as Spell Compendium's "Fins to Feet").
- **A line with its own SOURCELONG no longer inherits the file's or PCC's source date** – per-line sources must include SOURCEDATE.
- **PCGen supports multi-line objects** (continuation lines start with a TAB; Kalamar's `kokc_spells.lst`) – line-based tools must join them first.
- **BahamutDragon declares class spell types as `FACT:SpellType|Arcane`**, not `SPELLTYPE` – a type derivation that only reads `SPELLTYPE` misses the core classes.
- **Preserve bytes**: some files contain Windows-1252 characters (invalid UTF-8); read and write with `errors='surrogateescape'`.
- **The best verification is PCGen's own model**: `review_tools/SpellDump.java` writes every spell's unparsed tokens (after all `.MOD`s) plus its class and domain levels; comparing original and converted dumps caught every one of the problems above, which a file-level check could not.
- Loading many books at once can crash PCGen's loader (an ability-choice null pointer, also with the original data) – test in smaller sets; the Book of Erotic Fantasy adds a 7th ability score (APP), which test characters must have.

## Spell Compendium rule and Magic of Eberron learnings
- **"Book X wins" without touching data lines**: load the other book's file twice in its PCC, `…|(EXCLUDE:keys)|PRECAMPAIGN:1,INCLUDES=X` and `…|!PRECAMPAIGN:1,INCLUDES=X` (Lords of Madness' existing pattern) – independent of load order, unchanged when X is not loaded.
- **`SpellDump`'s LEVELS only covers the test character's own classes**; the unparsed `CLASSES`/`DOMAINS` tokens hold the full assignment – compare those.
- **Two-column PDFs need column-aware extraction**: the default text order can attach one column's heading to the other column's body (Magic of Eberron: "Orb of Dancing Death" received the statistics of "Magic Weapon, Legion's"). PyMuPDF spans give position, direction and font: drop rotated text (side tabs) and caption fonts, find the gutter, read each column separately (`review_tools/pdf_columns_fitz.py`).
- **Cross-check an extraction against an independent list** (here the repo's raw text file: 45/45 spells) and the parsed values against the source (class levels 44/44 against the Level lines).
- **Overlapping archives must carry identical copies** of shared files – verified by unpacking in every order.

## Psionic power learnings
- **Count duplicates within one game system only**: a repo-wide scan also picked up the 3e and 5e PHBs (Aid, Alarm…) and inflated the keep-inline set from 898 to 1,622 – restrict to `35e` and `darksun_35e`.
- **Normalization rules need edge cases tested**: "min." → "minutes" first produced "1 minutes"; display components need "a, b, and c" and "; see text" forms.
- **New content can create new duplicates**: Magic of Eberron's Suppress Schism is also in Complete Psionic – check new keys against the repo before adding, as the spell structure depends on keys being unique.
- **Psionic powers use the spell file format**: disciplines as `SCHOOL`, display as `COMPS`, manifesting time as `CASTTIME`, power resistance as `SPELLRES`; power points have no token in the XPH.

## Maneuver learnings
- **Maneuvers, powers and spells share one key space** (all are SPELL objects): four Tome of Battle maneuvers had the same keys as spells in other books and were silently replaced – and the loser's class `.MOD`s merged into the winner. Different objects with the same name need distinct keys; check every key of a book against all other spell files (case-insensitively, per game system).
- **Renaming a key means updating every reference**, in every form: `SPELLKNOWN:CLASS|…|KEY` and `SPELLS:Innate|…|KEY,DC formula` – the DC suffix hid two references on the first pass; PCGen's "Unconstructed Reference" messages show any that are missed.
- **Use the campaign's exact CAMPAIGN/KEY in test characters**: "Tome of Battle: The Book of Nine Swords" – with a shortened name the book silently doesn't load and every test passes trivially. Check that the tested objects are actually present.

## 3e books learnings
- **Folder names differ between systems**: 3e uses `campaign_setting`, 3.5 `campaign_settings` – a wrong path silently yields "0 objects"; assert that compared folders exist.
- **A missing key is not a missing object**: 3.5 often renamed (deity tags dropped, wizards' names dropped, "Ghorus" vs "Ghorun") or restructured (FR races as subraces); compare with name normalization and across all books before porting.
- **A shared key is not a duplicate either**: compare the kind of object (the 3e guide's ring *armor* vs the DMG's base *Ring*, coral armor vs the gem). Loaded unconverted, the guide's armor replaced the DMG's magic-ring base item.
- **Respect existing precedence decisions**: Races of Faerûn already yields its flight/signal arrows to the guide – a generic "3.5 reprint wins" rule made both disappear.
- **"Book X wins" for several books**: move the duplicates into files loaded with `!PRECAMPAIGN:1,INCLUDES=A,INCLUDES=B` (none of them loaded); drop duplicates of always-loaded books.

## Equipment learnings
- **Derive a "standard order" with a topological sort**, not a greedy ranking: the PHB's lines were fully consistent (KEY before TYPE 116 times, never after), but a naive score made it look contradictory.
- **The reference's own gaps define what is not a gap**: the PHB gives ranged weapons no WIELD/SIZE, so only melee weapons without WIELD are real gaps.
- **A tool that crashes after writing its output still produced valid output** – check what failed before rerunning everything (the dump tool died on `Ability`, the last class, after writing all equipment).
- **Measure test coverage by keys**: 10 of 79 files weren't loaded by any of the first 8 sets; two more sets (incl. the plain 35e game mode for The Psychic's Handbook) covered every item.
- **Overlays must be self-contained**: selecting files by name ("equip") pulled a new book's PCC without its other files; give a new book its own overlay and check that the topic overlays' union equals the combined one.

## Special ability learnings
- **Check what the user sees, not only the data model**: the converted abilities were equivalent in PCGen's model, but the standard 3.5 sheets list special-ability objects only by SpecialQuality/SpecialAttack – without one of them they would have vanished from character sheets. A test export with the real standard sheet (not just any sheet) caught it.
- **A legacy token's display path can differ from its replacement's**: SAB texts are listed via SPECIALLIST/COUNT[SA]; ability objects via ABILITYALL…TYPE=… – know both before converting.
- **Keys built from data inherit its errors**: an owner key with an unbalanced "(" broke the line it was written into; commas and "TODO" texts needed handling too – the before/after model comparison found all three.
- **`pkill -f <pattern>` can match the running shell command itself** – stop processes by PID.
- **Special abilities / SAB (reverted, your decision)**: the SAB conversion was undone entirely – the core books contain no SAB, but rewriting 500+ texts across books changed more than it fixed. Keeping a verified reference commit (15e8d03) and baseline dumps made a byte-exact revert and a full proof (131,863 objects identical) straightforward.
- **Respect entity boundaries**: feats are not special abilities – a SAB on a feat is its benefit text or a per-character detail and stays on the feat (your decision). Convert by object kind, not by token.
- **New books stay out of upstream-fix overlays**: changes to a book delivered on its own (the compendium) go into its own archive, or the overlays stop agreeing.

## Object type learnings
- **Measure the numbers a player sees**: a two-line sheet printing BAB and base saves (`|ATTACK.MELEE.BASE|`, `|CHECK.WILL.BASE|`) turned a suspicious formula into a proven bug (19 Draconomicon prestige classes with BAB +0) and proved a case change harmless.
- **A token outside the reference isn't an error**: SR, DR, SPELLS, UDAM on classes are legitimate PCGen tokens for features the core classes lack – survey function, not token lists.
- **Exclude files nobody loads** from gap counts: two "race files" were raw book text (one commented out, one unreferenced) and inflated every race statistic.
- **Count, don't estimate**, before writing numbers into notes.

## Book-data learnings (Complete Champion)
- **Copy the working examples and the repo's own template**: three complete churches and a template block defined every convention (rank cost = difference of minimum scores, automatic criteria via membership grants, per-CR expansion).
- **Prove the mechanism end to end with one character**: membership → automatic criteria (score 8 as predicted) → repeatable criteria (+1 each) → rank with its benefit on the standard sheet.
- **Keys: never cut inside a parenthesis, and none at all for MULT abilities** – an unbalanced "(" aborted the whole data load; PCGen forbids parentheses in repeatable abilities' keys.
- **Test files are data too**: a character-file ABILITY line uses `KEY:` (not `KEY=`), repeatable selections need `APPLIEDTO:`; alignment lines need a game mode that defines the alignment channel (plain 35e in this test install).
- **Fill tables from data, not memory**: the deity column was wrong for two churches until taken from PREDEITY.

## Testing learnings
- **Test in one game mode (your decision): plain 35e.** In the test installation, characters with an alignment line
  load only in 35e (Bahamut35e fails on ALIGN there), so 35e covers classes with alignment requirements too.
- **The working environment can be reset** (Oct 2026): the repo clone, the PCGen install and all tools disappeared; the output folder survived. Rebuild recipe: PCGen 6.08.00RC10 release zip + `git clone` of bahamutdragon/pcgen, copy the repo's `system/` and `outputsheets/` over PCGen's, point `data` at a repo copy (hard-link copy for the updated install), character template with `VERSION:6.08.00` (the RC suffix is rejected) and `GAMEMODE:Bahamut35e`; ability visibility prints as "Yes".
- **A character without an alignment passes alignment prerequisites** in this setup (Champions of Ruin, Evil Brand) – so an alignment fix shows no qualification change; verify the parsed form instead.
- **Alignment cannot be evaluated in the headless test setup**: any `ALIGN:` line makes character loading fail, and the alignment channel cannot be set from code. Instead, verify alignment prerequisites by printing PCGen's **parsed** prerequisite (which alignments it contains). Found with Complete Divine's Spontaneous Healer (`!PREALIGN:CE,NE,CE` missing LE).
- The per-prerequisite diagnostic truncates long prerequisites – use the full-text variant when checking lists (alignments, long key lists).
- Load every book a campaign requires (`PRECAMPAIGN`); use the campaign **KEY** when one exists (e.g. "35e ~ Ghostwalk", "Libris Mortis").
- The core books need `data/_universal` (outside `data/35e`).
- Test characters need what a real character would have: a **subrace choice** (dwarf stability comes with "Dwarf ~ Hill"), an **alignment-based turn/rebuke choice** (clerics; paladins work instead), **Perform ranks** for bardic music features.
- Racial subtypes can come from another book: kobolds are dragonblood only with Races of the Dragon loaded – a race check then fails for every test character; use the diagnostic to check the other prerequisites.
- **Choice feats in prerequisites** (`Spell Focus (Divination)`) match only the named choice – verified (Divination passes, Evocation fails).
- Prerequisites and test characters use the **KEY**, which can differ from the display name (Weapons of Legacy: "Least Legacy (Infiltrator)" is keyed `Least Legacy ~ Infiltrator`) – a feat given by display name is silently dropped at load.
- Books can add ability scores (Book of Erotic Fantasy: Appearance) – test characters need one `STAT` line per score, or PCGen refuses to load them.
- Repeatable `CHOOSE:NOCHOICE` feats (Toughness pattern) also need an `APPLIEDTO:` entry in a test character file, or they are dropped at load.
- Innate spell-like abilities from feats are checked through the character's "Innate" spellbook (`hasSpellInSpellbook`), not `getCharacterSpellCount` – calibrated against a known working feat (Eyes of Light).
- Test characters must give **choice feats a choice** (`APPLIEDTO:`), or PCGen drops the feat at load (Elven Spell Lore, Node Spellcasting).
- My qualification tool lists only **visible** feats; hidden first-level feats need a direct prerequisite check.
- When killing background jobs, use exact process IDs (`pkill -f` can match its own command line).
- Spellcasting checks need the casting **ability score**: a sorcerer with Cha 10 cannot cast 1st-level spells, so "can cast 1st-level spells" fails – give casters a suitable stat.
- `set -e` scripts abort on `grep -c` returning 0 matches – later steps (copies!) silently do not run; verify the test install has the intended files.
- **The diagnostic's ability list does not show virtual feats**: a fighter showed only the internal "Shield Prof", yet passes `PREABILITY:...,Shield Proficiency` (the feat is granted virtually). I briefly concluded that feat-only shield checks refuse fighters – wrong; PHB II's Shield Specialization accepts a fighter 3. Always evaluate the prerequisite itself rather than inferring from the ability list.
- An apparent failure may be a level requirement the test character is too low for (Empower Supernatural Ability needs level 6) – read the failing prerequisite before concluding.
- An apparent failure may be a second requirement the test character lacks (Overhead Thrust needs Power Attack too) – check every prerequisite before concluding.

## Tool improvements made along the way
- Reference checker (Complete Warrior) → extended to `.MOD` lines and to **skill types** (Psychic's Handbook).
- Line fixer: add tags, trim the text to what remains (commas and semicolons), repo-style merge.
- File check: only prerequisite tags changed; references resolve.
- Text-vs-tags check (after Complete Mage).
- First-level checks in BENEFIT/DESC and for the `FirstLevel` type (after Kalamar and Ghostwalk).
- Per-prerequisite PCGen diagnostic (after Races of Stone); full-text variant for long prerequisites (Complete Divine).
- Reference checker: stops keys at `|` inside bonus-embedded prerequisites (Complete Divine).
- Re-ran the extended checker on all finished books (skill types): no new problems.
- Leftover-"or" check (mis-split alternatives) on delivered files and the earlier patch (Magic of Incarnum).
- First-level checks skip feats using the Universal Rules counters (Races of the Dragon, Races of Destiny).
- First-level check no longer flags "1st-level spells/powers" (Magic of Incarnum).
- Self-reference check in the routine, plus a repo-wide scan (Champions of Ruin).## Rules reference
- **d20srd.org** (the Hypertext d20 SRD, v3.5, with the SRD errata worked in) – recommended by the user as the reference
  for the basic 3.5 rules: class tables (base attack, saves, spells per day), core spell lists, skills, domains, feat
  prerequisites. The web tool only opens URLs from a search result or the user's message. Tested: the index page
  (https://www.d20srd.org/index.htm) opens, but its links are not exposed, and general searches ("monk class table")
  return mostly Pathfinder (pathfinder.d20srd.org) and 5e pages – check the edition of every hit. Most reliable: the
  user pastes the specific d20srd page URL; for rules already in the repo's PHB data, that data (verified) is the
  reference.


