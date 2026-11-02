# Forgotten Realms deities – checked against the Forgotten Realms Campaign Setting

## How deities are built (PHB and Forgotten Realms)
- **PHB** (19 deities + "None"): `DOMAINS:<domains>|PREALIGN:<followers' alignments>`, `DEITYWEAP`, `ALIGN`, source tokens,
  `FACTSET:Pantheon|Base|PH`.
- **Player's Guide to Faerûn** (119 deities – the Realms' 3.5 deity data): the same mechanism, plus the divine rank as
  `TYPE` (Greater/Intermediate/Lesser/Demigod), `DESC` "<name> (gender)" and `FACTSET:Pantheon|Faerun`. It labels 14
  Greyhawk deities "Not FR Deity" (they stay selectable) and adds the Elf domain to Corellon Larethian.
- **Forgotten Realms Campaign Setting** (`frcs_deities.lst`): only 28 names – always loaded together with the Player's
  Guide (which includes it) and overridden by its full definitions (checked in PCGen).
- **Lost Empires of Faerûn** (10 dead deities): domains without follower alignments, no source page.
- **Faiths and Pantheons** in the repository has no deities (prestige classes, class abilities, companions,
  templates only; status ALPHA, source date 2015-05 though the book is from 2002).

## Checked against the book (Table 5–1 to 5–8 and the 28 detailed entries)
- 113 of the 119 deities are in the book's tables; 6 are not (added later): Ulutiu, Deep Duerra, Laduguer,
  Calladuran Smoothhands, plus the two misspelled names below.
- The 25 deities citing the Campaign Setting have exactly the book's page.
- Differences, mostly 3.0 → 3.5 updates in the Player's Guide: Death domain → Repose (Jergal, Kelemvor, Osiris,
  Urogalan); halfspear → shortspear (Talos, Sebek, Baervan Wildwanderer, Set, Gruumsh, Angharradh); probably 3.5:
  Auril Water → Cold, Umberlee Water → Weather. **Not changed, to check with the Player's Guide or Faiths and
  Pantheons**: ranks of Bane and Istishia (book Greater, data Intermediate) and Uthgar (book Lesser, data Demigod);
  Ilneval (book NE, data CE); Cyrrollalee (data adds quarterstaff); Urogalan (book "any flail", data dire flail);
  Deneir (book dagger, data longsword); Shiallia (book quarterstaff, data trident).

## Changed (your decision)
- Gender from the book's entry headings for 13 deities that had "()": Chauntea, Mielikki (F); Gond, Helm, Ilmater,
  Lathander, Malar, Mask, Oghma, Shaundakul, Talos, Tempus, Uthgar (M). All genders already in the data agree with the
  book.
- Names corrected: "Gwaeron Windstorm" → Gwaeron Windstrom, "Baghtru" → Bahgtru (old spellings kept as keys, so saved
  characters and references keep working).
- Verified in PCGen: the same 140 deities with unchanged keys; only these descriptions and names differ.

## Checked against the Player's Guide to Faerûn and Faiths and Pantheons (OCR)
- **The Player's Guide has no deity entries or deity table**: its introduction says the Faiths and Pantheons deities
  "can be used as previously presented"; it updates what the 3.5 rules changed – the domains, listed per domain in
  chapter 3 ("Deities: …"). So the deities' statistics come from Faiths and Pantheons (the 25 major deities from the
  Campaign Setting), their 3.5 domains from the Player's Guide.
- Faiths and Pantheons (OCR, 107 entries, 106 deities identified): parser checked against independent data – gender
  agrees in 63 of 64 cases, rank in 102 of 105, alignment in 93 of 95 (the differences are the corrections below).
- Player's Guide domain lists (30 domains): all match the data except the Balance domain.

## Changed (your decision)
- **Gender** for 52 more deities from Faiths and Pantheons (pronouns in each entry's description); **Red Knight
  male → female** (the "Lady of Strategy").
- **Alignment**: Laduguer neutral good → **lawful evil**, Ilneval chaotic evil → **neutral evil** (their cleric
  alignments already matched the corrected alignments).
- **Rank**: Bane and Istishia Intermediate → **Greater**, Uthgar Demigod → **Lesser** (Faiths and Pantheons and the
  Campaign Setting agree).
- **Favored weapon**: Deneir longsword → **dagger**, Shiallia trident → **quarterstaff** (both books agree).
- **Balance domain** added for Grumbar, Oghma, Ubtao and Waukeen (the Player's Guide's 3.5 list).
- **Name**: "Calladuran Smoothhands" → Callarduran Smoothhands (old spelling kept as the key).
- Verified in PCGen: the same 140 deities with unchanged keys; only these values changed; no load messages.

## Open
- **Cleric alignments**: for 40 deities Faiths and Pantheons lists narrower cleric alignments than the data, which
  follows the PHB's rule (one step from the deity, so TN for a LN deity). Not changed – both readings are defensible.
- **Callarduran Smoothhands' favored weapon** (data dagger; the OCR suggests battleaxe but couldn't confirm it).
- **Gender** still empty for 16 deities (OCR didn't yield a usable entry): Eldath, Finder Wyvernspur, Lliira,
  Ghaunadaur, Abbathor, Berronar Truesilver, Gorm Gulthyn, Haela Brightaxe, Sharindlar, Vergadain, Angharradh,
  Erevan Ilesere, Urdlen, Brandobaris, Urogalan, Yurtrus.
- **Source attribution**: 88 deities cite the Player's Guide, which has no deity pages. Their Faiths and Pantheons
  pages are below, in case they should cite that book instead.

| Deity (citing the Player's Guide) | Faiths and Pantheons page |
|---|---|
| Akadi | p.90 |
| Auril | p.91 |
| Beshaba | p.91 |
| Deneir | p.92 |
| Eldath | p.93 |
| Finder Wyvernspur | – |
| Garagos | p.94 |
| Gargauth | p.95 |
| Grumbar | p.96 |
| Gwaeron Windstrom | p.96 |
| Hoar | p.97 |
| Istishia | p.98 |
| Jergal | p.98 |
| Lliira | p.99 |
| Loviatar | p.100 |
| Lurue | p.101 |
| Milil | p.102 |
| Nobanion | p.102 |
| Red Knight | p.103 |
| Savras | p.104 |
| Sharess | p.105 |
| Shiallia | p.105 |
| Siamorphe | p.106 |
| Talona | p.107 |
| Tiamat | p.108 |
| Ubtao | p.108 |
| Ulutiu | p.109 |
| Valkur | p.110 |
| Velsharoon | p.110 |
| Anhur | p.141 |
| Geb | p.142 |
| Hathor | p.142 |
| Horus-Re | p.143 |
| Isis | p.144 |
| Nephthys | p.145 |
| Osiris | p.146 |
| Sebek | p.146 |
| Set | p.147 |
| Thoth | p.147 |
| Ghaunadaur | p.111 |
| Kiaransalee | p.112 |
| Selvetarm | p.113 |
| Vhaeraun | p.113 |
| Abbathor | p.115 |
| Berronar Truesilver | – |
| Clangeddin Silverbeard | p.116 |
| Deep Duerra | p.117 |
| Dugmaren Brightmantle | p.117 |
| Dumathoin | p.118 |
| Gorm Gulthyn | p.118 |
| Haela Brightaxe | – |
| Laduguer | p.120 |
| Moradin | p.121 |
| Sharindlar | p.122 |
| Thard Harr | p.122 |
| Vergadain | – |
| Aerdrie Faenya | p.123 |
| Angharradh | – |
| Corellon Larethian | p.125 |
| Deep Sashelas | p.126 |
| Erevan Ilesere | – |
| Fenmarel Mestarine | p.127 |
| Hanali Celanil | p.128 |
| Labelas Enoreth | p.128 |
| Rillifane Rallathil | p.129 |
| Sehanine Moonbow | p.129 |
| Shevarash | p.130 |
| Solonor Thelandira | p.131 |
| Baervan Wildwanderer | p.132 |
| Baravar Cloakshadow | p.133 |
| Callarduran Smoothhands | p.133 |
| Flandal Steelskin | p.134 |
| Gaerdal Ironhand | p.135 |
| Garl Glittergold | p.135 |
| Segojan Earthcaller | p.136 |
| Urdlen | – |
| Arvoreen | p.137 |
| Brandobaris | – |
| Cyrrollalee | p.139 |
| Sheela Peryroyl | p.139 |
| Urogalan | p.140 |
| Yondalla | – |
| Bahgtru | p.148 |
| Gruumsh | p.148 |
| Ilneval | p.149 |
| Luthic | p.150 |
| Shargaas | p.150 |
| Yurtrus | p.151 |

## Needs other books
- See "Open" above.
