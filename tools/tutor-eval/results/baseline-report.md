# Tutor eval results (baseline)

Run: 2026-10-19T22:20:52.070Z. Questions: 17. Mode: baseline.

- Groundedness (expected atlas facts present in the answer): **1** (gate: 0.75)
- Citation rate (answers naming at least one retrieved source and no unretrieved source; enforcement in scoreAnswer): **1** (gate: 1)
- Correct source rate (cited the subject file the question targets): **1** (gate: 0.75)

| Question | Subject | Facts found | Cited | Correct source | Retrieved from |
|---|---|---|---|---|---|
| chess-openings | chess | 3/3 | yes | yes | chess.js |
| plumbing-drain-slope | plumbing | 3/3 | yes | yes | plumbing.js |
| astronomy-hubble | astronomy | 3/3 | yes | yes | astronomy.js, math.js |
| beekeeping-varroa | beekeeping | 3/3 | yes | yes | beekeeping.js |
| sailing-jibe | sailing | 2/2 | yes | yes | sailing.js |
| knots-three-kinds | knots | 3/3 | yes | yes | knots.js, chemistry.js |
| welding-mig-tig | welding | 3/3 | yes | yes | welding.js |
| gardening-soil | gardening | 3/3 | yes | yes | biology.js, gardening.js |
| bbq-brisket | bbq | 3/3 | yes | yes | cs.js, bbq.js, economics.js |
| survival-priorities | survival | 3/3 | yes | yes | survival.js, hunting.js |
| physics-frameworks | physics | 3/3 | yes | yes | physics.js, math.js |
| geology-basics | geology | 3/3 | yes | yes | geology.js, astronomy.js |
| firstaid-cpr | firstaid | 3/3 | yes | yes | firstaid.js |
| finance-budget | finance | 3/3 | yes | yes | finance.js |
| nutrition-prout | nutrition | 3/3 | yes | yes | nutrition.js, history.js, chemistry.js |
| law-contracts | law | 3/3 | yes | yes | law.js, history.js |
| medicine-harvey | medicine | 3/3 | yes | yes | medicine.js, biology.js |

Baseline mode is an extractive answerer over retrieved atlas passages. It is the floor: any real tutor configuration should beat it, and a drop here means retrieval or content changed for the worse.
