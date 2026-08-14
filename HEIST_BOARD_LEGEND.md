# Nightglass — Fictional Bank Interior Legend

The SVG is intentionally a fictional **bank building**. It uses ordinary story objects—manager, security, workers, cashier tables, cameras, alarms, vaults, loopholes, and records—so the review can be imagined as a heist-board world. The technical correspondence stays here, not on the artwork.

## How to read the board

- **A–L / 1–7** is the chess-style planning grid.
- The rooms are aligned as a building floor plan; the bank interior is the stable baseline.
- **Workers** are transaction actors or internal processing steps.
- **The manager** is the administrative authority.
- **Security officers** are authorization and invariant guards.
- **Cameras** are observable checkpoints.
- **Alarms** are failed checks, aborted scenarios, or detected inconsistencies.
- **The vault** is shared custody and accounting state.
- **Loophole cards** are hypotheses added after a run; they are not prewritten exploits.
- **The black trace** is drawn after a scenario to show what was actually attempted.

## Bank-object mapping

| SVG bank object | MMT review meaning |
|---|---|
| **Fictional Bank Building** | The complete MMT V3 shared-object system |
| **Security Lobby** | `AdminCap`, `Acl`, `VersionCap`, and `Version` entry controls |
| **Manager** | `AdminCap` / administrative authority |
| **Security Roster** | `Acl` roles and authorization relationships |
| **Access Register** | `Version` / `VersionCap` compatibility checks |
| **Cashier Tables** | `GlobalConfig`, fee rates, and spacing/validation controls |
| **Rate Board** | `GlobalConfig` and fee configuration |
| **Main Vault** | `Pool<X,Y>` shared pool state |
| **Cash Room A** | Token-X reserve and associated fee custody |
| **Cash Room B** | Token-Y reserve and associated fee custody |
| **Customer Lockers** | `Position` objects and LP range state |
| **Customer File** | One `Position` and its range/liquidity data |
| **Claim Ledger** | Position fee/reward snapshots and owed amounts |
| **Manager's Office** | Pause gates and package/version control paths |
| **Security Corridor** | Conceptual transaction/checkpoint order |
| **Cashier Floor** | Swap/trade state and swap calculations |
| **Cashier Log** | `SwapState` |
| **Counting Sheets** | `SwapStepComputations` and amount/fee calculations |
| **Loan Desk** | Flash-loan and flash-swap lifecycle |
| **Loan Receipt** | `FlashLoanReceipt` |
| **Repayment Receipt** | `FlashSwapReceipt` or repayment evidence |
| **Staff Room** | Reward custody, worker/payroll-style accounting, and collection |
| **Worker Payroll** | `PoolRewardInfo`, reward growth, debt, and collection state |
| **Payroll Safe** | Reward custodian dynamic field |
| **Camera Room** | Oracle observations and historical records |
| **Camera Log** | `Observation` and cumulative timestamp data |
| **Blind-Spot Room** | Tick boundaries, bitmap movement, spacing, and loophole hypotheses |
| **Loophole Card** | A post-run investigation hypothesis, not a confirmed vulnerability |
| **Security Office** | Deployment metadata, lockfiles, source configuration, and test evidence |
| **Accounting Office** | Owed fees, rewards, safe withdrawal, actual transfer, and debt clearing |
| **Incident Board** | Alarm results, traces, and caught/cleared outcomes |
| **Exit Register** | Final scenario state and the next route to test |

## Building perimeter

- **North Street** — delivery and records approach.
- **South Street** — customer entrance and exit.
- **West Street** — staff entrance and deliveries.
- **East Street** — camera access and loan desk.
- **Main Entrance** — ordinary authorized entry.
- **Records Entrance** — deployment/version evidence.
- **Staff Entrance** — owned positions and capabilities.
- **Loan / Camera Entrance** — receipt and observation paths.

## Interior staff and security

- **Manager** — administrative authority and manager-only transitions.
- **Security Officer** — ACL, role, version, pool-pairing, and invariant checks.
- **Workers** — named visual placeholders for transaction steps and internal processing.
- **Cashiers** — swap/collection processing points.
- **Cameras** — trace checkpoints and evidence locations.
- **Alarms** — assertion failures, bad ranges, pause conditions, slippage failures, and repayment failures.

## Post-run investigation board

The **Blind-Spot Room** is intentionally empty of confirmed weaknesses. After a local scenario runs, add a loophole card only when the evidence supports it. Each card should record:

1. Which room and grid square were involved.
2. Which worker, cashier, camera, or alarm was reached.
3. The black-trace stopping point.
4. The expected accounting invariant.
5. The observed result.
6. Whether the card is a confirmed issue, a blocked hypothesis, or a test gap.

## Scenario names

- **The Thin Payout** — compare accounting credit cleared with the actual amount transferred; this covers `safe_withdraw`, fees, and rewards.
- **The Borrowed Mask** — verify loan/repayment receipts, pool pairing, one-time use, and exact repayment.
- **The Edge of Time** — examine boundary, sparse, negative, and timestamp/cardinality cases in the camera and blind-spot rooms.
- **The Worker Payroll Drift** — compare reward updates, rounding, custody, debt, and collection.
- **The Manager's Key** — compare capability, ACL, version, pause, and administrative checks.
- **The Records Mismatch** — compare deployment metadata, source package identity, and lockfile configuration.

## Run 01 — Cashier Fee Collection

- **Entrance:** Main Entrance / Gate S.
- **Route:** Gate S / Main Entrance → D3 Staff Room → D2 Loan Desk → D1 Cashier Floor → E2 Accounting Office.
- **Action:** generate a normal swap fee, crystallize the position claim, collect it once, then collect again.
- **Observed result:** claim and returned coins matched in both token types; one collection event was emitted; the second collection returned zero.
- **Outcome:** **PASS / no accounting mismatch demonstrated**.
- **Movie replay:** The front bell at Gate S gives one quiet note. The crew crosses into D3 Staff Room, passes the worker roster, and slips into D2 Loan Desk, where the repayment receipt is checked but never reused. They continue to D1 Cashier Floor, take the fee ledger to E2 Accounting Office, and find the numbers balanced. The cashier window closes; the second collection is silent. No real-world bank or funds are involved—this is a fictional protocol replay.
- **Board trace:** the black line now records this completed route. It is evidence of the run, not a future route proposal.

## Run 02 — The Loan Receipt

- **Entrance:** Gate S / Main Entrance.
- **Route:** Gate S / Main Entrance → D3 Staff Room / Worker Payroll → D2 Loan Desk → E2 Accounting Office.
- **Action:** create a controlled `FlashLoanReceipt`, calculate principal plus fee, repay exactly, then exercise one-unit-underpayment cases for both flash-loan and flash-swap receipts.
- **Observed result:** exact repayment increased each reserve by exactly its calculated fee; one-unit underpayment aborted for both receipt types.
- **Outcome:** **PASS / repayment boundary held; no reserve loss demonstrated**.
- **Alarms:** the short-repayment checks tripped as expected. The transaction did not complete with insufficient funds.
- **Movie replay:** At Gate S, the crew crosses the payroll room without opening the safe. At D2, the clerk issues a loan receipt stamped with the pool’s identity and the fee due. In E2, the exact repayment restores the vault and leaves only the fee behind. A second envelope arrives one coin short; the alarm rings, the scene rewinds, and the vault is unchanged.
- **Scope limit:** this run did not claim to prove receipt replay or cross-pool misuse. Those remain separate tests because the existing Move resource and pool-identity checks must be demonstrated explicitly.
- **Board trace:** the black line now records Run 02 and ends at the accounting office. The previous Run 01 path is retained in this legend as historical evidence, not as a second SVG route.

## Run 03 — The Payroll Shuffle

- **Entrance:** Gate S / Main Entrance.
- **Route:** Gate S → D3 Staff Room / Worker Payroll → D1 Cashier Floor → D4 Camera Room → D5 Blind-Spot Room → E2 Accounting Office.
- **Action:** create two positions with the same range, generate fees with a swap, collect A then B, generate fees again, and collect B then A.
- **Observed result:** each position received exactly its own crystallized claim in both collection orders. No claim was cleared without its matching payout.
- **Outcome:** **PASS / collection order did not alter accounting; no value mismatch demonstrated**.
- **Movie replay:** The crew passes the payroll safe without opening it. At the cashier floor, two workers receive identical claim slips. The first shuffle sends Worker A to the window before Worker B; the second sends B before A. The cameras compare both ledgers, and E2 finds the same sums in either order.
- **Scope limit:** this run exercised fee accounting only. Reward emission timing, clock changes, and partial liquidity removal remain separate unrun branches.
- **Board trace:** the black line now records Run 03 and ends at the accounting office. Earlier runs remain documented above as historical evidence.

## Run 04 — The Vault Exit

- **Entrance:** Gate S / Main Entrance.
- **Route:** Gate S → D1 Cashier Floor → B3 Main Vault → E2 Accounting Office.
- **Action:** create two identical positions, generate fees, then compare `collect → remove half` with `remove half → collect`.
- **Observed result:** both positions received their complete fee claims, and final reserves equaled initial reserves minus liquidity withdrawals and fee payouts.
- **Outcome:** **PASS / no reserve drain or claim loss demonstrated**.
- **Movie replay:** The crew reaches the vault with two matching ledgers. Worker A collects before opening the inner door; Worker B opens the door before collecting. E2 subtracts every returned coin from the vault record and finds the same balance either way. The vault door closes without a missing token.
- **Scope limit:** this run covered fee claims and partial liquidity removal. Reward-custodian timing, tick-crossing boundaries, and clock advancement remain separate tests.
- **Board trace:** the black line now records Run 04 and ends at the accounting office. Earlier runs remain documented above as historical evidence.

## Run 05 — The Blind-Spot Boundary

- **Entrance:** Gate S / Main Entrance.
- **Route:** Gate S → D1 Cashier Floor → D5 Blind-Spot Room → B3 Main Vault → E2 Accounting Office.
- **Action:** place one position above the shared boundary and one below it, move the price to the boundary, then move below it and collect both claims.
- **Observed result:** both positions retained fees accrued up to the boundary; after crossing below it, the upper-range claim stopped increasing and the lower-range claim increased. Each collected exactly its recorded claim.
- **Outcome:** **PASS / tick-boundary fee allocation matched the exercised range semantics; no value mismatch demonstrated**.
- **Movie replay:** The camera watches two workers standing on opposite sides of the same line. At the line, both ledgers retain what was earned before the crossing. Once the price slips below it, the upper worker leaves the earning floor and the lower worker takes over. E2 checks both envelopes and finds no missing coin.
- **Scope limit:** this run covered fee growth and tick crossing. Reward-custodian timing and clock advancement remain separate tests.
- **Board trace:** the black line now records Run 05 and ends at the accounting office. Earlier runs remain documented above as historical evidence.

## Run 06 — The Timekeeper’s Payroll

- **Entrance:** Gate S / Main Entrance.
- **Route:** Gate S → D3 Staff Room / Worker Payroll → D4 Camera Room → B3 Main Vault → E2 Accounting Office.
- **Action:** seed a fixed reward, test a pre-start claim, add a second position mid-emission, partially remove it, collect at the exact end, and collect again after the end.
- **Observed result:** pre-start and post-end collections returned zero; both claims survived timing and partial removal; payouts matched recorded reward debt; total payout stayed within the seeded reward amount.
- **Outcome:** **PASS / no reward overpayment, claim loss, or post-end emission demonstrated**.
- **Movie replay:** The timekeeper keeps the payroll safe sealed until the bell. One worker arrives early, another joins halfway through, and one leaves before closing. At the final bell, both envelopes match their ledgers. After closing, the empty windows stay empty.
- **Scope limit:** this run covered start/end timing and partial removal. Multi-reward ordering and clock-boundary rounding remain separate tests.
- **Board trace:** the black line now records Run 06 and ends at the accounting office. Earlier runs remain documented above as historical evidence.

## Black-trace protocol

There is only one route line on the SVG, and it is black. After each local review run:

1. Start at the relevant entrance.
2. Move through the bank rooms in the order the scenario actually uses.
3. Note each worker, cashier, camera, and alarm encountered.
4. Draw the actual path on the black trace.
5. Record the stopping point on the Incident Board.
6. Add a Loophole Card only if the evidence justifies it.

The line is a record of what happened—not a prewritten plan.

## Material key

- **Green** — customer funds, worker payouts, rewards, and accounting value.
- **Gold** — manager keys, security authority, fees, and receipts.
- **Cyan** — cameras, records, measurements, and configuration.
- **Purple** — customer lockers and access/version records.
- **Blue** — ordinary reserves and bank flow.
- **Red** — alarms and security boundaries.
- **Paper** — evidence, incident notes, and hypotheses.

## Scope note

This is a fictional visualization layer over a local protocol-security review. It is not a real bank layout or a physical attack plan. The bank objects are storytelling metaphors; the mapping above preserves the technical meaning for analysis.
