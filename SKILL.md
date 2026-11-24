---
name: founder-cfo
description: Calculate unit economics, break-even, cash needs and financial scenarios from sourced inputs; not a full business-plan compiler.
argument-hint: "[path to numbers.json]"
---

# Founder CFO

1. Read only CFO-relevant inputs (`founder/numbers.json`, `founder/cfo-readiness.md`, `founder/offer.md`, and BOM/pricing files) rather than loading sibling Founder skills or dumping large archives into context — excess context triggers compaction before modeling runs. Read [example shape](example.json) only when creating or repairing `numbers.json`. Persist sourced prices, FX rates, shipping, and payment/platform fees into `founder/cfo-sources.md` after each small research batch so raw numbers survive context compaction instead of forcing duplicate searches; user quotes outrank public prices, which outrank labelled estimates.
2. Include unit, price, variable costs per unit, monthly fixed costs, startup costs, planned units/day, days/month, 12-month ramp, and capacity when known. Costs use `label`/`cost` objects. Numbers must be finite and nonnegative; days and known capacity must be positive. Preserve an explicit zero sales plan. When the user supplies only a target selling price ceiling and unknown costs or volume, anchor `price` at the ceiling, assemble a bounded sourced variable cost (plus labelled estimates for unquoted overhead/ramp), and derive the max allowable unit cost rather than stalling to price every unchosen variant.
3. Set `currency` (such as `THB`) and keep all money inputs in that currency. The helper labels money; it performs no FX conversion. Its legacy default is `$`. Source any conversion before combining foreign quotes. Label sales/ramp assumptions; simulated interest is not a verified sales forecast.
4. Run:
```bash
python3 "~/.claude/skills/founder-cfo/unit_economics.py" founder/numbers.json --out founder/cfo.md
```
For a what-if, use the same script/input with `--price NUMBER` or `--volume FACTOR`; do not change actual inputs merely to explore a scenario. `--json` returns machine-readable results.
5. Read the output. Add a short note: margin/contribution, limiting cost or assumption, break-even, required cash/payback, capacity limits, and costed improvements. Check any board conditions. Every reported number must match inputs or helper output; revenue is before tax.

Done: `numbers.json`, `cfo.md` and sources agree on assumptions, currency and results. Report errors or missing capacity/demand evidence. retain established prices unless the user explicitly adopts a change. Do not run other Founder skills automatically.
