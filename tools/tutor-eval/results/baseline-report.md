# Tutor eval results (baseline)

Run: 2026-10-18T22:26:20.546Z. Questions: 17. Mode: baseline.

- Groundedness (expected atlas facts present in the answer): **0.961** (gate: 0.75)
- Citation rate (answers naming at least one retrieved source and no unretrieved source; enforcement in scoreAnswer): **1** (gate: 1)
- Correct source rate (cited the subject file the question targets): **1** (gate: 0.75)

| Question | Subject | Facts found | Cited | Correct source | Retrieved from |
|---|---|---|---|---|---|
| chess-openings | chess | 3/3 | yes | yes | chess.js |
| plumbing-drain-slope | plumbing | 3/3 | yes | yes | plumbing.js |
| astronomy-hubble | astronomy | 3/3 | yes | yes | astronomy.js, math.js, physics.js |
| beekeeping-varroa | beekeeping | 3/3 | yes | yes | beekeeping.js |
| sailing-jibe | sailing | 2/2 | yes | yes | sailing.js, medicine.js |
| knots-three-kinds | knots | 3/3 | yes | yes | knots.js |
| welding-mig-tig | welding | 3/3 | yes | yes | welding.js |
| gardening-soil | gardening | 3/3 | yes | yes | biology.js, gardening.js |
| bbq-brisket | bbq | 2/3 | yes | yes | cs.js, bbq.js, cooking.js |
| survival-priorities | survival | 3/3 | yes | yes | hunting.js, survival.js |
| physics-frameworks | physics | 3/3 | yes | yes | math.js, physics.js |
| geology-basics | geology | 2/3 | yes | yes | astronomy.js, geology.js |
| firstaid-cpr | firstaid | 3/3 | yes | yes | firstaid.js |
| finance-budget | finance | 3/3 | yes | yes | finance.js, math.js, politics.js |
| nutrition-prout | nutrition | 3/3 | yes | yes | nutrition.js, history.js, chemistry.js |
| law-contracts | law | 3/3 | yes | yes | history.js, law.js, b04-enhance.js, electrical.js |
| medicine-harvey | medicine | 3/3 | yes | yes | medicine.js, biology.js, astronomy.js |

Baseline mode is an extractive answerer over retrieved atlas passages. It is the floor: any real tutor configuration should beat it, and a drop here means retrieval or content changed for the worse.
