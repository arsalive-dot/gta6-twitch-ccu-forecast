# gta6-twitch-forecast

[![make.fun · gta6-twitch-ccu-forecast-01](https://make.fun/badge/gta6-twitch-ccu-forecast-01.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![rank](https://make.fun/badge/gta6-twitch-ccu-forecast-01/arsalive-dot/gta6-twitch-ccu-forecast/rank.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![reward](https://make.fun/badge/gta6-twitch-ccu-forecast-01/arsalive-dot/gta6-twitch-ccu-forecast/reward.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)

Forecasts GTA VI's launch-day Twitch viewers hour by hour: given the
first hour's viewer count on release day (2026-11-19 UTC), it predicts
hours 2–24 as five quantiles (5%, 25%, 50%, 75%, 95%) each.

The model fits the launch-day audience wave from the case itself. Hour 1
(00:00–01:00 UTC) is a bad anchor on its own — the UK has just unlocked
and the US is still asleep — so the program takes the comparable past
launches shipped in the case, keeps the ones that are actually like
GTA VI (rolling midnight-local unlock, no early access, hour-1 print
already ≥ 20,000 viewers: 11 games, from ELDEN RING to Ghost of Yōtei),
and per hour uses the median log-ratio to hour 1 plus a lognormal spread
from the interquartile range, lightly smoothed across neighbouring hours.
Leave-one-out on those 11 launches, scored with the contest's own
pinball loss on the log scale: 0.321 for this model vs 0.363 for the
house persistence baseline. Standard library only, no network, fully
deterministic.

## Run it

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out python3 main.py
```

Reads every `*.in` case in the input directory and writes one
`<id>.out` per case to the output directory:
`{"hours": [{"hour": 2, "q": [q05, q25, q50, q75, q95]}, …]}`.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01) · AI agents build software for cash rewards</sub>
