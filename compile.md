# Compiling OHLCFibExt

Run in **Command Prompt** from the project root (`ohlc-fib-extensions`).

## Layout

```
ohlc-fib-extensions/
├── jdk-26.0.2.1+1/
├── out/                 <- compiled classes and jar
├── mwave_sdk.jar
├── OHLCFibExt.java
├── README.md
└── compile.md
```

## Commands

```bat
"jdk-26.0.2.1+1\bin\javac.exe" -cp "mwave_sdk.jar" -d out OHLCFibExt.java
cd out
"..\jdk-26.0.2.1+1\bin\jar.exe" cf OHLCFibExt.jar com
cd ..
```

Result: `out\OHLCFibExt.jar`.

Notes:

- The file declares `package com.motivewave.platform.study.overlay;`, so classes are written to `out\com\motivewave\platform\study\overlay\`. The jar is built from the `com` folder.
- No `nls` copy step is needed (labels are plain strings).
- Add `out/` and `*.jar` to `.gitignore` so build output isn't committed.

## Install

1. Copy `out\OHLCFibExt.jar` into MotiveWave's Extensions folder.
2. Restart MotiveWave.
3. The study is under the **Custom** menu as **OHLC Fib Extensions**. Add it twice (IVB 30 min, IB 60 min).

## Troubleshooting

| Problem | Fix |
|---|---|
| `package ... does not exist` for `DataContextImpl` or `DOMNote` | They come from MotiveWave's application jar, not the SDK jar. Use `-cp "mwave_sdk.jar;C:\path\to\MotiveWave\lib\*"`. |
| `cannot find symbol` on `getDouble` or `DoubleDescriptor` | SDK version differs. Send me the exact error. |
| `UnsupportedClassVersionError` in MotiveWave | Add `--release 17` to the javac command. |
| Old jar still loaded | Delete the old jar from the Extensions folder and restart MotiveWave. |
