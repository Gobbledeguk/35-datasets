# Other object types against the Player's Handbook – review

Classes, races, skills, domains and deities against the Player's Handbook; templates against the Monster Manual
(the PHB has none). Survey first, then only clear errors and derivable fixes (after the special-ability revert).

## Fixed
- **Draconomicon: 19 prestige classes had no base attack bonus and too low Will saves.** 38 formulas read
  `classlevel("APPLIEDAS=NONEPIC")asslevel("APPLIEDAS=NONEPIC")` (an upstream search-and-replace accident), which
  PCGen evaluates as 0. Fixed to `classlevel("APPLIEDAS=NONEPIC")`; the Dispassionate Watcher of Chronepsis'
  `/3*4` is `*3/4` (its own fractional variable is ClassBABModerate). Measured at level 4: Dragonslayer BAB +0 → +4,
  Will +2 → +4; Dracolyte and Dispassionate Watcher BAB +0 → +3; Dragonkith BAB +0 → +4, Will +0 → +1. Affected:
  Disciple of Ashardalon, Dispassionate Watcher of Chronepsis, Dragon Ascendant (and Ex), Elemental Master,
  Hidecarved Dragon, Sacred Warder of Bahamut, Unholy Ravager of Tiamat, Dracolyte (and Ex), Dragonkith, Dragonrider,
  Dragonslayer, Dragonsong Lyrist, Dragonstalker, Hoardstealer, Initiate of the Draconic Mysteries, Platinum Knight,
  Talon of Tiamat.
- **Deities: `PANTHEON:x` → `FACTSET:Pantheon|x`** (the PHB's form) – 11 deities in Lords of Madness and Libris Mortis.
- **Magic of Incarnum: Totem Rager `Base.Fortitude`/`Base.Will` → `BASE.…`** (cosmetic – PCGen ignores the case; the
  numbers are identical before and after).

## Checked and in order
- No class uses the older `SPELLTYPE` – all 140 spellcasting classes use `FACT:SpellType` like the PHB.
- 559 base-attack and 1,783 save tokens are in exactly the PHB's form.
- Tokens the core books don't use (SR, DR, SPELLS, UDAM, VISION, … on classes) are legitimate PCGen tokens for
  features the core classes don't have.
- Two "race files" with raw book text are not loaded by any PCC (Fey Feature `ff_races.lst` – commented out –,
  Spell Compendium `sc_races.lst`).

## Open decision – optional base-attack rules
176 base-attack tokens in 33 class files lack the parts the PHB uses for Unearthed Arcana's alternate and
fractional base-attack variants (`PREVAREQ:UseAlternateBABProgression,0`, the ClassBABModerate/ClassBABPoor
variables). With the default rules they compute exactly the same values; with those variants switched on, these
classes would add up differently from the PHB's. Adding the missing parts is derivable from each class's progression.

## Data gaps (need the books)

### Races (1573 objects in loaded files)

| File | no RACETYPE | no SIZE | no MOVE | no FACE | no LEGS | no CR | no SOURCEPAGE |
|---|---|---|---|---|---|---|---|
| 35e/wizards_of_the_coast/core/monster_manual/mm_races.lst | 2 | 10 | 1 | 13 | 24 | 10 | 10 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/races_of_faerun/rac_races.lst | 24 | 0 | 0 | 24 | 4 | 13 | 1 |
| 35e/wizards_of_the_coast/supplement/expanded_psionics_handbook/xph_races.lst | 0 | 0 | 0 | 25 | 15 | 17 | 0 |
| 35e/wizards_of_the_coast/supplement/draconomicon/dr_races.lst | 0 | 12 | 0 | 12 | 12 | 1 | 12 |
| 35e/wizards_of_the_coast/supplement/libris_mortis/lm_races.lst | 0 | 0 | 0 | 2 | 36 | 5 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/unapproachable_east/una_races.lst | 14 | 0 | 0 | 14 | 7 | 7 | 0 |
| 35e/paizo/dragon_magazine_compendium/dmc_races.lst | 0 | 0 | 0 | 0 | 0 | 41 | 0 |
| 35e/kenzer_and_co/kokc_races.lst | 4 | 4 | 4 | 4 | 4 | 4 | 4 |
| 35e/wizards_of_the_coast/campaign_settings/ghostwalk/gw_races.lst | 1 | 1 | 0 | 9 | 9 | 1 | 0 |
| 35e/wizards_of_the_coast/supplement/monster_manual_2/mm2_races.lst | 0 | 8 | 3 | 8 | 1 | 0 | 0 |
| darksun_35e/campaign_setting/dscs_races.lst | 0 | 0 | 0 | 0 | 8 | 0 | 9 |
| 35e/wizards_of_the_coast/supplement/dragon_magic/dm_races.lst | 0 | 0 | 1 | 7 | 0 | 2 | 6 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/players_guide_to_faerun/pg_races.lst | 2 | 1 | 1 | 1 | 5 | 3 | 1 |
| 35e/wizards_of_the_coast/campaign_settings/dragonlance/campaign/dcs_races.lst | 1 | 0 | 1 | 0 | 4 | 8 | 0 |
| 35e/wizards_of_the_coast/supplement/magic_of_incarnum/moi_races.lst | 0 | 1 | 0 | 5 | 4 | 4 | 0 |
| 35e/paizo/dragon_magazine_compendium/dmc_races_xph.lst | 0 | 0 | 0 | 0 | 0 | 12 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/oriental_adventures/oriental_adventures/oa_races.lst | 1 | 0 | 0 | 2 | 2 | 5 | 0 |
| 35e/wizards_of_the_coast/supplement/frostburn/fr_races.lst | 2 | 0 | 0 | 2 | 2 | 2 | 2 |
| 35e/wizards_of_the_coast/campaign_settings/eberron/campaign/ecs_races.lst | 0 | 1 | 0 | 0 | 3 | 4 | 1 |
| 35e/wizards_of_the_coast/supplement/stormwrack/sto_races.lst | 0 | 0 | 0 | 3 | 3 | 3 | 0 |
| 35e/wizards_of_the_coast/supplement/lords_of_madness/lom_races.lst | 0 | 0 | 0 | 0 | 4 | 1 | 4 |
| 35e/wizards_of_the_coast/supplement/sandstorm/sa_races.lst | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| 35e/wizards_of_the_coast/supplement/races_of_the_wild/rw_races.lst | 0 | 0 | 0 | 1 | 4 | 2 | 0 |
| 35e/sovereign_press/dragonlance/age_of_mortals/aom_races.lst | 0 | 0 | 0 | 2 | 2 | 2 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/monsters_of_faerun/mon_races.lst | 0 | 2 | 0 | 2 | 0 | 2 | 0 |
| 35e/wizards_of_the_coast/supplement/races_of_stone/rs_races.lst | 0 | 0 | 0 | 1 | 2 | 3 | 0 |
| 35e/guardians_of_order/besm_revised/besm_races.lst | 0 | 0 | 1 | 1 | 1 | 1 | 1 |
| 35e/valar_project/book_of_erotic_fantasy/boef_races.lst | 0 | 0 | 0 | 5 | 0 | 0 | 0 |
| 35e/wizards_of_the_coast/supplement/monster_manual_3/mm3_races.lst | 0 | 1 | 0 | 1 | 1 | 1 | 1 |
| 35e/wizards_of_the_coast/supplement/races_of_the_dragon/rdr_races.lst | 0 | 0 | 0 | 1 | 2 | 1 | 1 |
| 35e/green_ronin/the_psychics_handbook/tph_races.lst | 0 | 0 | 0 | 1 | 2 | 1 | 1 |
| 35e/green_ronin/advanced_player_manual/apm_races.lst | 1 | 0 | 0 | 1 | 1 | 1 | 1 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/shining_south/shs_races.lst | 0 | 0 | 0 | 0 | 2 | 2 | 0 |
| 35e/wizards_of_the_coast/supplement/unearthed_arcana/ua_races.lst | 0 | 0 | 1 | 1 | 0 | 1 | 1 |
| 35e/wizards_of_the_coast/supplement/book_of_vile_darkness/bv_races.lst | 1 | 0 | 0 | 0 | 1 | 1 | 1 |
| 35e/sword_and_sorcery/campaign_setting/ravenloft/ravenloft_players_handbook/rph_races.lst | 0 | 0 | 0 | 1 | 1 | 1 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/champions_of_ruin/cr_races.lst | 0 | 0 | 0 | 0 | 3 | 0 | 0 |
| 35e/wizards_of_the_coast/supplement/races_of_destiny/rd_races.lst | 0 | 0 | 0 | 0 | 1 | 2 | 0 |
| 35e/wizards_of_the_coast/supplement/complete_adventurer/cad_races.lst | 0 | 0 | 0 | 1 | 1 | 0 | 1 |
| 35e/wizards_of_the_coast/supplement/savage_species/ss_races.lst | 0 | 0 | 1 | 0 | 1 | 1 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/_modules/pool_of_radiance_attack_on_myth_drannor/por_races.lst | 0 | 0 | 0 | 0 | 2 | 0 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/underdark/und_races.lst | 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 35e/wizards_of_the_coast/supplement/complete_psionic/cp_races.lst | 0 | 0 | 0 | 1 | 0 | 1 | 0 |
| 35e/wizards_of_the_coast/supplement/book_of_exalted_deeds/be_races.lst | 0 | 0 | 0 | 0 | 2 | 0 | 0 |
| 35e/paizo/dragon_magazine_compendium/dmc_races_cadv.lst | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| 35e/paizo/dragon_magazine_compendium/dmc_races_ca.lst | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| 35e/wizards_of_the_coast/web/spellbook_archive/sa_races.lst | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/eberron/magic_of_eberron/moe_races.lst | 0 | 0 | 0 | 0 | 0 | 1 | 0 |
| 35e/wizards_of_the_coast/supplement/heroes_of_horror/hh_races.lst | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| 35e/wizards_of_the_coast/supplement/epic_level_handbook/el_races.lst | 0 | 0 | 0 | 1 | 0 | 0 | 0 |
| 35e/wizards_of_the_coast/supplement/fiend_folio/ff_races.lst | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| 35e/wizards_of_the_coast/supplement/complete_arcane/car_races.lst | 0 | 0 | 1 | 0 | 0 | 0 | 0 |

### Deities (448 objects in loaded files)

| File | no DOMAINS | no ALIGN | no DEITYWEAP |
|---|---|---|---|
| 35e/kenzer_and_co/kokc_deities.lst | 43 | 0 | 43 |
| 35e/kenzer_and_co/kalamar/players_guide/kokpg_deities.lst | 43 | 0 | 43 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/players_guide_to_faerun/frcs/frcs_deities.lst | 28 | 28 | 28 |
| 35e/green_ronin/the_book_of_fiends/tbof_deities.lst | 0 | 31 | 31 |
| darksun_35e/campaign_setting/dscs_deities.lst | 6 | 25 | 6 |
| 35e/wizards_of_the_coast/campaign_settings/dragonlance/campaign/dcs_deities.lst | 5 | 1 | 21 |
| 35e/wizards_of_the_coast/campaign_settings/eberron/campaign/ecs_deities.lst | 0 | 2 | 22 |
| 35e/wizards_of_the_coast/supplement/book_of_vile_darkness/bv_deities.lst | 4 | 0 | 19 |
| 35e/malhavoc_press/module/return_to_the_temple_of_elemental_evil/rt_deities.lst | 2 | 2 | 2 |
| 35e/valar_project/book_of_erotic_fantasy/boef_deities.lst | 0 | 1 | 1 |
| 35e/wizards_of_the_coast/supplement/heroes_of_horror/hh_deities.lst | 0 | 1 | 1 |
| 35e/wizards_of_the_coast/supplement/draconomicon/dr_deities.lst | 0 | 0 | 2 |
| 35e/sword_and_sorcery/campaign_setting/ravenloft/ravenloft_players_handbook/rph_deities.lst | 0 | 0 | 1 |
| 35e/wizards_of_the_coast/supplement/book_of_exalted_deeds/be_deities.lst | 0 | 0 | 1 |
| 35e/wizards_of_the_coast/core/players_handbook/ph_deities.lst | 0 | 1 | 0 |

### Domains (371 objects in loaded files)

| File | no DESC | no SPELLLEVEL | no SOURCEPAGE |
|---|---|---|---|
| darksun_35e/campaign_setting/dscs_domains.lst | 1 | 0 | 22 |
| 35e/wizards_of_the_coast/supplement/complete_divine/cd_domains.lst | 8 | 8 | 0 |
| 35e/green_ronin/the_book_of_fiends/tbof_domains.lst | 0 | 8 | 8 |
| 35e/wizards_of_the_coast/campaign_settings/oriental_adventures/oriental_adventures/oa_domains.lst | 8 | 6 | 0 |
| 35e/wizards_of_the_coast/supplement/spell_compendium/sc_domains.lst | 0 | 8 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/players_guide_to_faerun/pg_domains.lst | 1 | 1 | 1 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/unapproachable_east/una_domains.lst | 0 | 1 | 0 |
| 35e/wizards_of_the_coast/supplement/fiendish_codex_ii/fci_domains.lst | 0 | 0 | 1 |

### Skills (384 objects in loaded files)

| File | no KEYSTAT | STR/DEX without ACHECK |
|---|---|---|
| 35e/guardians_of_order/besm_revised/besm_skills.lst | 11 | 18 |
| 35e/wizards_of_the_coast/core/players_handbook/ph_skills.lst | 3 | 3 |
| 35e/wizards_of_the_coast/campaign_settings/oriental_adventures/oriental_adventures/oa_skills.lst | 3 | 0 |
| 35e/wizards_of_the_coast/campaign_settings/forgotten_realms/lost_empires_of_faerun/le_skills.lst | 0 | 2 |
| 35e/green_ronin/the_psychics_handbook/tph_skills.lst | 2 | 0 |
| 35e/wizards_of_the_coast/supplement/unearthed_arcana/ua_skills.lst | 1 | 0 |
| 35e/wizards_of_the_coast/supplement/complete_scoundrel/cs_skills.lst | 1 | 0 |


Note: races in a file can legitimately lack tokens they get from a template or `.MOD` elsewhere; the PHB itself
has skills without USEUNTRAINED (optional token) and templates without SOURCEPAGE, so those are not listed.

## Unearthed Arcana: Battle Sorcerer – spells per day and known (your decision)
BahamutDragon's battle sorcerer used the plain sorcerer's tables. The variant (Unearthed Arcana, open content) has one
spell per day less at each spell level (minimum 0) and one spell known less at each spell level (minimum 1). Both tables
derived from the PHB sorcerer's data in the repository (20 level lines, CAST and KNOWN only). Matches the rule's examples:
1st level 4/2 per day; 4th level 5/2/1 known; 5th level 5/3/1. Verified in PCGen (Cha 19): known and per day at levels
1/4/5/20 exactly as derived (+ Charisma bonus spells per day). The spell list itself (SPELLLIST:1|Sorcerer) was already right.
