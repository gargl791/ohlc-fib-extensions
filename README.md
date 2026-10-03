# OHLC-fib-extensions

A custom [MotiveWave](https://www.motivewave.com) overlay study that extends the built-in **OHLC** study with Fibonacci extensions of the opening range.

## What it does

The original OHLC study plots the day's open, high, low, previous close, overnight levels and an **opening range** (high/low of the first N minutes or seconds of the session).

This study keeps all of that and adds up to **3 Fibonacci extensions** projected from the opening range:

- Upper level = `ORH + (ORH - ORL) * ratio`
- Lower level = `ORL - (ORH - ORL) * ratio`

Each extension slot has:

- An editable ratio (defaults 0.5, 1.0, 1.5)
- Its own upper and lower line, each with enable toggle, color, width and dash style
- Labels such as `ORH+1:` and `ORL-1:`

Levels update live while the opening range forms.

### Intended use

Add the study **twice** to a chart, each with its own opening range:

| Instance | Opening range |
|---|---|
| IVB | 30 minutes |
| IB | 60 minutes |

## Repository contents

| Item | Description |
|---|---|
| `OHLCFibExt.java` | The new study (id `OHLC_FIB_EXT`, menu: Custom, name: OHLC Fib Extensions). Built from `OHLC.java`. |
| `OHLC.java` | Original MotiveWave OHLC study, kept for reference. |
| `CustomOHLC.java` | Earlier fork of OHLC with 5 extra opening-range slots. It contains no Fibonacci code and has known bugs (e.g. `range4` never assigned, `rHigh_1`/`rHigh_2` mixed up in the tick code). Kept for reference only. |
| `compile.md` | Step-by-step build and install instructions. |
| MotiveWave SDK jar(s) | Compile-time dependencies. |
| `jdk-26.0.2.1+1/` | Local JDK used to compile. |
