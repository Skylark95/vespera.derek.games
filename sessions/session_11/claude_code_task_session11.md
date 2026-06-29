# Task: Update Vespera Reference Page — Session 11

## Context

You are updating a single self-contained interactive HTML reference page for a D&D 5e character named Vespera. The page is used at the game table as a quick reference for stats, inventory, followers, and open plot threads. It was last updated for Session 10. This task brings it current through Session 11 (6/13/2026).

The page has four tabs (Combat, Party, Inv, Threads) and several interactive elements: a bolt counter, an HP counter, temp HP, spell slot trackers, a Hunter's Sense use tracker, a Favored Foe use tracker, a Support Points counter, a Hit Dice tracker, and a long-rest reset button. All of these persist via localStorage. The interactivity must remain fully intact after your edits.

---

## Files in Your Workspace

- `index.html` — the current HTML file to update (single self-contained file; CSS and JS are inline)
- `vespera_table_reference_session11.md` — **authoritative source for all Vespera stats, spells, inventory, followers, and open threads as of Session 11**
- `session_11_notes.md` — full session notes (use for narrative context and thread descriptions)
- `party_inventory_session11.md` — full party inventory (use for per-character and party pool item details)

When any value in this task document conflicts with `vespera_table_reference_session11.md`, the markdown file is correct.

---

## Approach

Make **targeted string replacements** throughout `index.html`. Do **not** rewrite the file from scratch. Preserve all existing CSS, JavaScript, localStorage logic, event handlers, accordion behavior, and tab switching code exactly as they are. Only change content values, labels, and display text as specified below.

Read the full HTML file before making any changes so you understand the existing structure and can find the correct locations for each edit.

---

## Critical Constraints

- Do not alter any JavaScript logic, localStorage keys, or event listeners
- Do not change the tab structure or navigation
- Do not change any CSS class names or styling
- All existing interactive counters must continue to work correctly after your edits
- The long rest reset button must continue to reset all appropriate trackers
- Do not add any new JavaScript files or external dependencies

---

## Complete Change Manifest

Work through these changes in order. Each section corresponds to a region of the HTML.

---

### 1. Page Header / Identity Block

| Field | Current | New |
|---|---|---|
| Class/level line | "Monster Slayer Ranger 3" | "Monster Slayer Ranger 4" |
| Session number | "Session 10" | "Session 11" |
| Session date | "5/30/2026" | "6/13/2026" |

---

### 2. Combat Tab — Stats

| Stat | Current | New |
|---|---|---|
| AC display | 14 | 16 |
| AC formula note | "AC 14 = studded leather 11 (degraded S6) + DEX +3" | "AC 16 = studded leather 12 (new S11) + DEX +4" |
| HP Max (display label) | 32 | 40 |
| HP Max (tracker max value) | 32 | 40 |
| Initiative | +3 | +4 |
| Stealth | +7 | +8 |
| Hit Dice total | "3 total" | "4 total" |

The HP tracker currently shows "max 32 · tap to adjust". Update to "max 40 · tap to adjust". If the tracker has a `data-max` or similar attribute, update it to 40.

---

### 3. Combat Tab — Bolt / Arrow Counters

**Bolt counter:** The existing bolt counter label and default value of 34 are correct — do not change them.

**Add an arrow counter:** Add a new counter for arrows immediately after the bolt counter, using the same HTML structure and pattern as the bolt counter. Label it "Arrows". Default value: 40. This counter should also be included in the long rest reset (arrows do not reset on long rest — do NOT include it in the long rest reset). Use a distinct localStorage key such as `vespera-arrows`.

---

### 4. Combat Tab — Attacks Table

Remove the existing attacks table and replace it with the following three-row version:

| Weapon | To Hit | Damage |
|---|---|---|
| Longbow | +8 | 1d8+4 piercing |
| Hand Crossbow | +8 | 1d6+4 piercing |
| Shortsword ×2 | +6 | 1d6+4 piercing |

Update the note beneath the attacks table to:
"Longbow and Hand Crossbow both include +2 from Fighting Style: Archery. Roll20 may display +6 for the Hand Crossbow — the correct value is +8."

---

### 5. Combat Tab — Damage Combos Table

Update all instances of "1d6+3" in the damage combos table to reflect the new modifier. Because Vespera now has two ranged weapons with different damage dice (1d8+4 longbow, 1d6+4 hand crossbow), replace the base damage expressions as follows:

Replace the table's base damage column header or intro text to add:
"Base damage: Longbow 1d8+4 · Hand Crossbow / Shortsword 1d6+4. Substitute as appropriate."

Then update each row's damage expressions by replacing "1d6+3" with "base+4" throughout the combos table (both first-hit and subsequent-hit columns):

| Row | First Hit | Subsequent |
|---|---|---|
| Slayer's Prey only | base+4 + 1d6 | base+4 |
| Hunter's Mark only | base+4 + 1d6 | base+4 + 1d6 |
| ★ Both stacked | base+4 + 2d6 | base+4 + 1d6 |
| Favored Foe only | base+4 + 1d4 | base+4 |

---

### 6. Combat Tab — Features & Abilities

**Remove the Ensnaring Strike entry entirely** (title, subtitle/tags, and expanded description content).

**Add a Goodberry entry** in the same accordion style as the other spell entries. Place it where Ensnaring Strike was. Use this content:

Title: "Goodberry"
Tags/subtitle: "1st-lvl spell · 1 slot"
Expanded description: "Action. Up to **10 magical berries** appear in your hand. A creature can use its action to eat one berry, restoring **1 HP** and providing nourishment for one day. Berries lose their potency after **24 hours** of casting. Requires material component (sprig of mistletoe). Costs 1 spell slot."

**Update the Protection from Evil & Good entry note** to read:
"Hadrin's assembled spell component pouch (recovered from the black stone tower, S8) is available to Vespera outside of combat. Original component pouch still missing."
(Remove the specific mention of Hadrin carrying original equipment, as the original equipment thread has been partially resolved.)

---

### 7. Combat Tab — Support Points Counter

Update the support points counter:
- Max value: 11 → 10
- Any label displaying "max 11": update to "max 10"
- If the counter has a `data-max` attribute, update it to 10
- Default/reset value: 10

---

### 8. Combat Tab — Destination / Status Block

Update the destination and status block:

| Field | Current | New |
|---|---|---|
| Destination | "Gracklstugh" | "Gracklstugh" (unchanged) |
| Status | "✅ ARRIVED (S10)" | "In city — tracking Droki in West Cleft District (S11)" |

---

### 9. Party Tab — Player Characters

Update each character entry's description:

**Vespera:**
Replace "Monster Slayer Ranger 3" with "Monster Slayer Ranger 4".
Replace "Original equipment missing" note or warning with: "Longbow recovered S11. Carries healer's kit and explorer's pack (S11)."

**Hadrin:**
- Remove "shortsword" from the list of items he carries.
- Remove the mace delivery note ("Mace to be delivered to Werz Saltbarren as customs tax (S10)").
- Add "light crossbow (S11)" to his carried items.
- Add a note: "Mace identified as Torch Mace S11; given to Zara."

**Mercy:**
- Add to her entry: "Maul traded at Blade Bazaar S11."

**Zara:**
- Add to her entry: "Carries Torch Mace (magic weapon, identified S11) in addition to mace. Holy symbol spotted in Themberchaud's hoard S11 — not yet retrieved."

**David el Gnomo:**
- Add to his entry: "new armor (S11; type unconfirmed; homebrew pricing)"

---

### 10. Party Tab — Followers Table

Update the followers section header from "Followers (11 active)" to "Followers (9 active)".

**Buppido:** Change status icon from ✅ to 🚪. Update notes to: "Derro. No longer traveling with party as of S11; departure circumstances unrecorded. Long-standing suspicion figure — cut backpack S8; confronted S10."

**Hemeth:** Change status icon from ✅ to 🚪. Update notes to: "Duergar. No longer traveling with party as of S11; departure circumstances unrecorded. Presence had aided entry to Gracklstugh (S10)."

All other follower rows are unchanged.

---

### 11. Party Tab — Party Resources

Add the following row to the party resources table (or section):
"Party pool gold | ~347 gp | 68 gp from S10 + 279 gp net from S11 Blade Bazaar transactions"

---

### 12. Inv Tab — Vespera's Inventory

Remove:
- "⚠ Original equipment missing: longbow, quiver, arrows, component pouch" warning/note
- "Studded leather armor AC base 11 — degraded by gray ooze S6"

Add:
- "Studded leather armor AC base 12 — new, purchased S11"
- "Longbow purchased S11; replaces original missing since S1"
- "Quiver purchased S11"
- "40 arrows purchased S11" (note: tracked by the new Arrows counter on the Combat tab)
- "Healer's kit purchased S11"
- "Explorer's pack purchased S11: backpack, bedroll, 2 costumes, 5 candles, 5 days of rations, waterskin, disguise kit, 50 ft. of hempen rope"
- "1 common clothes purchased S11"

Replace the original equipment note at the bottom of Vespera's section with:
"Longbow, quiver, and arrows now in possession (S11). Original component pouch still missing; Hadrin's assembled pouch is available outside of combat."

---

### 13. Inv Tab — Hadrin's Inventory

Remove:
- "Shortsword given by Mercy after black pudding combat, S6"
- The mace entry ("Mace donated by Glabagoul, S6 — to be delivered to Werz Saltbarren as customs tax (S10)")

Add the following struck-through notes for documentation:
- "Shortsword — traded at Blade Bazaar S11"
- "Mace (Glabagoul's donation S6) — identified as Torch Mace; given to Zara S11"

Add:
- "Light crossbow purchased at Blade Bazaar S11"
- "20 crossbow bolts purchased at Blade Bazaar S11 (for light crossbow)"

---

### 14. Inv Tab — Mercy's Inventory

Remove "Maul looted from mummified corpse cocoon, S4" or replace with struck-through:
- "Maul — traded at Blade Bazaar S11"

---

### 15. Inv Tab — Zara's Inventory

Add:
- "Torch Mace magic weapon; identified S11; previously Hadrin's mace — Glabagoul's donation S6. Zara now carries both this and her S4 mace."

---

### 16. Inv Tab — David el Gnomo's Inventory

Add:
- "Suit of armor purchased at Blade Bazaar S11; type unconfirmed — 100 gp (homebrew pricing); flagged for DM confirmation"

---

### 17. Inv Tab — Party Pool: Weapons & Armor

Make these changes to the weapons/armor list:

| Item | Change |
|---|---|
| "4 suits of plate mail armor orog ambush, S9" | Change to "1 suit of plate mail armor (1 remaining of 4 from orog loot S9; 3 sold at Blade Bazaar S11)" |
| "3 greataxes orog ambush, S9" | Change to "1 greataxe (1 remaining of 3 from orog loot S9; 2 traded at Blade Bazaar S11)" |
| "1 shortsword drow cocoons S4; holder unconfirmed" | Remove entirely (traded S11) |
| "1 shortsword drow ambush S3; holder unconfirmed" | Remove entirely (sold S11 for 5 gp) |

Add these new items:
- "3 whips purchased at Blade Bazaar S11; recipients unassigned — flagged for confirmation"
- "3 rapiers purchased at Blade Bazaar S11; recipients unassigned — flagged for confirmation"
- "1 gnarled quarterstaff purchased at Blade Bazaar S11; recipient unassigned — flagged for confirmation"
- "20 pitons purchased at Blade Bazaar S11"
- "1 hammer purchased at Blade Bazaar S11"

---

### 18. Inv Tab — Currency Section

| Entry | Change |
|---|---|
| "Party pool: 68 gp 41 gp from S9; +27 gp orog loot S10; not yet divided" | Update to: "Party pool: 347 gp (68 gp from S10 + 279 gp net from S11 Blade Bazaar transactions)" |
| "Party pool: 121 sp 106 sp from S9; +15 sp orog loot S10" | Update to: "Party pool: 119 sp (121 sp from S10; −2 sp in S11 transactions)" |
| "Party pool: 2 green gold bracelets 25 gp each; 1 of 3 spent on maps S7" | Remove entirely (both sold at Blade Bazaar S11) |

---

### 19. Threads Tab — NPCs & Followers Section

**Update** the Buppido thread entry:
"Buppido — departed S11; circumstances unrecorded. Long-standing suspicion figure — cut backpack S8; confronted by Mercy S10, denied it. His departure in Gracklstugh without explanation is itself notable."

**Update** the Werz Saltbarren thread entry. Replace with:
"Werz Saltbarren murder — found dead at Darklake docks S11; multiple cauterized stab wounds; killer unknown. Party cleared of suspicion. Mace was never delivered; identified as Torch Mace S11 and given to Zara."

**Add** these new thread entries to the NPCs & Followers section:
- "Hemeth — departed S11; circumstances unrecorded. Duergar whose presence had aided the party's entry to Gracklstugh (S10)."
- "Gartokkar — Keeper of the Flame representative who escorted the party to Themberchaud S11; further role unknown."
- "Themberchaud liaison — guard assigned by Themberchaud S11 to work with the party; name not recorded at the table."

---

### 20. Threads Tab — Creatures & Locations Section

**Add** these new thread entries:

- "Themberchaud — red dragon of Gracklstugh; 'Father of Flame, Foundry's Heart.' Party is his agents: fulfill Keepers of the Flame requests but report to him first. Issued gold pins (S11)."
- "Droki — duergar in West Cleft District; linked to a conspiracy and to the Gray Ghosts; party tasked by Errde Blackskull (capture/kill) and Themberchaud (follow to find the Gray Ghosts)."
- "The Gray Ghosts — thieves' guild in Gracklstugh; stole Themberchaud's red dragon egg; believed responsible for the Faerzress disturbance; party must recover the artifact they used."
- "Errde Blackskull — Captain of the Stone Guard; interrogated the party after Werz's murder; cleared them and assigned the Droki mission in exchange for safe passage out of Gracklstugh."

---

### 21. Threads Tab — Equipment / Mechanics Section

**Update** the "Original equipment" thread entry:
"Original equipment — longbow, quiver, and arrows replaced via S11 purchases. Original component pouch still missing; Hadrin's assembled pouch available outside combat."

**Add** these new thread entries:

- "Zara's holy symbol — visible in Themberchaud's hoard S11; has been missing since Session 1 when equipment was stripped by the drow; not yet retrieved."
- "Zara's mace situation — carries both her S4 mace and the Torch Mace received S11; whether she retains both long-term is unrecorded."
- "Gold pins (broken arrow symbol) — issued by Themberchaud S11; the broken arrow holy symbol has been seen around Gracklstugh but its affiliation is not recognized by the party."
- "Errde Blackskull's conspiracy target — faction name unclear in notes (recorded as 'coluncel of sivance'); flagged for DM confirmation."
- "New weapon assignments S11 — 3 rapiers, 3 whips, 1 gnarled quarterstaff purchased at the Blade Bazaar; distributed to specific party members at the table but not recorded."
- "David el Gnomo's armor — purchased for 100 gp S11; type unconfirmed (homebrew pricing); flagged for DM confirmation."

---

## Output

Write the updated file as `index.html`. Verify before finishing that:
- All four tabs (Combat, Party, Inv, Threads) render their updated content correctly in the HTML structure
- No JavaScript functions, localStorage keys, or event listeners have been removed or altered
- The long rest button resets bolt counter, HP, spell slots, Hunter's Sense, Favored Foe, Support Points, and Hit Dice — but does NOT reset the new Arrows counter
- The page header reads "Monster Slayer Ranger 4 · Session 11 · 6/13/2026"
