# PokeNexus Trainer Tree Planner

A click-to-plan simulator for the Trainer Tree in the PokeNexus Godot beta (client 1.0.52), for min-maxing builds before spending points in game.

## Files

| File | What it is |
|---|---|
| `index.html` | The planner. Self-contained, so it works on GitHub Pages as-is. If `skilltree.json` sits next to it, the page loads that file instead of its built-in copy, so a data update only means replacing the JSON. |
| `skilltree.json` | Full tree: 261 nodes, 276 connections, layout coordinates. |
| `skilltree.csv` | The same nodes as a flat table (one row per node, with its neighbours listed). |

## Using the planner

Click a node to take it plus the cheapest path to it, as the game does. Right-click a taken node to refund it; anything that loses its connection to the start is refunded too. Set your trainer level to lock or unlock gated nodes. Search highlights matching nodes. "Copy share link" puts the whole build in the URL, and three local save slots are available.

## What the data covers

Every node lists its name, branch, type (normal node, keystone or trainer skill), point cost, effect text, trainer level requirement and path cost (cheapest total points from the start). The path costs were checked against every "Path: N points" readout in the game, and all 261 match.

| Branch | Nodes | | Branch | Nodes |
|---|---|---|---|---|
| Seeker | 50 | | Prospector | 24 |
| Fortune | 34 | | Trainer | 24 |
| Hunter | 32 | | Explorer | 18 |
| Angler | 26 | | Battler | 16 |
| Collector | 25 | | Breeder | 12 |

There are 22 keystones (all need trainer level 30) and 11 trainer skills. Shiny Bond (Seeker) is the one node gated at level 50. Taking every node costs 342 points.

## Bonus caps

Each bonus has a hard cap, stored in `stats[]` in `skilltree.json`. 41 caps were confirmed in game, and every one equals exactly what the regular nodes for that bonus add up to. So a full set of regular nodes always reaches the cap, and the only way past it is a keystone (Shiny Obsession, Pilgrim's Vow, Treasure Hunter, Iron Will, Frugal, Nomad, Elite Slayer, Deep Core, Safari Ranger and others). The planner adds a keystone's unconditional bonuses and penalties to the same totals, caps the result, and shows anything over the cap as wasted. Conditional keystone effects (night only, Safari only, solo play and so on) are listed as text and not counted. The 18 bonuses with no confirmed cap use the sum of their nodes and are marked with \* in the planner.

## Mutually exclusive keystones

Only one keystone from each group can be held at a time. Each group is stored in `exclusiveGroups` in `skilltree.json`.

| Group | Keystones |
|---|---|
| Shiny hunting | Pilgrim's Vow, Rare Hunter, Shiny Obsession |
| Party play | Treasure Hunter, Lone Wanderer, Pack Leader |
| Location | Cave Dweller, Night Owl, Safari Ranger |
| Mining | Deep Core, Seismic Sense |
| Collecting | Collector's Creed, Catch Combo |
| Battle Tower | Iron Will, Underdogs |

The planner greys out a keystone that conflicts with one you hold, explains the conflict when clicked, and drops conflicting keystones from shared links. Elite Slayer and Horde Caller can be held together (confirmed in game). These keystones have no confirmed exclusions yet: Patient Angler, Duelist, Nomad, Frugal and Monotype Specialist.

## Known gaps

- **Points per level.** The game showed 1 point at trainer level 1. The planner assumes 1 point per level and lets you override it.
- **Penalty order.** It isn't confirmed whether a keystone penalty applies before or after the cap. The planner applies the cap to the combined total. For example, all shiny nodes plus Rare Hunter shows 15%, not 20%.
- **Hidden path costs.** Gated nodes hide their path cost in game, so those values are computed from the graph.
- **Beta data.** Values were read on 2026-11-10 and will change between beta patches.

## How it was captured

The node data was read off the in-game tooltips in the web beta, with no access to the game's files. The connections were detected from the lines the game draws between nodes and then validated against the in-game path costs. The client's data bundle is encrypted, so it wasn't used.
