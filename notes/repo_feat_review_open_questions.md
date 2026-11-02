# Repo feat review – open questions to confirm against the books

## Full re-audit (Oct 2026) – status and remaining decisions
All 69 delivered files plus the 33 Dragon Magazine Compendium files were re-audited with `review_tools/audit.py` (every check from the learnings). Fixed in this pass: Epic Level Handbook variable typos (`KiStrikeAdaman`, `DefensiveStance`, `EWildshape` – 7 epic feats were unobtainable); Lords of Madness classes (3 save bonuses joined by a space); Kalamar unescaped "%"; Savage Species Multivoice (undefined `Heads`); Races of Destiny Menacing Demeanor (commented-out key removed); Heroes of Horror Blood Calls To Blood (broken type from my earlier audit); race keys in Races of Faerûn / Player's Guide (Fey'ri, Kir-lanan, Planetouched); `PREMULT` + `PRESPELLTYPE` overcount (Ascetic Mage, Lyric Spell, Accelerate Metamagic, Blood Calls To Blood, Prophecy's Shaper, Arcane Strike, Epic Manifestation, Alternative Source Spell); Dragon Magazine Compendium (Mind Daggers, Vathrin Stigmata, first-level rule on Bronze Solaris Member, Noble Born, Troll Blooded). Remaining audit findings (45) are all listed below.

**Decisions needed**
- **Greyhawk regional feats** (Dragon Magazine Compendium) – **resolved** (your decision): not restricted to 1st level; left without `LevelOneFeatOnly`/`PREPCLEVEL`.
- **Epic Spellcasting** – **accepted as is** (your decision): the PREMULT overcount remains documented; 9th-level casters below character level 21 could take it before having 24 ranks.
- **Draconic Knowledge – two different feats share this key.** Dragon Magic's version (the text you quoted) is fully implemented: `BONUS:SKILL|TYPE=Knowledge|DraconicFeats` with the Draconic Feat Tracker counting `TYPE=Draconic` feats, plus `CSKILL:TYPE=Knowledge` – verified: Knowledge (arcana) +2 with two draconic feats. The Draconomicon's version is a different feat (dragons' bardic-knowledge-like ability) – and because Dragon Magic requires the Draconomicon, PCGen always keeps only Dragon Magic's version, so the Draconomicon feat silently never exists. **Open**: give the Draconomicon version its own key (e.g. `KEY:Monstrous ~ Draconic Knowledge`, like the Oriental Adventures ancestor feats), and its broken prerequisite `PRESKILL:3,TYPE=Knowledge` (no rank count – never satisfied) still needs the Draconomicon's text.
- **`%` idioms** – **resolved** (your decision): `!PRECLASS:1,%=1` → `!PRECLASS:1,ANY=1` (PCGen documents `ANY`, not `%`, for PRECLASS) in Races of the Wild (Centaur class) and Unearthed Arcana (4 generic classes). The `%` form never matched, so "no class levels" was always true: a fighter could take GC_Warrior and a centaur fighter the Centaur monster class – both now refused, class-less characters still qualify (verified). `PRERACE:1,%` stays: it *is* PCGen's documented "any race" form.

**Data gaps found by the reference check (no change possible without new data)**
- Races not defined or commented out: Urdunnir (Stoneblood, Stonewalker Fist – unobtainable), Lesser Aasimar and Lesser Tiefling (commented out), Deep Imaskari, Slyth, Chitine (Player's Guide regional feats – alternatives only), whisper gnome (Races of Stone: Extra Silence, Silencing Strike – unobtainable), Extaminaar.
- Deities not defined: Varae (Initiate of Varae – unobtainable), Vathris (Dragon Magazine Compendium – now text).
- Subtypes never set: Gully (Dragonlance Cornered Rat – unobtainable), Dragonmarked (Eberron Aberrant Dragonmark – negative check, harmless), Acid/Electricity (Savage Species Final Strike – alternatives).


Items the repo data cannot settle on its own (no prerequisite text, or text that conflicts with the tags).
Nothing listed here has been changed; each needs a check against the printed book.

## Core rule books
- **Monster Manual – Multiattack**: "three or more natural weapons" has no tag; the repo models no natural-weapon count.
- **Monster Manual – Improved Natural Attack**: its check `PREWEAPONPROF:1,TYPE.Natural` is satisfied by a human's unarmed strike (found while reviewing Eberron), so it does not really require a natural weapon.

## Player's Handbook II
- Battle Dancer, Indomitable Soul, Spectral Skirmisher, Defensive Sweep: exact printed prerequisites (numbers) not verified.

## Complete Warrior
- Defines its own "Improved Familiar" next to the DMG's (possible duplicate key).

## Expanded Psionics Handbook
- Hidden Talent: does the printed feat also require that the character is *not already psionic*? (A psion can currently take it.)

## Eberron Campaign Setting
- Dragon Totem / Dragon Rage: "region of origin Argonnessen or Seren" kept as text (Eberron data uses no regions).

## Races of Faerûn
- Song of Fury, Primitive Caster: no prerequisites in the repo and none in their text.
- Shield Dwarf Warder: "Dwarf (Shield)" kept as text (the shield-dwarf subrace exists only commented out).

## Player's Guide to Faerûn
- Shadow Weave Magic: repo has Wis 15 (recalled as Wis 13 or Shar as patron).
- Inscribe Rune: repo has divine caster level 5 and Int 13.
- Portal Master: repo has only Craft Wondrous Item.

## Complete Adventurer
- **Deft Strike**: stat conflict – text says Int 13, tag says `PRESTAT:1,INT=15`. Unchanged; no repo evidence either way (unlike Wolfpack and Dragonfire Assault). Which is printed?

## Complete Arcane
- Battle Caster: "ignore arcane spell failure from armor" kept as text (the only variable covers warmage only).

## Races of Stone
- Craft Rune Circle: "caster level 5th" tagged as 3rd-level spells (slightly strict for sorcerers).

## Ghostwalk
- About 20 ghost feats (Ectoplasm, Ghost Hand, Corrupting Touch, Control Visage, …) have no prerequisites: are they restricted to ghosts in the book?

## Libris Mortis
- Fell Animate, Fell Drain, Fell Frighten, Fell Weaken: no prerequisites (possibly "any other metamagic feat").
- Graft Flesh (Beholder), Graft Flesh (Undead): unlike the other Graft Flesh feats, no creature requirement.
- Corpsecrafter, Enduring Life, Necromantic Presence, Unquenchable Flame of Life: no prerequisites.

## Complete Scoundrel
- Third Times the Charm (renamed from "Thid Times the Charm"): tags require a luck feat and character level 3; its text adds "Access to the Luck domain". Is the domain an additional requirement or an alternative to the luck feat?
- Chant of the Long Road: rebuilt from a garbled tag as "bardic music + Perform 6 ranks"; confirm the rank count.

## Champions of Ruin
- Snatch Trophy, Node Sensitive, Entangling Spell, Lingering Spell: no prerequisites in the repo (and none in their text). (Evil Brand and Poison Immunity: see Resolved.)

## Complete Champion
- The 19 Devotion feats (Air, Animal, Chaos, Death, Destruction, Earth, Evil, Fire, Good, Healing, Law, Luck, Magic, Plant, Protection, Strength, Sun, Travel, Trickery, War, Water – except Knowledge Devotion) have no prerequisites; their benefits refer to "your deity". Do they require a patron deity (or access to the domain)?

## Dungeonscape
- **Dungeonscape's feat file contains all 32 Cityscape feats** (only 11 of its 43 feats are Dungeonscape's own), and the two copies have drifted: Cityscape's Favored Mystery feats require the mystery (`PREABILITY ... <mystery>`, an ability defined only in Cityscape's ci_abilities.lst), Dungeonscape's have no prerequisite. Adding Cityscape's check to Dungeonscape was tried and **reverted** – without Cityscape loaded the ability does not exist and the feats become unobtainable. Question: should Dungeonscape carry Cityscape's feats at all, and if so with `PRESPELL:1,<mystery>` (the mysteries are spells in du_spells.lst)?
- ~~Favored Mystery (Trail of Haze, Umbral Fist): bonus condition "Apprentice mysteries supernatural"~~ – **resolved** (Tome of Magic review): now `PREVARGTEQ:ShadowMysteryTierLVL,3` (master tier, 13th level). Remaining: the counters `TrailOfHazeUses` / `UmbralFistUses` are never defined or read by anything, so the extra use is still not shown anywhere. Cityscape has the same two feats (to fix there).

## Lords of Madness
- Craft Aboleth Glyph (caster level 5), Grell Alchemy (caster level 1): kept as text – aboleth and grell characters cast through racial abilities, so a class-level check would lock them out.
- Craft Psionic Seal: "Psionic Ability" kept as text next to the new caster/manifester level check – what exactly does it require?
- Bane of the Unclean: "True Beholder or Favored Enemy (Aberration)"; Disintegration Finesse: "cast disintegrate or use it as a spell-like ability" – kept as text.

## Tome of Magic
- Sudden Ability Focus: "Special attack" kept as text (no common type for monster special attacks).

## Races of the Dragon
- Dragon Wings: its alternative path ("Dragonwrought and fewer than two feats", `!PREABILITY:2,CATEGORY=FEAT,%`) relies on the `%` wildcard, which PCGen does not evaluate. What exactly does the book allow for kobolds with Dragonwrought?

## Resolved
- **Dragonfire Assault (Dragon Magic)** – stat conflict from the sanity check (tag Cha 13 vs text Cha 11): **resolved** to Cha 11. Evidence: the feat's own text and all three sibling Dragonfire feats (Channeling, Inspiration, Strike) use Cha 11 in both text and tag.
- **Blackguard rebuke undead (DMG)** – **resolved at the source** (your decision; confirmed upstream in BahamutDragon master d353e9b and by the SRD: the blackguard "command[s] and rebuke[s] undead … as would a cleric of two levels lower"). `Blackguard ~ Command Undead` now grants the `Rebuke Undead` ability, 3+Cha uses per day, the Cha turning check and the Extra/Improved Turning flags, like the paladin's turn ability. Before, blackguards had no rebuke uses at all and were refused by 19 feats (and 3 prestige classes) checking rebuke undead. Delivered in core_feat_fixes.zip (dmg_abilities.lst).
- **Evil Brand (Champions of Ruin)** – had no prerequisite: **resolved** – the same vile feat in the Book of Vile Darkness requires an evil alignment (as all vile feats do); added `PREALIGN:LE,NE,CE`. Champions of Ruin's other vile feats lacking the check (Demonsworn/Hellbound/Tormented Knight, Evil Embraced) already require an evil-checked feat, so evil is enforced through their chains.
- **Poison Immunity (Champions of Ruin)** – no prerequisite: **resolved as correct** – the Book of Vile Darkness copy has none either.
- **Oriental Adventures placeholders** – **resolved** with the book text you provided (3.0 printing, adapted to the repo's 3.5 terms): the 73 stubs in `oa_abilities.lst` (the separate oa_abilities_feat.lst is empty upstream) are now 71 implemented feats – 44 ancestor feats (`TYPE:Ancestor`, `PREPCLEVEL:MAX=1` – "character creation" only – plus a one-ancestor check; clan in the description; unconditional bonuses tagged), 19 general, 2 item creation, 6 martial-arts masteries; the Improved Grapple stub (PHB 3.5 version applies) and a duplicate Prone Attack stub removed. Great Throw's benefit from your text; Great Stamina's +2 stays text, its +1 hp is a flat bonus (verified 11 → 12). Names shared with other books: Complete Warrior's 3.5 reprints keep the same key (Complete Warrior's version wins when loaded); different feats with the same name (9 Player's Guide regional feats, Cool Head, Sea Legs) use `KEY:Ancestor ~ <Name>` so both coexist.
- **Unearthed Arcana placeholders** – **resolved** with the book text you provided: the 17 Weapon Group feats were already fully implemented (internal group abilities grant every weapon the book lists, including the exotic and exotic-double parts and the Arms and Equipment Guide / Complete Warrior support files) – only their "[Not Implemented]" labels were stale; verified a character's proficiencies are identical before and after. The 17 spelltouched feats now carry their mechanics where PCGen can model them (Bladeproof Skin DR 3/bludgeoning and −2 armor check; Breadth of Knowledge +1 per Knowledge skill with ranks; Momentary Alteration alter self 1/day, repeatable; Photosynthetic Skin as a daylight toggle; save DCs for Conductivity, Live My Nightmare, Stench of the Dead); the "exposure to a spell" prerequisites stay text (story condition).
- **Wolfpack (Races of the Wild)** – stat conflict from the sanity check (tag Dex 5 vs text Dex 15): **resolved** to Dex 15. Evidence: the feat's own text; a Dex 5 prerequisite would be meaningless. PCGen: a Dex 12 fighter qualified before, is refused now.
- **Weapons of Legacy tiers** – **resolved** (your decision): Lesser Legacy (X) requires Least Legacy (X), Greater Legacy (X) requires Lesser Legacy (X) – 7 links for the 4 items, plus the authoring template. Verified in PCGen.
- **Eternal Strength (Races of Destiny)** – tag cleric level 3 vs text cleric level 5: **resolved** to 5. Evidence: the feat adds 3rd-level spells (heroism) to the cleric list, which clerics cast from 5th level; the 3 was apparently copied from the Initiate feats.
- **Favored Mystery – "apprentice mysteries supernatural" (Dungeonscape)**: resolved via Tome of Magic's `ShadowMysteryTierLVL` (see Dungeonscape).

## Races of Destiny
- Diverse Background: "Half-human" kept as text (no common race type for half-human races).
- Able Learner: "Human or doppelganger" kept as text alongside its first-level counters.

## Races of the Wild
- Aerial Reflexes, Aerial Superiority, Diving Charge: no prerequisites and no text – do they require a fly speed (`PREMOVE:1,Fly=1`)?
- Elf Dilettante (+1 on untrained skill checks) and Born Flyer (bonuses while flying): conditional bonuses kept as text.

## Complete Book of Eldritch Might (Malhavoc Press)
- Reviewed: no broken references, no text prerequisites, nothing changed.
- Aid Spellcasting: tags require Cha 15 **and** Int 15 (two separate PRESTAT). Is it "and" or "or" in the book?
- Lace Spell: Spellripper (Cha 21 and Int 17) and Lace Spell: Unravel (Cha 15 and Int 17): confirm both stats are required.
- Good Memory, Magical Talent, Precise Touch, Subtle Scrying: no prerequisites in the repo.

## Heroes of Horror
- Improved Oneiromancy requires **Dreamcasting**, a feat that does not exist in the repo – the requirement stays text (missing feat to implement?).
- Taint and depravity ("mild taint", "mild depravity": Corrupt Arcana, Lunatic Insight, Mad Faith, Surge of Malevolence) kept as text: depravity is not tracked; `TaintScore` exists but "mild" is a threshold relative to Con/Wis.
- Blood Calls to Blood ("descended from a fiend"), Touch of Taint (natural attack dealing ability damage/drain or energy drain), Spirit Sense (near-death experience): kept as text.

## Magic of Eberron
- Heroic Companion: "or homunculus" cannot be checked (no "has a homunculus" ability) – an artificer whose only companion is a homunculus is not covered by the new one-of check.
- Deathless Fleshgrafter: "Aereni elf" kept as text (Aereni are not modelled as a subrace).

## Unapproachable East
- Battle Jump, Draw from the Land, Long Reach, Vremyonni Training, Woodwise: 1st-level limit (now `PREPCLEVEL:MAX=1`, converted from the legacy `PRELEVELMAX:1` – behaviour unchanged). The data author's comments show `PRELEVELMAX:1` marked **regional** feats as 1st-level only. **Rule (confirmed by you): regional feats are 1st level only** – all 83 regional feats in the repo (Player's Guide to Faerûn 45, Races of Faerûn 28, Shining South 10) already follow it via `Regional.LevelOneFeatOnly` + `VISIBLE:EXPORT`, plus the "one regional feat" check. These five are typed General with no region check. **Now converted to the regional convention** (`Regional.LevelOneFeatOnly` + `VISIBLE:EXPORT` + one-regional-feat check + `PREPCLEVEL:MAX=1`). Still open: their **regions** (no region check yet). Evidence for Woodwise: Shining South reprints it as a regional feat for elves of Misty Vale, Sildeyuir and the **Forest of Lethyr** (an Unapproachable East region) – same feat, slightly different wording; Unapproachable East may list its own regions.
- The berserker-lodge memberships stay text.

## Book of Vile Darkness
- Reviewed: every vile feat requires an evil alignment; references clean; nothing changed. Its Evil Brand and Poison Immunity resolved the Champions of Ruin questions.
- Boost Spell-Like Ability, Mortalbane, Poison Immunity: no prerequisites in the repo.

## Fiendish Codex II
- Brand of the Nine Hells: "devil" kept as text – the earlier audit had turned it into the Unearthed Arcana devil *bloodline* (reverted as a doubtful reading). Does it mean being a devil (baatezu), devil-blooded, or sworn to an archdevil?
- The Mark of ... feats: "allegiance to <archdevil>" kept as text; Devil's Favor: "pact with devil" kept as text.

## Underdark (Forgotten Realms)
- Race requirements kept as text because some of the races do not exist in the repo: Portal Sensitive (Deep Imaskar or gloaming), Stone Soul (Deep Imaskar or slyth), Tunnelrunner (chitine or grimlock), Wisdom Breeds Caution (slyth or svirfneblin). Missing races: Deep Imaskari, slyth, chitine (svirfneblin exists only as a gnome subrace).
- Caver: +2 Heal and Survival "in the Underdark" – situational, kept as text. Improved Levitation ("levitate as a spell-like ability") and Exotic Armor Proficiency (matching armor proficiency) kept as text.

## Stormwrack
- Water Adaptation: "aquatic half-elf" kept as text (no clear representation of half-aquatic elves).
- Landwalker now accepts the three aquatic-elf forms in the repo (core subrace, Unearthed Arcana variant, Forgotten Realms template).

## Book of Erotic Fantasy (Valar Project)
- Fixed beyond the feats: legacy `BONUS:COMBAT|BAB` (15 lines, 17 prestige classes had no BAB), `BONUS:CHECKS` (2 equipment modifiers), a non-existent ability category (Imagist's Inspired Smite Evil was never granted). The book now loads without errors (67 → 16 load messages, none from this book).
- Sexually Open Society / Sexually Private Society: opposite home-society background feats with no mutual exclusion – should they exclude each other?
- The book is marked `STATUS:ALPHA`; its classes still use the legacy `SAB:` tag for some class features (e.g. Inspired Smite Evil uses) – not flagged by PCGen, left unchanged.

## Weapons of Legacy
- Reviewed: no feat changes needed. Legacy rituals stay text (story conditions); the compound type check of Empower/Quicken Legacy works (8 legacy abilities are both spell-like and command-activated); the "(LegacyItemName)" template feats are not loaded by the PCC.
- Load error: an ability offers a choice of **legacy shields** (`TYPE=Legacy.Shield`), but the book defines none – data gap.

## Shining South
- Reviewed: no changes needed beyond the first-level rule (its 10 regional feats now carry `PREPCLEVEL:MAX=1`); loads without errors; references clean. Tribe memberships stay text. Its Woodwise is evidence for Unapproachable East's Woodwise regions (see there).

## Repo-wide idioms left unchanged
- `!PRECLASS:1,%=1` (no class levels: Races of the Wild, Unearthed Arcana classes) and `PRERACE:1,%` (any race: DMG) – not class-name wildcards; PCGen's documented form for "any class" is `ANY`. Convert to `!PRECLASS:1,ANY=1`?

## Heroes of Battle
- Guerrilla Scout / Guerrilla Warrior: "Listen and Spot (Hide and Move Silently) ranks cost 1 skill point even if cross-class" kept as text (no simple tag); Guerrilla Warrior's armor check reduction applies only in light/medium armor – text.

## Dragonlance
- **Orphaned data**: `campaign_settings/dragonlance/_feats.lst` (56 feats – Races of Ansalon/Krynn material such as Improvise Weapon, Gnome's Luck, Mad Genius, Woodshaper) is **not loaded by any book** (Races of Ansalon's feat line is commented out). Should it be wired into a PCC (and then reviewed)?
- Reserves of Strength: text "spellcaster level 1", tag allows only **arcane** casters (`PRESPELLTYPE:1,Arcane=1`). Arcane only, or any spellcaster?
- Honor-Bound: no prerequisites (its benefit is lost if you break your word until you atone) – alignment or code requirement?
- Improved Resist Dragonfear / Resist Dragonfear: "must have taken damage from / encountered a dragon" – story conditions, text.

## Dragon Magazine #311 (Paizo)
- Reviewed: no feat changes needed (ceremonial feats require spellcasting; each spell-template feat requires its ceremonial feat; the .MODs only add descriptions). Loads without errors.
- Its PCC (`dm311.pcc`) has no `PRECAMPAIGN` line, unlike every other book (`PRECAMPAIGN:1,INCLUDESBOOKTYPE=Core35e`) – add it? (Same for Green Ronin's Advanced Player's Manual.)

## Ravenloft Player's Handbook (Sword & Sorcery)
- Reviewed: feats fine (Redhead and Reincarnated already carry `PREPCLEVEL:MAX=1` from the first-level work; delivered in rlphb_feat_fixes.zip). Story conditions (energy drain, brush with death, a death close to you…) stay text; Courage, Jaded, Open Mind, Voice of Wrath have no prerequisites.
- **Load error – missing domain**: four deities (Ra, Set, Ezra, the Lawgiver) grant a **Curse** domain that the book does not define (rph_domains.lst has only Mist and Repose RL); the only "Curse" domain in the repo is Green Ronin's Book of Fiends. Add a Ravenloft Curse domain?

## Advanced Player's Manual (Green Ronin)
- Reviewed: no changes needed – every feat's tags match its text exactly; the choice-dependent check `Spell Focus (Divination)` works (Divination passes, Evocation fails); loads without errors. Its PCC has no `PRECAMPAIGN` line (see Dragon Magazine #311).
- Armored Caster: no prerequisites in the repo (and no text).

## Last 13 small books (batch)
- Fixed: The Mind's Eye (Drilbu, Powergrace, Psychic Sight + Crystal Master class), Complete Scoundrel (Psithief, Psychic Luck – re-delivered), Dragon Magazine #338 (5 staff feats), City of Splendors: Waterdeep (Jester's Magic ×2), Magic of Faerûn (Attune Gem), Dungeon Master's Guide II (Apprentice), Lords of Madness (Topaz Guardian variable – re-delivered).
- No changes needed: Fey Feature and Monster Manual III (first-level work already delivered), Frostburn, Sandstorm, Monster Manual II, Secrets of Sarlona, Lost Empires of Faerûn, Fantasy Firearms.
- Dungeon Master's Guide II: Mentor carries the inert `FirstLevel` type but is not a 1st-level feat (requires a completed apprenticeship) – remove the type? Business Savvy's profit-check bonus and guild memberships stay text.
- Class prerequisites on undefined variables (outside the feats): Complete Psionic prestige class `PREVARGTEQ:PsionicPowerPoint,1`; Book of Exalted Deeds prestige class `PREVARGTEQ:SneakAttackQualify,3` – both always fail.
- Frostburn modifies a "Harpoon" weapon not defined in its required books (only core) – the .MOD is skipped unless Stormwrack is loaded.
- Secrets of Sarlona's PCC has no `PRECAMPAIGN` line either (see Dragon Magazine #311).

## Unearthed Arcana (weapon-group variant, beyond the feats)
- Not implemented, all optional parts of the variant: replacing class weapon proficiencies by weapon groups (the class table), adding Weapon Group (any) to the fighter's bonus feats, and the racial rules (dwarves with Axes also get dwarven waraxe and urgrosh; elves automatically get Bows and Heavy or Light Blades; gnomes with Picks and Hammers get the gnome hooked hammer). Implement them?
- Breadth of Knowledge: "all Knowledge checks are treated as trained" stays text (PCGen cannot change a skill's untrained rule from a feat).

## Oriental Adventures
- Martial-arts masteries: the book says a character who masters a style *gains* its mastery ability – implemented as feats with the style's prerequisites. Should they be granted automatically (no feat slot)?
- Pain Touch: Table 4-2 shows Wis 19+, the feat text Wis 15+ – implemented Wis 15.
- Keen Intellect (already implemented in the repo) differs from the 3.0 printing (repo: Int instead of Wis for some checks and Will saves; book: +1 Int checks, +1 Knowledge/Scry/Search) – presumably the official 3.5 update; left unchanged.
- Situational benefits kept as text: Fearsome and Fearless, Powerful Voice, Resist Poison/Taint, Soul of Loyalty, Strength of the Crab, Warrior Shugenja's Concentration bonus, Great Stamina's +2.

## Dark Sun 3.5 (data/darksun_35e – Campaign Setting, Terrors of Athas)
- Reviewed with the full routine (game mode 35e). Fixed (ds_feat_fixes.zip): the 15 regional feats' one-regional check (`!PREABILITY…TYPE=Regional` alone disqualified the feat once taken – now the self-exception form; verified: a fighter with Freedom still qualifies for Freedom, not for Companion); Gladiatorial Entertainer (ability key `Gladiator ~ Gladiatorial Performance`); Psionic Mimicry ("Knowedge"); Sickening Raze (prerequisite "Agonizing Radius" split into the description); Shield Wall ("Large Shield" → `PREPROFWITHSHIELD:1,TYPE.Heavy`); Agonizing Radius typed Defiler (was missing from the Defiler Feat category); **Gladiator and Templar Knight proficiencies** (`Martial Weapon Proficiency Output` does not exist – every gladiator character failed to load; now the fighter's `ABILITY:Internal|AUTOMATIC|TYPE=WeaponProfMartial`); `VIIBLE`, Feylaar `ARMS:4` → `HANDS:4`. Load messages 61 → 58, none new.
- Dark Sun regional feats – **resolved** (your decision): not 1st-level only; the self-exception fix stays, no level tags. The audit's regional 1st-level rule now applies to Forgotten Realms books only.
- Path Sinister – **resolved** (your decision): prerequisite text now "only by defilers".
- Arena Clamor / Brutal Attack – **confirmed** (your decision): identical prerequisites are correct.
- "Defiler", "preserver" and "cultural background" (city-state) have no data representation – stay text.
- Campaign Setting PCC – **resolved** (your decision): `PRECAMPAIGN:1,INCLUDES=Expanded Psionics Handbook` added (verified: PCGen registers the requirement; it is enforced in the Source tab, not when a character file is loaded from the command line).
- Load errors outside the feats: deity domains Charm, Glory, Madness, Nobility and languages Aarakocran, Feylaar, Ur Draxa are not defined.

## Not implemented in the repo – waiting for the book text (to be posted later)
- **Kingdom of Kalamar Player's Guide**: 7 "[Not Implemented]" placeholder feats.
