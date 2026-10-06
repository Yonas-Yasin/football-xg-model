# Expected Goals (xG) Model: World Cup 2022

A logistic regression expected goals model built from scratch with StatsBomb open data, trained on three international tournaments and tested on the unseen 2022 FIFA World Cup.

## Key results

| Model | Log loss ↓ | ROC AUC ↑ | Brier ↓ |
|---|---|---|---|
| Naive baseline | 0.341 | 0.500 | 0.095 |
| **Logistic regression (this project)** | **0.285** | **0.777** | **0.081** |
| Gradient boosting | 0.290 | 0.766 | 0.082 |
| StatsBomb xG (professional benchmark) | 0.267 | 0.815 | 0.076 |

- With only ten features, the model gets most of the way to a professional xG model on out-of-sample data.
- Gradient boosting did not beat logistic regression on this data size, so the simpler, interpretable model was kept.
- Kylian Mbappé was the tournament's standout finisher: 6 non-penalty goals from about 2.9 xG.

## Method

1. **Data:** every shot from World Cup 2018, Euro 2020, Euro 2024 and World Cup 2022 (5,606 non-penalty shots, shootouts excluded).
2. **Features:** distance and angle to goal, header, free kick, first-time shot, one-on-one, open goal, under pressure, counterattack, set piece.
3. **Validation:** tournament-based split. The model is trained on 2018–2024 tournaments other than WC 2022 and evaluated only on WC 2022.
4. **Application:** players ranked by non-penalty goals minus xG (minimum 8 shots).

The full analysis, charts and caveats are in [`xg_model.ipynb`](xg_model.ipynb).

## Run it yourself

```bash
pip install -r requirements.txt
jupyter notebook xg_model.ipynb
```

The first run downloads the data from StatsBomb (a few minutes) and caches it in `data/`.

## Data

[StatsBomb Open Data](https://github.com/statsbomb/open-data), used under StatsBomb's open data terms.
