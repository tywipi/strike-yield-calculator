[README.md](https://github.com/user-attachments/files/28865749/README.md)
# ⚡ STRIKE Yield Calculator

> How rich do you want to **$STRIKE** it? 🟢

A community-built, real-yield calculator for [Strike Finance](https://app.strikefinance.org) staking on Cardano. Enter your STRIKE holdings, drag the volume slider, and see what the protocol pays you — from **new kicks 👟 to yacht money 🛥️**.

**Live demo:** https://tywipi.github.io/strike-yield-calculator/

<!-- Add a screenshot: docs/screenshot.png -->
<!-- ![Screenshot](docs/screenshot.png) -->

## What it does

- **Live protocol data** — pulls cumulative volume, revenue, and recent daily pace directly from the Strike Statistics API (falls back to a static snapshot if offline)
- **Yield calculator** — daily / monthly / annual USDM yield for any position size at any volume scenario
- **Levels of Rich ladder** — how many STRIKE you need for each lifestyle's annual yield; rungs light up when your holdings clear them
- **Scenario table** — yield per 1,000 STRIKE at every milestone from today to top-10 perp DEX territory
- **No black box** — the full formula and every assumption is printed on the page

## The formula

```
Annual yield = Daily Volume × 365
             × Net Fee Rate
             × ( Your STRIKE ÷ Total Staked )

Net Fee Rate = Tiered taker fee − Maker rebate
             (compresses from ~0.035% → ~0.024% as volume scales)
```

### Assumptions (all stated, all challengeable)

| Input | Value | Source |
|---|---|---|
| Blended fee rate | 0.03554% | Confirmed: all-time revenue ÷ all-time volume from the dashboard |
| Fee compression | 0.036% → 0.028% taker | [docs.strikefinance.org](https://docs.strikefinance.org) fee tiers (Tier 0–6) |
| Maker rebates | up to −0.010% | Strike maker rebate tiers, subtracted from net fee at scale |
| Staking participation | 84.5% of circulating supply | Static — not yet exposed in the public API |
| Scope | **V2 only** | V1 revenue exists and pays stakers too; excluding it keeps the model conservative |

**Known unknown:** staked-STRIKE fee discounts may further compress staker revenue. Not yet confirmed — treat the numbers as a pre-discount baseline.

## Data sources

Strike Perpetuals Statistics API (public, cached ~3 min):

- `GET https://api.strikefinance.org/stat/v1/dashboard/summary` — totals
- `GET https://api.strikefinance.org/stat/v1/dashboard/volumes` — daily volume series (current pace = 7-day average)

## Run it locally

It's one HTML file. No build step, no dependencies.

```bash
git clone https://github.com/tywipi/strike-yield-calculator.git
cd strike-yield-calculator
open index.html        # or just double-click it
```

To deploy your own: fork → Settings → Pages → deploy from `main`.

## Contributing

Fork it, improve it, verify the math. PRs welcome — especially:

- [ ] On-chain staking participation via Koios/Blockfrost (replace the static 84.5%)
- [ ] Live STRIKE price feed for the ROI-on-cost figures
- [ ] V1 revenue as an optional "bonus yield" toggle
- [ ] Confirmation of how staked-STRIKE fee discounts affect the staker pool

If you find an error in the model, **open an issue** — getting the math right matters more than the numbers being big.

## ⚠️ Disclaimer

This tool is for **educational purposes only**. Nothing here is financial advice. Yield projections are models, not promises — they fluctuate with volume, staking participation, and fee structure changes. Past performance ≠ future results. Crypto is risky. **DYOR** — never invest more than you can afford to lose.

This is an independent community project, not affiliated with or endorsed by Strike Finance.

## License

[MIT](LICENSE) — the code is free to use. The disclaimer above still applies to the content.

---

Built by an Elite Striker 🟢 · [Follow me on X](https://x.com/tywipi) · `$STRIKE` `$ADA` #Cardano
