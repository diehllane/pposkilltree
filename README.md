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

## Known gaps

- **Points per level.** The game showed 1 point at trainer level 1. The planner assumes 1 point per level and lets you override it.
- **Keystone rules.** Nothing in the tooltips says whether keystones exclude each other. The planner doesn't restrict them.
- **Hidden path costs.** Gated nodes hide their path cost in game, so those values are computed from the graph.
- **Beta data.** Values were read on 2026-11-10 and will change between beta patches.
