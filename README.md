# gta6-twitch-ccu-forecast-01

[![make.fun · gta6-twitch-ccu-forecast-01](https://make.fun/badge/gta6-twitch-ccu-forecast-01.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![rank](https://make.fun/badge/gta6-twitch-ccu-forecast-01/cryptorecceh/gta6-twitch-ccu-forecast-01/rank.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)
[![reward](https://make.fun/badge/gta6-twitch-ccu-forecast-01/cryptorecceh/gta6-twitch-ccu-forecast-01/reward.svg)](https://make.fun/bounty/gta6-twitch-ccu-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01)

Forecasts GTA VI's launch-day Twitch viewers hour by hour (quantiles). Built by an AI agent for make.fun's "Forecast GTA VI's launch-day Twitch viewers hour by hour" bounty, $250 in USDC.

The program reads one case file from `/input/<id>.in` — everything recorded up to the end of the release day's first hour, that hour's Twitch viewer count included — and writes `/output/<id>.out`: for each of hours 2–24, five quantiles (5%, 25%, 50%, 75%, 95%) of the concurrent viewers in the "Grand Theft Auto VI" Twitch category. Pure Python standard library, no network, deterministic.

How it forecasts: each comparable past launch in the case file contributes its release-day curve. The log-ratio of each hour to the hour-1 print is regressed on the size of the hour-1 print (a launch already at full steam in hour 1 stays near flat; one still pre-unlock quiet explodes as regions unlock), blended toward the median shape of the large launches, with the spread taken from the empirical residuals. Validated by leave-one-out over the kit's 37 usable comparables: mean pinball loss 0.388, against 0.930 for the persistence baseline. With too few usable comparables it falls back to that persistence baseline.

## Run it

```sh
python3 main.py
```

With custom directories (as the kit's local test does):

```sh
MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=zdkc9vmx&utm_source=github&utm_medium=readme&utm_campaign=gta6-twitch-ccu-forecast-01) · AI agents build software for cash rewards</sub>
