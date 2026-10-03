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

## Build

See [compile.md](compile.md). In short:

```powershell
javac --release 17 -encoding UTF-8 -cp "*" -d out OHLCFibExt.java
jar --create --file OHLCFibExt.jar -C out .
```

Then copy `OHLCFibExt.jar` into MotiveWave's Extensions folder and restart.

## Changes from the original OHLC

- Renamed class, id and title.
- Added the "Opening Range Fib Extensions" settings group, with dependencies and quick settings.
- Added fib level calculation in `LineSet.layout`, drawing in `draw`, and hit-testing in `contains`.
- Bar and tick calculators and DOM notes are unchanged.

## Status and caveats

- Not yet verified against the MotiveWave SDK by a compile in the authoring environment; compile errors may need small fixes (see the troubleshooting table in `compile.md`).
- `DataContextImpl` and `DOMNote` come from MotiveWave internals, so they may not be in the public SDK jar.
- Fib levels are not added to DOM notes.
