# AI swarm vs Polymarket: MiroFish on Claude Opus 5.5

Forecasts from the open-source [MiroFish](https://github.com/666ghj/MiroFish) AI swarm, running on Claude Opus 5.5, Sonnet 5.5
and Haiku 5.5, on four live Polymarket markets. Every forecast here was made **before** the market resolved. We will add the
outcomes and score every source after resolution.

By [OrcaLayer](https://orcalayer.com), a public analytics layer for Polymarket. Round one, with five cheap models, is written up
in [MiroFish on Polymarket: Can an AI Swarm of LLM Agents Forecast?](https://orcalayer.com/blog/mirofish-ai-swarm-polymarket-experiment).

## The forecasts (round 2, locked October 24-25, 2026)

Probability of YES, in %.

| Source | Toronto | Likud | Bank of Canada | US x Iran |
|---|---|---|---|---|
| Polymarket at the snapshot | 65.5 | 30.5 | 18.7 | 82.5 |
| OrcaLayer Smart Money, wallets on YES | 47.7 | 24.9 | 39.3 | 67.1 |
| OrcaLayer Smart Money, money on YES | 86.8 | 29.4 | 96.5 | 93.7 |
| Opus 5.5, asked directly (median of 5) | 49 | 38 | 45 | 84 |
| Sonnet 5.5, asked directly (median of 5) | 52 | 30 | 50 | 80 |
| Haiku 5.5, asked directly (median of 5) | 48 | 33 | 45 | 80 |
| Swarm on Opus 5.5 (median agent) | 52 | 40 | 45 | 85.5 |
| Swarm on Sonnet 5.5 (median agent) | 50 | | 49.5 | |
| Swarm on Haiku 5.5 (median agent) | 50 | 25 | 55 | 78 |
| MiroFish report agent, Opus swarm | 60 | 40 | 89 | 74 |

| Market | YES means | Snapshot (UTC) | Resolves |
|---|---|---|---|
| [toronto-mayor-chow](round2/toronto-mayor-chow) | Olivia Chow wins the Toronto mayoral election | Oct 24 10:46 | Oct 26 election |
| [israel-likud-most-seats](round2/israel-likud-most-seats) | Likud's own list wins the most Knesset seats in the October 27 election | Oct 24 11:29 | Oct 27 election |
| [bank-of-canada-hold-oct-28](round2/bank-of-canada-hold-oct-28) | The overnight rate stays at 2.25% (any move is NO) | Oct 24 11:57 | Oct 28, 9:45 AM ET |
| [us-iran-no-strike-oct-31](round2/us-iran-no-strike-oct-31) | No qualifying US air or missile strike hits Iranian territory (ground raids, naval gunfire and intercepted munitions don't count) | Oct 25 09:56 | Oct 31, 11:59 PM Iran time |

All numbers in machine-readable form: [`forecasts.csv`](forecasts.csv). Costs: [`costs.csv`](costs.csv).

Smart Money figures describe positioning (the share of OrcaLayer's smart wallets, or of their invested money, holding YES), not a
probability. See the [methodology](https://orcalayer.com/methodology#smart).

## How the swarm was run

- **Engine.** MiroFish at commit `7657031`, Reddit-style feed only (CAMEL-AI OASIS), 25 rounds, at most one action per agent per
  round. Isolated container, no access to OrcaLayer's database, only public information.
- **World building.** For each market Claude Opus 5.5 built the knowledge graph from the seed files, generated one persona per
  entity (34 to 56 agents) and wrote the simulation setup, once.
- **Same personas, three models.** On those personas and opening posts the swarm ran with every agent on Opus 5.5, then on Haiku
  5.5, and on two markets on Sonnet 5.5. One run per configuration.
- **Polling.** After each run every agent got the exact question (`prompt_interview.txt`): today's date, the deadline and the
  Polymarket rule for YES, and answered `PROBABILITY_YES` (0 to 100), then YES or NO, then one sentence. The swarm number is the
  median agent. MiroFish's report agent was asked the same question separately (`prompt_chat.txt`).
- **Direct baseline.** Each model got the same question and the same seed files in one prompt, five times (`direct/`).
- **Seeds.** Written from public reporting up to October 24, 2026, with a date in every sentence. No prediction-market prices and
  no forecast-model probabilities; polls, official data and statements are included. `seed/` is what we wrote (with sources);
  `seed_as_fed/` is what MiroFish received. For Toronto and Likud the two are identical; for the Bank of Canada and Iran the
  `Sources:` line was removed before feeding, after the persona generator turned source lists into "cited in research documents"
  on Likud.
- **Model API.** Anthropic Messages API with prompt caching, through a small proxy that priced every call and enforced a hard
  budget stop.

## Hand corrections (read this before reusing the data)

Even on Opus 5.5, MiroFish's persona generator wrote factual errors that contradicted the seed files, some aimed straight at the
question: a wrong election date, a preferred-PM poll with the leader reversed, the Bank of Canada confused with the Federal
Reserve, a mayoral campaign for a person who was not running. Every persona was checked against the seeds by a second model
(`persona_check.json`) and by hand before the runs.

- `persona_fixes_applied.json`: every corrected sentence, old and new text, and why. Toronto 13 (one persona replaced as a whole),
  Likud 46, Bank of Canada 37, Iran 31.
- `config_fixes_applied.json`: sentences removed from the simulation's narrative setup because they stated a verdict
  ("leave a slight edge to Chow", "the narrative should drift toward cautious confidence that the pause holds").
- `removed_opening_posts.json`: opening posts removed because of wrong facts, swapped voices or a ready-made verdict, with the
  original text and the reason. Toronto 2, Likud 1, Bank of Canada 2, Iran 6.

An uncorrected swarm would have behaved differently.

## Files per market

```
round2/<market>/
  question.md, polymarket_rules.md   the question as asked and the Polymarket rule, verbatim
  requirement.txt, prompt_*.txt       exact texts sent to MiroFish and to the agents
  seed/, seed_as_fed/                 input documents
  snapshot.json                       Polymarket price and OrcaLayer Smart Money shares at the snapshot
  persona_check.json                  automatic check of the generated personas
  persona_fixes_applied.json          hand corrections, config_fixes_applied.json: removed narrative sentences
  removed_opening_posts.json          opening posts removed before the runs, with the reason
  runs/<model>_interview_parsed.json  every agent's answer
  runs/<model>_posts.json             what the agents posted
  runs/<model>_report.md, _chat.json  MiroFish's report and its report agent's answer
  direct/direct_<model>.json          five direct answers per model, with reasoning
```

## Costs

Round 2 cost $98.56 in API fees: preparation and persona generation on Opus, persona checks on Sonnet, ten swarm runs and sixty
direct answers. One swarm run on Opus 5.5 cost $13.6 to $24.0; five direct Opus answers cost $0.12 to $0.14 in total. Details in
[`costs.csv`](costs.csv).

## Limitations

- Eight markets across two rounds are an illustration, not a statistic.
- One run per configuration. In round one, repeat runs of the same setup moved the median by up to 10 points.
- The swarm knows only its seed files and has no internet access.

## License

Data and texts: [CC BY 4.0](LICENSE). Cite as "OrcaLayer, AI swarm vs Polymarket, 2026".
