# 3e books (data/3e/wizards_of_the_coast) – review for the 3.5 data set

Scope (your choice): the Forgotten Realms books and modules, the Arms and Equipment Guide and the Epic Level
Handbook. Reference for the 3.5 changes: the free *D&D v.3.5 Accessory Update* booklet (Wizards of the Coast, 2003).

## 1. Forgotten Realms books and modules – compared with their 3.5 versions

| 3e folder | 3.5 counterpart | Result |
|---|---|---|
| Races of Faerûn | Races of Faerûn (35e) | Nothing missing. The 3e book's 18 race entries (shield dwarf, avariel, the genasi, ghostwise halfling …) exist in 3.5 as Forgotten Realms subraces; "Ride (Dire Bat)"/"Ride (Hippogriff)" are 3e per-mount Ride skills (one Ride skill in 3.5); "draonic" is a typo of Draconic; the two feats, the warsling and the shade template are in other 3.5 books. |
| Into the Dragon's Lair, Pool of Radiance, City of the Spider Queen | same modules (35e) | Identical object sets. |
| Forgotten Realms Campaign Setting (spell file only, not loaded) | Player's Guide to Faerûn / FRCS (35e) | Nothing missing (Lesser Ironguard is in two 3.5 files). |
| Magic of Faerûn (spell file only, not loaded) | Magic of Faerûn (35e) | **One spell missing: Create Crossroads and Backroad** (druid 7, p.86) – added to `mag_spells.lst`/`mag_spells_class.lst` in the PHB structure (components and cast time in 3.5 form). Everything else exists: 14 spells without the deity in parentheses (Amanuensis, Darkfire …), Mestil's Acid Breath as Acid Breath, Ghorun Toth's Metal Melt as Ghorus Toth's Metal Melt, Bane's Symbol of Death as the PHB's Symbol of Death, and two typos (blood freny, wind tinnel). |

## 2. Epic Level Handbook – checked against the booklet

Already in 3.5 form: all revised benefits (Epic Inspiration, Holy/Unholy Strike, Improved Combat Reflexes, Improved
Whirlwind Attack, Legendary Leaper/Rider, Self Concealment …), most revised prerequisites (Keen Strike, Vorpal
Strike, Mighty Rage, Mobile Defense, Plant Wild Shape, Uncanny Accuracy, Magical Beast Companion, Improved Flyby
Attack), Beast Wild Shape removed, the renamed items (anarchic/axiomatic power, universal energy resistance/immunity)
and the revised damage reduction of Great Invulnerability, Ironskin, the rod of invulnerability, Golem Armor and the
Invulnerable Coat.

Fixed:
- Improved Ki Strike: Wis 21 → 25.
- Righteous Strike: ki strike (lawful) added as a prerequisite.
- Trap Sense: shown as Epic Trapfinding (key unchanged, so saved characters keep it).
- Penetrate Damage Reduction: the choice is a special material (adamantine, cold iron, silver) – it offered
  alignments, magic, epic and weapon types and lacked cold iron.
- Rod of Invulnerability: its +5 natural armor is an enhancement bonus to natural armor.
- Ring of Universal Energy Resistance, Minor (84,000 gp, resistance 10 to all five energies) added – it was missing.
  Key `Ring of Universal Energy Resistance (Minor/Epic)`, distinct from the Magic Item Compendium's minor ring.

Not checked (not encoded as data in the repository, or outside the booklet's data-relevant parts): epic prestige class
progressions, epic monsters, epic skill usages.

## 3. Arms and Equipment Guide – converted for 3.5

The repository's 3e data was already structurally 3.5 (light/one-handed/two-handed wield categories, light shields,
no 3e damage reduction) and loads in 3.5 without messages. Changes:
- PCC: game mode Bahamut35e, 3.5 core requirement; placed in `data/35e/wizards_of_the_coast/supplement/arms_and_equipment/`
  with its campaign name unchanged (Unearthed Arcana's weapon-group support and Races of Faerûn already refer to it).
- Text (booklet terms): Medium-size → Medium, subdual → nonlethal, Wilderness Lore and Intuit Direction → Survival,
  Pick Pocket → Sleight of Hand, Alchemy → Craft (alchemy), Ambidexterity → Two-Weapon Fighting; item names
  "Cage (Medium-size)" and "Leash and Muzzle (Medium-size)" → "(Medium)". The `Subdual` equipment type stays (3.5 data
  uses it too).
- **Same key, different object** – these would have silently replaced 3.5 objects, and now have their own keys:
  Ring → Ring Armor (the DMG's Ring is the base magic ring), Coral → Coral Armor (the DMG's Coral is a gem),
  Ice Axe → Ice Axe (Tool) (Races of Faerûn's is a weapon), the spiked collar (clothing) → key Collar (Spiked/AEG).
- **Reprinted in 3.5 books – the 3.5 reprint wins:** 33 objects moved to `ae_*_dup*.lst` files that load only when
  none of the reprinting books is loaded (Dragon Magazine Compendium, Complete Warrior, Forgotten Realms Campaign
  Setting, Races of Faerûn, Races of Stone, Races of the Wild, Dungeonscape, Libris Mortis, Magic Item Compendium);
  4 weapon proficiencies dropped because the always-loaded Universal Rules define them (Chakram, Claw Bracer, Khopesh,
  Maul). Exception: Flight Arrow and Signal Arrow stay in the guide unconditionally – Races of Faerûn already yields
  them to the guide.
- Verified in PCGen: as-is versus converted differ only by the changes above; with the reprinting books loaded every
  duplicate comes from the 3.5 book; Unearthed Arcana's support file resolves; no load messages.

## Noticed, not changed
- Races of Faerûn's PCC loads `rac_equip.lst` twice when the guide is loaded without Complete Adventurer (its first
  and third EQUIPMENT lines both apply) – harmless, the definitions are identical.
- Epic Level Handbook: Self Concealment has an incomplete source page ("p.").
