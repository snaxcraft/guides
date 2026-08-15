# snaxcraft dailies + Quest Point shop

**Last verified:** 2026-08-14 (9-day cycle, 108 dailies, bread smelt, Kitchen chain)  
**Applies to:** Paper 26.2 / Quests Classic 5.3.2 / CommandPanels / TAB  
**Edition:** Java only

Optional side content. The branched ladder (`guide/snaxcraft-quests.md`) stays separate. Completed ladder history is **`/qc`** (not this board).

## Quick commands

| Command | What |
|---------|------|
| `/q` | **Active** quests (ladder tips **and** any dailies you took) |
| `/ql` | Available ladder quests **GUI** (dailies intentionally excluded) |
| `/daily` or `/qd` | **Today’s** daily board — take/re-check here |
| `/qc` | Completed ladder + Together only (dailies stay on `/qd`) |
| `/qp` | Quest Point shop |
| `/qs` | Quest stats / QP total |

## How lists are organized

Each command opens a different list:

| List | Contents |
|------|----------|
| `/q` | **Active** only (never completed). **Left-click** a quest to start or stop tracking it; a tracked quest points your compass and shows in the boss bar. `/track` (`/qt`) and **`/kit quest`** do the same. |
| `/ql` | Ladder unlocks only. Click an entry to toggle it. |
| `/qd` | **Today’s** board — finished dailies stay listed (lime “done”) until swap. |
| `/qc` | Ladder/Together completion history — **excludes** all dailies. |

## How dailies work

- **Reset:** every day at **7:00 PM Pacific** (PST/PDT).
- **Personal (8) / Shared (4):** same board for everyone; shared uses Together-style progress sharing.
- **Pools:** 72 personal / 36 shared on a fixed **9-day** board cycle.
- **Rewards:** QP + exp + items scaled to difficulty (easy/medium/hard/shared) — below `/qp` god-roll.
- **Daily QP:** easy **6** · medium **10** · hard **16** · shared **24**.
- **Bread quests:** bread dailies count **smelting**, not crafting — bake dough in a furnace.
- **Auto-give:** today’s 12 are handed to you at the **7:00 PM Pacific** reset, or when you next log in if you were offline.
- **Backup:** if your dailies are missing, take them from **`/qd`**. That is normal on your very first join.
- Together quests only start arriving after you finish **Gotta Start Somewhere**.
- Unfinished dailies drop when the board swaps, so finish them before 7:00 PM Pacific.

Source: `server/plugins/Quests/storage/quests.yml`  
Source: https://pikamug.gitbook.io/quests/beginner/planner

## QP shop (`/qp`)

Spend **Quest Points** (not Vault money) in the `/qp` menu.

Full stock, prices, and what is not sold: [`guide/snaxcraft-qp-shop.md`](snaxcraft-qp-shop.md).

QP comes from dailies (main) and the ladder (drip).

Source: `guide/snaxcraft-qp-shop.md`
Source: `server/plugins/CommandPanels/panels/qp-shop.yml`

## Tab list

Hold Tab: the footer lists your active **personal** and **shared** dailies, plus any ladder and Together steps you are on. Finished lines drop off.

Source: `server/plugins/TAB/config.yml`  
Source: `server/plugins/CommandPanels/panels/daily.yml`
