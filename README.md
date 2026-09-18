# NMOS Cascode Current Mirror Random-Mismatch Calculator

A browser-based calculator for estimating random current-matching error in an NMOS cascode current mirror.

## What it calculates

The calculator uses the Pelgrom mismatch model to estimate the local random mismatch between the current-setting transistor **M1** and the mirror transistor **M2**. It reports:

- Nominal output current and nominal current ratio
- Threshold-voltage mismatch, `σ(ΔVTH)`
- Current-factor mismatch, `σ(Δβ/β)`
- Relative and absolute current error at 1σ, 3σ, and 6σ
- Predicted output-current ranges at 3σ and 6σ

## How to use

1. Open `index.html` in any modern web browser.
2. Enter the reference current, M1/M2 dimensions, and the process transconductance parameters.
3. Enter the foundry/PDK mismatch coefficients:
   - `AVt` in mV·µm
   - `Aβ` in %·µm
4. Read the 1σ, 3σ, and 6σ matching results in the result panel.

Use dimensions in µm and current in µA. The two dimensions are entered separately because mismatch depends on device area, `W × L`, while the nominal mirror ratio depends on `W/L`.

## Equations

For independent local mismatch:

```text
σ(ΔVTH) = AVt × sqrt(1/(WM1 LM1) + 1/(WM2 LM2))
σ(Δβ/β) = Aβ × sqrt(1/(WM1 LM1) + 1/(WM2 LM2))
VOV = sqrt(2 IREF / (k'n × WM1/LM1))
σ(ΔI/I) = sqrt((2 σ(ΔVTH)/VOV)^2 + σ(Δβ/β)^2)
```

## Scope and limitations

This is a first-order local random-mismatch estimate for M1 and M2. M3/M4 cascode mismatch, body effect, finite output resistance, output-voltage variation, layout gradients, and PVT behavior are not included. Use foundry PDK models and Monte Carlo simulation for sign-off.
