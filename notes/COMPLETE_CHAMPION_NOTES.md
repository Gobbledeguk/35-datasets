# Complete Champion – churches completed from the book

Complete Champion's church affiliations: three churches were complete in the repository (Fharlanghn's Way, The Ruby
Temple, The Shining Light of Pelor); the other 11 were stubs (membership and the character-level criterion only, no
ranks). They are now complete, from the book (`review_tools/cc_churches_parse.py`, `cc_churches_build.py`), following
the complete churches and the file's own template blocks:

| Church | Deity | Criteria | Ranks |
|---|---|---|---|
| The Anvil of Creation | Moradin | 26 | 4 |
| Assembly of Balance | Ehlonna | 22 | 5 |
| The Blessed Bounty of Yondalla | Yondalla | 16 | 4 |
| The Brotherhood of Equals | Obad-Hai | 23 | 4 |
| The Eternal Library | Boccob | 21 | 4 |
| Fingers of the Laughing Rogue | Olidammara | 27 | 5 |
| The Fist of Valor | Heironeous | 20 | 4 |
| The Mighty Arms of Kord | Kord | 25 | 4 |
| Scales of Balance | St. Cuthbert | 22 | 4 |
| The Temple of True Aim | Corellon Larethian | 21 | 5 |
| The Temple of the Twinkling Eye | Garl Glittergold | 28 | 4 |

(Deities as required by the existing memberships.)

## How it is built (as in the complete churches)
- **Membership** (category Church): requires the deity, starts the affiliation score, opens the rank pool and grants
  the automatic criteria.
- **One-time criteria** PCGen can evaluate are automatic, with prerequisites: alignment, skill ranks (incl. ranges and
  "lacks ranks"), base attack bonus, save bonuses, ability scores, Power Attack, class levels, spellcasting level,
  school or specific spells (50). The others are selectable once (18) – e.g. "has visited one of the Elemental
  Planes", "has been undead", proficiencies, "+1/skill" counts.
- **Multiple-use criteria** are selectable as often as they happen (154); "+1/4 creature's CR" criteria are expanded
  per CR (from the stated minimum CR to 20), as in the Ruby Temple.
- **Ranks** (category Church Rank) cost the difference between the ranks' minimum scores and require the previous rank;
  each grants its benefit as a special ability shown under the rank's title. Unconditional skill bonuses are
  mechanical (Mighty Arms +2 Intimidate, Fingers +2 Perform and Tumble, Scales +1 Climb and Jump, True Aim +2 Sense
  Motive); everything else is in the description.
- Keys: no commas or parentheses (PCGen forbids parentheses in keys of repeatable abilities), never cut inside a
  parenthesis.

## Verified in PCGen
- All 14 churches' rank lists (4–5 ranks) and criteria lists are populated.
- A 10th-level lawful good fighter of Heironeous in the Fist of Valor with 5 ranks in Knowledge (religion) gets
  affiliation score 8 automatically (level +5, lawful +1, Knowledge +1, base attack +1); each "Converts a new member"
  adds +1; the rank Soldier-at-Arms appears on the standard 3.5 sheet with its benefit and page.
- With Complete Champion loaded: only the 11 memberships changed and 722 church abilities are new; nothing else
  changed; identical load messages.

## Notes
- **Dallah Thaun**: the Blessed Bounty also describes the church of Yondalla's dark aspect, Dallah Thaun, with its own
  criteria and ranks. Not added – the repository has no deity Dallah Thaun, so no character could qualify.
- **The Brotherhood of Equals** prints ranks 13–22 and 24–29 (23 missing – likely a misprint); the book's numbers are
  used (rank 3 costs 11).
- The Brotherhood's ranks have no titles in the book; they are named "Rank 1" … "Rank 4".
- Character files (for testers): a repeatable criterion needs `APPLIEDTO:` on its ABILITY line to count.
