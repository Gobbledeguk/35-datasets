From 13/10/2026, this contains an attempt at using Claude.ai to convert the YagmothLives collected Mostly Complete Dragon Compendium pdf. https://www.reddit.com/r/DungeonsAndDragons35e/comments/1iiq5v0/the_mostly_complete_dragon_magazine_compendium/

Updated conversion notes can be found in the repository.

19/10/2026 

Updated the repository to also contain a data folder which houses updated versions of the 35e folders from BahamuthDragon where I'm attempting to align feats to the tagged requirements, making PRETEXT requirements into actual, machine checkable requirements.

BahamutDragon PCGen data – feat review fixes
Overlay for https://github.com/bahamutdragon/pcgen (base commit d353e9b): unpack in the repository root;
every file replaces the file of the same path (no new files except where noted).

Please create issues if you find any issues - and I'm sure you will.

28/10/2026

Updated the data folder with the later review work. Every file is still an overlay for https://github.com/bahamutdragon/pcgen (base commit d353e9b): unpack or copy `data/` into the repository root; files replace the originals of the same path, and files that don't exist upstream are new.

- Feats: as before, plus the Epic Level Handbook feats checked against the free D&D v.3.5 Accessory Update booklet.
- Spells, psionic powers and Tome of Battle maneuvers: converted to the Player's Handbook's spell structure and syntax (class levels and domains in new `*_class.lst` files); Spell Compendium wins where a spell is defined in several books; Magic of Eberron's spells and powers added from the book; four maneuvers that collided with spells of the same name have their own keys.
- Equipment: all equipment files in the Player's Handbook's token order and value forms.
- Classes and deities: 19 Draconomicon prestige classes had no base attack bonus and too low Will saves (garbled formulas) – fixed; deity pantheons in the Player's Handbook's form.
- Magic of Incarnum: checked (loads cleanly, soulmeld lists complete); the lost template's emotion choice was empty – fixed. Five empty selection lists in other books (Hierophant Align, Dragon Familiar Advancement, Great Rune, Studied Foe, Thrall of Orcus) fixed; the remaining ones need book data and are listed in `notes/INCARNUM_NOTES.md`.
- Tome of Magic: mysteries and vestiges in the Player's Handbook's spell structure; checked (loads cleanly, selection lists populated). Truenaming utterances are not implemented – see `notes/TOME_OF_MAGIC_NOTES.md`.
- Complete Champion: the 11 unfinished churches completed from the book (criteria, ranks and their benefits) – see `notes/COMPLETE_CHAMPION_NOTES.md`.
- Forgotten Realms deities: checked against the Campaign Setting, the Player's Guide to Faerûn and Faiths and Pantheons; 65 genders filled, alignments, ranks, favored weapons and the Balance domain corrected, three names corrected – see `notes/FR_DEITIES_NOTES.md`.
- New book: the 3e Arms and Equipment Guide converted for 3.5 (`data/35e/wizards_of_the_coast/supplement/arms_and_equipment/`).
- The Dragonlance books from Sovereign Press (Age of Mortals, Legends of the Twins): brought in line with this data set – they now load without errors in both the 35e and Bahamut35e game modes (see `notes/DRAGONLANCE_PACKS_NOTES.md`).

Notes on what was changed and what still needs the books are in `notes/`; `data/ALL_FIXES_MANIFEST.txt` lists every file. `GDG-BD_all_fixes_281026.zip` contains all fixes as one overlay.
