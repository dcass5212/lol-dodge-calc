# lol-dodge-engine

**How much reaction-time slack does each boot tier actually buy you?**

An interactive skillshot-dodge calculator and Python model built on the [League of Legends movement-speed formula](https://wiki.leagueoflegends.com/en-us/Movement_speed).

[**→ Live demo**](https://dcass5212.github.io/lol-dodge-calc)

\---

## What it does

For a linear, non-tracking skillshot aimed at your center, the optimal dodge direction is perpendicular to the missile path. You escape if your lateral displacement exceeds the combined hitbox radius `S = r\_champion + r\_skillshot` before the missile arrives.

The **dodge window** — the maximum reaction time that still lets you escape — is:

```
W(v) = (cast\_delay + distance / missile\_speed) − S / v
```

where `v` is your effective move speed after LoL's full formula: flat bonuses → additive % → slow × (1 − slow\_resist) → soft caps.

The marginal value of move speed is `dW/dv = S / v²` — always positive, always diminishing. Your first boots buy more window than each tier upgrade, and a slow collapses your window far faster than +20 MS rebuilds it.

## Scope and assumptions

This model applies to **linear, non-tracking skillshots** (Blitzcrank Q, Morgana Q, Ezreal Q, etc.). It does not cover:

* Tracking / homing skillshots
* Cones, circles, or point-and-click abilities
* Diagonal or angled dodge paths (the model assumes optimal perpendicular movement)
* Move-speed items or runes beyond boots (easily extended via `additive\_ms\_pct` / `multiplicative\_ms\_pcts` in the Python API)

## Quick start — demo

Open `index.html` in any browser. No server, no build step.

\---

## Data sources

Boot values (flat MS, slow resist) from the current SR table on the [movement-speed wiki page](https://wiki.leagueoflegends.com/en-us/Movement_speed).  
When a patch changes values, edit `\_BOOT\_LIST` in `dodge\_model.py` and the `BOOTS` array in `index.html`.

\---

## License

MIT. Not affiliated with or endorsed by Riot Games. League of Legends is a trademark of Riot Games, Inc.

