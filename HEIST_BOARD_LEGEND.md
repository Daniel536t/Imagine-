# MMT V3 Core — Visual Heist Board Legend

Open `HEIST_BOARD.svg` in a browser. The numbered sections below match the drawing.

## ① Outside perimeter

1. **Perimeter fence** — the review boundary around the repository and local test environment.
2. **ACL cop** — represents `Acl` authorization checks and pool-admin/rewarder-admin roles.
3. **Version cop** — represents `Version` and `VersionCap` compatibility gates.
4. **Pool-ID cop** — represents `pool::verify_pool` and position/receipt pool-pairing checks.
5. **Slippage cop** — represents price-limit and slippage protections, including `slippage_check`.
6. **Assertions alarm** — Move `assert!` guards, invalid-range checks, pause checks, and arithmetic preconditions.
7. **Reentrancy/receipt alarm** — the flash-loan and flash-swap repayment boundary; receipts must be consumed and repaid correctly.
8. **Deployment dossier** — published package IDs and deployment metadata from the `deployments/` files; this is public deployment context, not a secret.
9. **Audit-route papers** — current investigation routes, not protocol state.

## ② The bank

10. **Security lobby**
    - `AdminCap`
    - `Acl`
    - `VersionCap`
    - `Version`
    - Administrative modules in `app.move`, `admin.move`, and `version.move`

11. **Rate-control room**
    - `GlobalConfig`
    - enabled fee rates
    - fee-rate-to-tick-spacing mapping
    - constants used by fee, price, and range validation

12. **Main vault: `Pool<X,Y>`**
    - shared pool object
    - token-X reserve
    - token-Y reserve
    - protocol fee X
    - protocol fee Y
    - total liquidity
    - current square-root price
    - current tick index
    - swap fee rate
    - flash-loan fee rate
    - protocol fee shares
    - fee-growth globals
    - reward information
    - oracle observations
    - tick bitmap and tick table

13. **Locker room**
    - `Position`
    - position liquidity
    - lower and upper ticks
    - owed token-X and token-Y fees
    - fee-growth snapshots
    - `PositionRewardInfo`
    - reward debt and reward growth snapshots

14. **Trading floor**
    - `SwapState`
    - `SwapStepComputations`
    - swap amount calculations
    - fee growth updates
    - reserve movement through `add_to_reserves` and `take_from_reserves`
    - trade/liquidity action boundary

15. **Flash desk**
    - `FlashLoanReceipt`
    - `FlashSwapReceipt`
    - flash-loan debt amounts
    - flash-swap debt amounts
    - repayment functions
    - replay/cross-pool/under-repayment investigation route

16. **Reward custody**
    - `PoolRewardInfo`
    - reward emission rate
    - reward end time
    - reward growth global
    - total allocated reward
    - reward custodian dynamic field
    - fee collection and reward collection paths

17. **Oracle and tick room**
    - `Observation`
    - observation cardinality/index
    - `TickInfo`
    - tick bitmap
    - tick spacing
    - tick gross/net liquidity
    - seconds-per-liquidity cumulative values
    - tick cumulative values
    - negative/boundary/sparse-tick investigation route

18. **Authorized entry**
    - transaction context
    - owned positions
    - owned capabilities
    - shared `Pool`, `GlobalConfig`, `Acl`, and `Version` objects

19. **Audit exits/routes**
    - cashier mismatch: payout versus cleared accounting
    - receipt replay or forgery
    - tick bitmap and crossing behavior
    - reward over-crediting or stranded funds
    - oracle observation manipulation
    - inconsistent admin/version guards
    - deployment/source drift

## Color key

- **Green** — asset custody, rewards, or accounting value.
- **Gold** — capabilities, administration, fee controls, and flash repayment obligations.
- **Cyan** — configuration, oracle, and tick machinery.
- **Purple** — positions and version controls.
- **Red** — alarms, assertions, and security boundaries.
- **Paper** — evidence, deployment metadata, or an investigation hypothesis.
- **Dashed blue arrows** — authorized flow or an audit route, not an automatic transfer of funds.

## Scope note

The picture groups related Move structs and state fields into rooms so it can be understood visually. It does not claim that every event struct is a separate stored object. Events such as `PoolCreatedEvent`, `SwapEvent`, `FeeCollectedEvent`, and admin events are emitted records and are represented by the rooms/actions that produce them rather than drawn as vaults.
