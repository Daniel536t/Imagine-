# Nightglass — Hollow Citadel Alias Ledger

The SVG is intentionally written as a fictional world so the map can be imagined freely. The names below are the private correspondence between the story and the MMT V3 review model.

## How to read the map

- **Columns A–L and rows 1–7** are the chess-style planning grid.
- **Rooms are deliberately scattered and slightly turned** so the citadel feels like a place, not a dashboard or a symmetrical matrix.
- **Watchers** are authorization or invariant monitors.
- **Watch-eyes** are observable checkpoints where a trace can be remembered.
- **Bells** are failed guards, invalid inputs, aborts, or suspected accounting inconsistencies.
- **Doors and arches** are imagined boundaries between capabilities, ownership, package checks, and state transitions.
- **The black trace** is the only route line. It is drawn after a scenario runs so we record what actually happened.

## Fictional alias mapping

| SVG name | Hidden review meaning |
|---|---|
| **Nightglass** | The fictional name for this visual review world |
| **Hollow Citadel** | The complete MMT V3 shared-object system |
| **Ivory Foyer** | `AdminCap`, `Acl`, `VersionCap`, and `Version` entry controls |
| **Crown Token** | `AdminCap` |
| **Oath Ring** | `Acl` |
| **Clock Seal** | `VersionCap` / `Version` compatibility gate |
| **Tuning Forge** | `GlobalConfig` and fee/spacing constants |
| **Master Dial** | `GlobalConfig` |
| **Amber Heart** | `Pool<X,Y>` shared pool state |
| **Sun Well** | Token-X reserve and related fee custody |
| **Moon Well** | Token-Y reserve and related fee custody |
| **Mirror Lockers** | `Position` objects and LP range state |
| **Mirror Shard** | A `Position` |
| **Echo Ledger** | `PositionRewardInfo` and reward snapshots |
| **Clocktower** | Pause gates and package/version control paths |
| **Blue Hall** | The conceptual transaction/checkpoint corridor |
| **Tide Market** | Swap/trade state and swap calculations |
| **Current Board** | `SwapState` |
| **Tide Calculations** | `SwapStepComputations` |
| **Borrower's Table** | Flash-loan and flash-swap lifecycle |
| **Borrowing Token** | `FlashLoanReceipt` |
| **Exchange Token** | `FlashSwapReceipt` |
| **Garden of Ash** | Reward custody, emission, and collection |
| **Ash Seed Ledger** | `PoolRewardInfo` |
| **Hidden Seed Vault** | Reward custodian dynamic field |
| **Timewell** | Oracle observations and historical cumulative values |
| **Echo Stone** | `Observation` |
| **Boundary Garden** | Tick state, bitmap navigation, spacing, and crossings |
| **Boundary Stone** | `TickInfo` |
| **Star Map / stride** | Tick bitmap and tick spacing |
| **Archive of Papers** | Deployment metadata, lockfiles, source configuration, and test evidence |
| **Ledger Chamber** | Owed fees, rewards, safe withdrawal, actual transfer, and debt clearing |
| **Bell Archive** | Alarm results, traces, and caught/cleared outcomes |
| **Return Register** | Final scenario state and next investigation route |
| **Ivory Key watcher** | ACL/role authorization monitor |
| **Clock Seal watcher** | Version compatibility monitor |
| **Twin Seal watcher** | Pool/position/receipt pairing monitor |
| **Glass Needle watcher** | Slippage and price-limit monitor |
| **Broken Oath bell** | Assertions, invalid ranges, pause checks, and arithmetic preconditions |
| **Borrowed Mask bell** | Flash repayment and one-time receipt boundary |

## Fictional locations

### The Outer Ring

- **North Causeway** — sealed papers and old maps.
- **South Causeway** — return lane and quiet exit.
- **West Causeway** — bearer tokens and keeper rites.
- **East Causeway** — echo stones and borrowed masks.
- **South Arch** — authorized transaction entry.
- **Paper Arch** — deployment and version evidence.
- **Keeper's Arch** — owned position/capability boundary.
- **Echo Arch** — receipt and observation boundary.

### The inner rooms

1. **Ivory Foyer** — capability and authorization controls.
2. **Tuning Forge** — configuration and fee/spacing controls.
3. **Amber Heart** — two token wells, reserves, liquidity, price, fees, rewards, oracle, and tick state.
4. **Mirror Lockers** — user positions, ranges, liquidity, owed fees, and reward snapshots.
5. **Clocktower** — pause and compatibility controls.
6. **Blue Hall** — the conceptual order of checks before and after a state transition.
7. **Tide Market** — swap calculations, price limits, fee growth, and reserve movement.
8. **Borrower's Table** — flash-loan and flash-swap debt/repayment lifecycle.
9. **Garden of Ash** — reward emission, custody, growth, debt, and collection.
10. **Timewell** — observation history, timestamps, cardinality, and interpolation.
11. **Boundary Garden** — initialized ticks, bitmap movement, spacing, crossings, and liquidity changes.
12. **Archive of Papers** — deployment/build/test evidence.
13. **Ledger Chamber** — accounting reconciliation.
14. **Bell Archive** — outcome recording.
15. **Return Register** — the next route to test.

## The four fictional tales

- **The Thin Payout** — compare a promise being cleared with the purse actually being transferred. This is the `safe_withdraw` / fee / reward accounting scenario.
- **The Borrowed Mask** — check whether a flash token is bound to the right heart, repaid once, and gone afterward.
- **The Edge of Time** — explore negative, boundary, sparse, and timestamp/cardinality cases around the Boundary Garden and Timewell.
- **The Ash Drift** — compare emission updates, rounding, custody, reward debt, and final gathering.

## The black trace protocol

The board deliberately contains only one route line. After each local audit scenario:

1. Start at the fictional entry arch.
2. Follow the scenario's conceptual calls through the rooms.
3. Mark each watcher, watch-eye, and bell encountered.
4. Draw the actual path as one black line over the board.
5. Record the stopping point in the Return Register.
6. Add the result to the next tale without changing the fictional names on the SVG.

The black line is a record of what we tried, not a prewritten route.

## Material key

- **Green** — living stores, custody, rewards, and accounting value.
- **Gold** — keys, oaths, tolls, and borrowed obligations.
- **Cyan** — wells, stars, time, and measures.
- **Purple** — mirrors and clockwork.
- **Blue** — ordinary stores and flow.
- **Red** — bells and watchers.
- **Paper** — rumors, maps, clues, and evidence.

## Scope note

This is a fictional visualization layer over a local protocol-security review. The alias names are for imagination; the mapping above preserves the technical meaning for analysis. The board does not represent a real-world bank or a physical attack plan.
