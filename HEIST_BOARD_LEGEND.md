# MMT V3 Core — Expanded Protocol Floor Plan Legend

Open `HEIST_BOARD.svg` in a browser and zoom in. This version is a large, top-down, chess-style planning map rather than a compact dashboard.

## How to read the board

- **Columns A–L and rows 1–7** form the planning grid. A location can be described as a square, such as `B2` or `H5`.
- **Rooms** group related Move modules, structs, state fields, and transaction boundaries.
- **Corridors** represent conceptual call-flow/checkpoint order. They are not a claim about physical network topology.
- **Dashed colored routes A–G** are deterministic audit scenarios. They model protocol call order and guard coverage, not real-world intrusion instructions.
- **Cameras** mark observable checkpoints where a trace or invariant can be recorded.
- **Cops** represent authorization or invariant monitors.
- **Alarms** represent an abort, failed assertion, invalid input, or suspected accounting inconsistency.
- **Doors/gates** represent a module, capability, ownership, or package/version boundary.

## A — Outer perimeter / approach board

1. **North service road** — deployment and package-metadata approach.
2. **South service road** — authorized transaction approach and audit exit.
3. **West road** — owned positions and capability route.
4. **East road** — flash receipts, observations, and evidence route.
5. **Perimeter fence** — the trust boundary around deployment context, object ownership, shared objects, and transaction inputs.
6. **COP-01 ACL** — `Acl` authorization checks and role separation.
7. **COP-02 VERSION** — `Version` / `VersionCap` compatibility checks.
8. **COP-03 POOL-ID** — pool-position and pool-receipt pairing checks.
9. **COP-04 SLIPPAGE** — price-limit and slippage protections, including the dependent `slippage_check` package.
10. **ALARM-01 ASSERTS** — Move `assert!` guards, invalid ranges, pause checks, and arithmetic preconditions.
11. **ALARM-02 RECEIPT** — flash-loan / flash-swap repayment and receipt-consumption boundary.
12. **CAM-01 through CAM-08** — perimeter and room checkpoints for evidence capture.
13. **Gates N/S/W/E** — conceptual entry boundaries for deployment evidence, authorized transactions, owned positions, and receipts/oracle data.

## B — The bank / shared-object building

The building shell is the `mmt_v3` shared-object system. It is divided into five top-row rooms, a central transaction corridor, five lower-row rooms, and evidence desks.

### B1 — Security lobby

14. `AdminCap`
15. `Acl`
16. `VersionCap`
17. `Version`
18. Administrative paths in `admin.move`, `app.move`, and `version.move`
19. **Lobby camera and alarm** — administrative observability and unauthorized-path failure boundary.

### B2 — Rate control

20. `GlobalConfig`
21. Enabled/disabled trading configuration
22. Swap and protocol fee rates
23. Fee-rate-to-tick-spacing mapping
24. Constants used by fee, price, range, and validation logic
25. `global_config.move` and constants-related machinery
26. **Rate-control camera and alarm** — configuration-change evidence and invalid-rate guards.

### B3 — Main vault: `Pool<X,Y>`

27. Shared pool object
28. Token-X reserve
29. Token-Y reserve
30. Protocol fee X and protocol fee Y
31. Total liquidity
32. Current square-root price
33. Current tick index
34. Swap fee rate and flash-loan fee rate
35. Protocol fee shares
36. Fee-growth globals
37. Reward information attached to pool state
38. Oracle observations attached to pool state
39. Tick bitmap and tick table attached to pool state
40. `add_to_reserves` and `take_from_reserves`
41. `pool.move` custody and pool-state transitions
42. **Vault camera and alarm** — reserve movement, price limits, arithmetic, and pool-state evidence.

### B4 — Position lockers

43. `Position`
44. Position liquidity
45. Lower and upper ticks
46. Owed token-X and token-Y fees
47. Fee-growth snapshots
48. `PositionRewardInfo`
49. Reward debt and reward-growth snapshots
50. Owned LP object boundary
51. **Locker camera** — position ownership, pool pairing, range, and liquidity evidence.

### B5 — Control room

52. Trading pause/toggle
53. Package/version checks used by state-changing paths
54. Admin-only transitions
55. Global safety switches
56. **Control-room camera and alarm** — inconsistent perimeter checks or unexpected administrative state.

## C — Central corridor / transaction bus

57. Ownership checkpoint
58. Pool-ID pairing checkpoint
59. Slippage/price-limit checkpoint
60. Accounting checkpoint
61. Assertion/receipt-consumption checkpoint
62. Conceptual sequence: owned object or capability → shared pool → validation → state update → balance/receipt return.
63. The corridor is a planning abstraction for Move call flow, not a statement that the protocol uses a literal bus.

## D — Lower operating rooms

### D1 — Trading floor

64. `SwapState`
65. `SwapStepComputations`
66. Swap amount calculations
67. Fee growth updates
68. Price-limit checks
69. Tick traversal during a swap
70. Reserve movement through pool helpers
71. `trade.move` swap and trade boundary
72. **Trading camera and alarm** — slippage, price limits, overflow/wrapping behavior, and reserve invariants.

### D2 — Flash desk

73. `FlashLoanReceipt`
74. `FlashSwapReceipt`
75. Flash-loan debt amounts
76. Flash-swap debt amounts
77. Receipt pool ID
78. Repayment functions
79. Receipt consumption / one-time-use boundary
80. **Flash camera and alarm** — replay, cross-pool, forged, and under-repayment scenarios.

### D3 — Reward custody

81. `PoolRewardInfo`
82. Reward emission rate
83. Reward end time
84. Reward growth global
85. Total allocated reward
86. Reward custodian dynamic field
87. Reward debt and collection paths
88. Fee collection and reward collection boundary
89. **Reward camera and alarm** — rounding, end-time, over-credit, underpayment, and stranded-fund scenarios.

### D4 — Oracle room

90. `Observation`
91. Observation timestamp
92. Observation cardinality and index
93. Cumulative tick values
94. Seconds-per-liquidity cumulative values
95. Observation write/interpolation path
96. **Oracle camera and alarm** — stale, boundary, interpolation, and manipulation hypotheses.

### D5 — Tick room

97. `TickInfo`
98. Tick bitmap
99. Tick spacing
100. Tick gross liquidity
101. Tick net liquidity
102. Tick crossing and initialized/uninitialized boundaries
103. Negative, boundary, and sparse-tick scenarios
104. **Tick camera and alarm** — bitmap navigation, crossing, range, and liquidity-preservation evidence.

## E — Evidence and accounting desks

105. **E1 Evidence Desk** — deployment files, published IDs, `Move.lock`, source/build configuration, and baseline test results.
106. **E2 Accounting Ledger** — owed fees, rewards, `safe_withdraw`, actual transfers, and debt clearing.
107. **E3 Incident Desk** — alarm events, trace timeline, route result, and caught/cleared outcome.
108. **E4 Exit Log** — final scenario state and follow-up route to test next.

## F — Route inventory

### Route A — Authorized swap

`South entry → central corridor → Security/ownership checkpoint → Trading Floor → pool vault → slippage checkpoint → clean exit`.

Question: do the final reserve, fee-growth, price, and user-balance deltas match the intended swap invariant?

### Route B — Position / fee collection

`East entry → pool-ID checkpoint → Position Lockers → Reward Custody or Accounting Ledger → authorized exit`.

Question: is the position paired with the correct pool, and do fee/reward claims match the snapshots and owed amounts?

### Route C — Receipt repayment check

`North gate → Main Vault → central corridor → Flash Desk → repayment checkpoint → consume receipt`.

Question: can a receipt be replayed, cross-pool reused, under-repaid, or consumed inconsistently with the balance movement?

### Route D — Deployment / version gate

`North service road → Evidence Desk → Version/Control Room → Security Lobby → authorized state-changing path`.

Question: are package/version/capability checks consistent across every administrative and state-changing entry point?

### Route E — Oracle / tick edge

`West entry → Trading Floor → Tick Room → Oracle Room → pool price/tick state`.

Question: do negative, boundary, sparse, and timestamp/cardinality cases preserve liquidity and oracle invariants?

### Route F — Reward accounting

`East entry → central corridor → Reward Custody → Accounting Ledger → collection/exit`.

Question: do emission updates, rounding, end times, custody, debt, and actual transfers remain synchronized?

### Route G — Clean baseline trace

`South entry → corridor checkpoints → Main Vault → ordinary successful path`.

This is the control route used to compare a scenario under investigation with a known passing path.

## G — Scenario cards

- **A1 Cashier mismatch:** `safe_withdraw` → fee/reward debt → actual transfer. Compare “accounting cleared” with “assets transferred.”
- **A2 Receipt replay:** flash receipt → pool ID → repayment → consume. Check one-time use and pool binding.
- **A3 Tick/oracle edge:** negative, boundary, or sparse tick → observation read/write. Check navigation and interpolation.
- **A4 Reward drift:** emission update → rounding → custody → collect. Check over-crediting, underpayment, or stranded funds.
- **A5 Admin perimeter:** capability → ACL role → version check → state change. Check for inconsistent authorization.
- **A6 Deployment drift:** published package metadata → source manifest → lockfile. Check identity and configuration mismatch.

## Color key

- **Green** — asset custody, rewards, or accounting value.
- **Gold** — capabilities, administration, fee controls, and flash repayment obligations.
- **Cyan** — configuration, oracle, and tick machinery.
- **Purple** — positions and version controls.
- **Blue** — token reserves and ordinary authorized flow.
- **Red** — alarms, assertions, and security boundaries.
- **Paper** — evidence, deployment metadata, or investigation hypotheses.
- **Dashed colored routes** — scenario traces.
- **Dashed white route** — clean baseline control trace.

## Scope note

The board groups related Move structs, fields, modules, events, and transitions into visual rooms so they can be planned on one map. It does not claim that every event struct is a separate stored object, and it does not depict a real-world bank or physical attack plan. It is a fictional, local protocol-security review artifact.
