# Market 2941850: question for MiroFish (do NOT pass Polymarket price)

**Prediction requirement (English, paste into MiroFish):**

As of October 24, 2026, the Bank of Canada's target for the overnight rate is 2.25%, the level it has held at seven consecutive decisions since its last change on October 29, 2025. Will the Bank of Canada leave the target for the overnight rate unchanged at its scheduled interest rate announcement on Wednesday, October 28, 2026 (9:45 a.m. Eastern Time)? The answer is YES only if the target is still exactly 2.25% after that announcement; any increase or any decrease of any size (for example to 2.50% or 2.00%, or even a 10 basis-point move, which the rules round to 25 basis points) counts as NO. If the announcement is postponed but still made before the next scheduled decision on December 9, 2026, that postponed decision counts; if it is cancelled or no decision is made before December 9, 2026, the outcome counts as YES, and any emergency move outside the October 28 announcement is ignored. Give the probability (0-100) that the Bank of Canada makes no change to the target for the overnight rate at its October 28, 2026 announcement.

**Resolution rule (Polymarket, gamma API, market 2941850):**

- The market resolves on the change, in basis points, of the Bank of Canada's target for the overnight rate resulting from the October 2026 announcement, relative to the level just before it (2.25%).
- Source: official Bank of Canada information, including the statement / release of the announcement scheduled for October 28, 2026 (calendar: https://www.bankofcanada.ca/core-functions/monetary-policy/key-interest-rate/#target-dates). It may resolve as soon as that release is published.
- If the rate is defined by upper and lower bounds, the upper bound is used (not applicable in practice: the Bank sets a single target).
- Rounding: changes under 25 bps are rounded to 25 bps; changes above 25 bps are rounded to the nearest 25 bps, ties away from zero (37.5 bps -> 50 bps). "Increase" / "Decrease" options include moves of any size. So "No change" (YES of this market) = exactly 0 bps.
- Postponed to a time before the start of the next scheduled announcement (December 9, 2026) -> resolves on the postponed announcement. Cancelled, or no decision by the start of the next scheduled announcement -> resolves to "No Change".
- Emergency changes not resulting from the specified announcement are not considered.
- Gamma end date: 2026-10-28T00:00:00Z (before the 9:45 ET announcement; actual resolution follows the release).
