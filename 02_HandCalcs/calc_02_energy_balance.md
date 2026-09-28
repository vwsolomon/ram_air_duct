# Calc 02: Energy Balance

**Project:** Ram-Air Duct | **Author:** Vernon Solomon | **Date:** 2026-09-27 | **Rev:** A
**Feeds:** Step 3 (heat exchanger core sizing)

## Purpose
Find the coolant and air mass flows needed to reject 10 kW, the heat
capacity rates of each stream, and which air temperature rises satisfy
the core frontal area constraint.

## Nomenclature
- Subscript h = hot fluid (coolant); c = cold fluid (air); i = inlet; o = outlet
- ΔT_h = T_h,i − T_h,o (coolant temperature change)
- ΔT_c = T_c,o − T_c,i (air temperature change)
- C = ṁ · c_p (heat capacity rate, W/K)
- ITD = T_h,i − T_c,i

## Inputs
| Input | Value | Source |
|---|---|---|
| Q | 10,000 W | Design case §2 |
| T_h,i / T_h,o | 70 / 60 °C | Design case §3 |
| ΔT_h | 10 °C | Design case §3 |
| T_c,i | 25.1 °C | Calc 01 (climb) |
| ρ_air | 0.985 kg/m³ | Calc 01 (climb) |
| ρV (inlet mass flux) | 38.0 kg/(m²·s) | Calc 01 (climb) |
| Face velocity at core | 8 m/s (assumed) | Typical value; refine in Step 3 |
| Core frontal area limit | 0.10 m² | Design case §6 |

## Properties
| Fluid | c_p | ρ | Evaluated at |
|---|---|---|---|
| 50/50 EG–water | 3,500 J/(kg·K) | 1,045 kg/m³ | 65 °C (mean) |
| Air | 1,005 J/(kg·K) | 0.985 kg/m³ | Climb condition |

## Equations
1. ṁ = Q / (c_p · ΔT)
2. V̇ = ṁ / ρ
3. C = ṁ · c_p
4. A_inlet = ṁ_c / (ρV)
5. A_fr = ṁ_c / (ρ · V_face)
6. ε = ΔT_c / ITD (valid when air is C_min)

## Calculation: coolant side
1. ṁ_h = 10,000 / (3,500 × 10) = 0.286 kg/s
2. V̇_h = 0.286 / 1,045 = 2.73×10⁻⁴ m³/s = 16.4 L/min = 4.3 gpm
3. C_h = 0.286 × 3,500 = 1,000 W/K

## Calculation: air side sweep
ρ · V_face = 0.985 × 8 = 7.88 kg/(m²·s)

| ΔT_c (°C) | ṁ_c (kg/s) | C_c (W/K) | A_inlet (m²) | A_fr (m²) | ≤ 0.10 m²? | ε |
|---|---|---|---|---|---|---|
| 10 | 0.995 | 1,000 | 0.026 | 0.126 | ✗ | 0.22 |
| 15 | 0.663 | 667 | 0.017 | 0.084 | ✓ | 0.33 |
| 20 | 0.498 | 500 | 0.013 | 0.063 | ✓ | 0.45 |
| 25 | 0.398 | 400 | 0.010 | 0.051 | ✓ | 0.56 |

Constraint boundary: ṁ_c,max = 0.10 × 7.88 = 0.788 kg/s
→ ΔT_c,min = 10,000 / (1,005 × 0.788) = 12.6 °C

## Sensitivity: ΔT_h = 5 °C instead of 10 °C
| Quantity | ΔT_h = 10 °C | ΔT_h = 5 °C |
|---|---|---|
| ṁ_h | 0.286 kg/s | 0.571 kg/s |
| V̇_h | 16.4 L/min | 32.8 L/min |
| C_h | 1,000 W/K | 2,000 W/K |
| T_h,i | 70 °C | 65 °C |
| Δp (∝ ṁ²) | 35 kPa | ~140 kPa (exceeds limit) |
| Pump power (η = 0.5) | ~19 W | ~153 W |
| HX area (∝ 1/ΔT_mean, ΔT_c = 20 °C) | baseline | ~+9% |

## Checks
- Every air case: ṁ_c × 1,005 × ΔT_c = 10,000 W ✓
- Area ratio A_fr / A_inlet = 0.063 / 0.013 = 4.8 = velocity ratio 38.6 / 8 ✓ (mass conservation)
- ΔT_c < ITD (44.9 °C) in all cases ✓ (air cannot exceed coolant inlet temperature)

## Results
- Coolant: ṁ_h = 0.286 kg/s (16.4 L/min), C_h = 1,000 W/K
- Air is C_min for ΔT_c > 10 °C
- Frontal area constraint requires ΔT_c ≥ 12.6 °C
- Carry ΔT_c = 15–25 °C into Step 3; baseline ΔT_c = 20 °C
- Keep ΔT_h = 10 °C baseline (5 °C violates the pressure drop limit)

## Assumptions
- Steady state; properties constant at mean temperatures
- Air density unchanged from inlet to core face (small pressure recovery ignored)
- Pressure drop scales with ṁ² (turbulent flow, same hardware)