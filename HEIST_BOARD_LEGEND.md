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
