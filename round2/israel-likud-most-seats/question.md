# Market 2100981: question for MiroFish (do NOT pass Polymarket price)

**Prediction requirement (English, paste into MiroFish):**

As of October 24, 2026, Israel's general election for the 26th Knesset is scheduled for Tuesday, October 27, 2026, polls close at 22:00 local time, and no new opinion polls may be published before then. Will Likud, the candidate list led by Benjamin Netanyahu (which also carries New Hope candidates), win more Knesset seats than any other single party or joint candidate list in this election, for example Gadi Eisenkot's Yashar or Naftali Bennett's Together? It counts as YES only if the Likud list's own seat total is the highest; if two lists tie on seats, the list with more valid votes wins the tie, and if that is also tied, alphabetical order decides. Bloc totals, the coalition that later governs, the person asked to form a government and election-night exit polls do NOT count, and if the results are not definitively known by June 30, 2027, the answer is NO. The outcome is taken from a consensus of credible reporting, or from the official results of Israel's Central Elections Committee if there is any ambiguity. Give the probability (0-100) that Likud wins the most seats in the October 27, 2026 Knesset election.

**Resolution rule (Polymarket, gamma API, market 2100981):**

- The election is expected on October 27, 2026; the market end date is 2026-10-28T03:59:00Z.
- The market resolves to the party or coalition (candidate list) that wins the most Knesset seats in this election. Only the seat count of the named list counts.
- Tie on seats: the list with more valid votes wins. If that is also tied, the listed name that comes first alphabetically wins.
- Source: a consensus of credible reporting. If there is ambiguity, the official results of the Central Elections Committee (https://www.gov.il/en/departments/central-elections-committee/govil-landing-page) decide.
- If the results are not definitively known by June 30, 2027, 11:59 PM ET, the market resolves "Other", so Likud = NO.
- Mergers: if Likud or Together (or a successor created by merger) merges with or runs jointly with another party, the Likud or Together option represents the resulting list. Likud filed its own list on September 8, 2026, with New Hope candidates on the slate, so the Likud option = the "Likud under the leadership of Benjamin Netanyahu" list.
- Other mergers and splits: a listed party running jointly with unlisted parties takes all the joint list's seats; a joint list of two listed parties goes to the party with more seats in the previous Knesset, and otherwise to the one first alphabetically. In a split, the option goes to the successor with the most seats.
