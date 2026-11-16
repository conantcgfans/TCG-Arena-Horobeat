# Holobeat TCG - Arena Game Files

A fan-made [TCG Arena](https://tcg-arena.fr) setup for the **Holobeat Card Game** (ホロビートカードゲーム) by Takara Tomy.
Card data comes from the official card list: https://www.takaratomy.co.jp/products/horobeat-cardgame/cardlist/

TCG Arena is a manual table: it doesn't enforce rules. Players resolve battles, damage and triggers themselves.
The in-game help (`customHelp` in `Game_Holobeat.json`) has a condensed rules summary.

## Load into TCG Arena

On [tcg-arena.fr](https://tcg-arena.fr) → **Custom Game** → paste:

```
https://raw.githubusercontent.com/conantcgfans/TCG-Arena-Holobeat/main/Game_Holobeat.json
```

## Update the card list

```bash
cd F:\projects\Holobeat\Scripts
python update_cards.py
```

This scrapes all card-list pages, rebuilds `HolobeatCards.json` and downloads any new images into `Images/`.
Then commit and push `HolobeatCards.json` and `Images/`.

## Files

```
TCG-Arena-Holobeat/
├── Game_Holobeat.json     ← game config (board, deck rules, help text)
├── HolobeatCards.json     ← card database (generated)
├── HolobeatDecks.json     ← sample decks (empty for now)
└── Images/                ← card images (<file_stem>.webp) + CardBack.jpg
```

## Card fields

| Field | Description |
|---|---|
| `id` | Unique per printing, from the image name, e.g. `HB01-033-SEC-02` |
| `name` | Japanese card name. Shared by all printings, so the 4-copy limit counts them together |
| `type` | `Holobito` or `Waza` |
| `color` | `Red` / `Blue` / `Green` |
| `cost`, `power` | Numbers |
| `boost` | `true` if the Holobito has Boost (boost cost/power is only printed on the image) |
| `tribe` | 種族 |
| `keyword` | Double Damage / Barrier / Ena-yomi / Resonance |
| `trigger` | Entry / Over / Draw / Last Over Trigger |
| `package` | Product code, e.g. `HB-BP01`, `HB-SD01`, `PR-HOLOMOTION01` |
| `cardNumber` | Printed number, e.g. `HB01-033` |
| `feature` | Card text (Japanese) |

## Board layout

```
[ Hearts ]  [ Line 1 ][ Line 2 ][ Line 3 ][ Line 4 ][ Line 5 ]
[ Check  ]  [ ─────────────────── Ena ─────────────────────── ]
```

Waza and Boost cards go sideways into the line where they're used. Move them to the graveyard after that line's battle.
