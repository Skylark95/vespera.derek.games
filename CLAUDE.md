# CLAUDE.md — Vespera Reference Page

This is the Claude Code project context file. It is read automatically at the start of every Claude Code session. It provides structural context about the HTML file so that per-session task files can focus purely on the change manifest without restating standing information.

---

## What This Project Is

`index.html` is a single self-contained HTML reference page for a D&D 5e character named Vespera, used at the game table. It is deployed at https://vespera.derek.games/. All CSS and JavaScript are inline — there are no external stylesheets or script files.

---

## File Conventions

- The HTML file in this workspace is always named `index.html`
- After each session update, the output file should also be named `index.html` (overwrite in place)
- Per-session task files are named `claude_code_task_session[#].md`
- Reference markdown files are named `session_[#]_notes.md`, `party_inventory_session[#].md`, and `vespera_table_reference_session[#].md`

---

## Page Structure

The page has four tabs. All tabs are present in the HTML simultaneously; JavaScript controls which is visible.

| Tab | Contents |
|---|---|
| **Combat** | Stats block, bolt/arrow counters, spell slots, HP tracker, hit dice, attacks table, damage combos table, features & abilities (accordion), long rest button, destination/status, support point risk reference |
| **Party** | Party resources, player character entries (expandable), party insanity tracker, followers table, fungi reference table |
| **Inv** | Per-character inventory sections (Vespera, Hadrin, Mercy, Zara, Willow, David el Gnomo), unassigned/party pool section (weapons, ammunition, consumables, scrolls, documents), NPC follower equipment, currency |
| **Threads** | Open plot threads grouped by category: NPCs & Followers, Creatures & Locations, Equipment/Mechanics |

---

## Interactive Elements

The following elements are interactive and must continue to function after any update.

| Element | Behavior | Resets on Long Rest? |
|---|---|---|
| Bolt counter | Increment/decrement; persists in localStorage | Yes — resets to default |
| Arrow counter | Increment/decrement; persists in localStorage | No — arrows are not replenished by rest |
| Spell slots (1st level) | Tap to expend; persists in localStorage | Yes |
| Hunter's Sense uses | Tap to expend (up to max uses); persists | Yes |
| Favored Foe uses | Tap to expend (up to max uses); persists | Yes |
| Current HP | Increment/decrement with max cap; persists | Yes — resets to max |
| Temp HP | Increment/decrement; persists | Yes — clears on rest |
| Support Points counter | Increment/decrement with max cap; persists | No — SP are a campaign resource, not a rest resource |
| Hit Dice | Tap to use; persists | Partial — long rest restores 1 |
| Long Rest button | Resets: bolt counter, HP (to max), spell slots, Hunter's Sense, Favored Foe, temp HP, hit dice | — |
| Tab navigation | Switches visible tab; active tab persists via localStorage | No |
| Accordion entries (features, PC bios, SP risk reference) | Expand/collapse on tap | No |

---

## localStorage

The page uses two localStorage keys:
- `vespera-state` — stores all counter/tracker values as a JSON object
- `vespera-tab` — stores the active tab name

Do not change these key names. Do not modify any localStorage read/write logic.

---

## Approach for All Updates

- Make **targeted string replacements** throughout `index.html`
- Do **not** rewrite the file from scratch
- Preserve all existing CSS, JavaScript, localStorage logic, event handlers, accordion behavior, and tab switching code **exactly as they are**
- Only change display text, data values, and table/list content as specified in the per-session task file
- Read the full HTML file before beginning any edits so you understand the surrounding structure at each edit location

---

## What to Never Change

- Any `<script>` blocks
- Any `<style>` blocks
- localStorage key names (`vespera-state`, `vespera-tab`)
- Tab names or tab navigation logic
- Class names or element IDs
- The accordion expand/collapse mechanism
- The long rest reset function (except updating the bolt default and HP max values as directed per session)

---

## Counter Default and Max Values

When a per-session task updates a counter's max or default value, look for the relevant `data-max`, `data-default`, or similar attributes in the HTML element AND any matching reset logic in the long rest button's JavaScript handler. Both must be updated together.

Known counters and what to look for:

| Counter | What to update when value changes |
|---|---|
| HP max | The stat display, the tracker's max attribute, and the long rest reset value |
| Bolt counter default | The displayed default and the long rest reset value |
| Spell slot count | The number of slot pips and the long rest reset logic |
| Hunter's Sense max | The use tracker max and the stat block description |
| Favored Foe max | The use tracker max and the stat block description |
| Support Points max | The counter's max attribute and the label |
| Hit Dice total | The display label only; do not change dice type (d10) |

---

## Character Reference

Vespera is a Wood Elf Monster Slayer Ranger. Her primary ranged weapon is a longbow (1d8+4, range 150/600); her secondary ranged weapon is a hand crossbow (1d6+4, range 30/120). Both benefit from Fighting Style: Archery (+2 to attack rolls). Her melee weapons are two shortswords (1d6+4, finesse). She tracks bolt ammunition (for the hand crossbow) and arrow ammunition (for the longbow) separately.

Current party size and follower details are in the per-session task file.

---

## Deployment

Derek deploys the updated `index.html` manually. Your job is only to produce the updated file — do not attempt to push, upload, or deploy.
