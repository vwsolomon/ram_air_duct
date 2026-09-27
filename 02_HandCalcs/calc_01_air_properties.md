# Calc 01: Air Properties at Design Conditions

**Project:** Ram-Air Duct | **Author:** Vernon Solomon | **Date:** 2026-09-26 | **Rev:** A
**Feeds:** design_case.md sections 4, 5, 5a

## Purpose
Compute true airspeed, temperature, pressure, density, mass flux, dynamic
pressure, and ITD for the climb (sizing) and cruise (check) conditions.

## Inputs
| Input | Climb | Cruise | Source |
|---|---|---|---|
| Airspeed | 75 KTAS | 120 KTAS | Design case |
| Pressure altitude h | 5,000 ft | 8,000 ft | Design case |
| Temperature offset | ISA + 20 °C | ISA + 20 °C | Design case (hot day) |
| Coolant into HX | 70 °C | 70 °C | Design case section 3 |

## Constants
- 1 kt = 0.5144 m/s
- Sea-level ISA: T₀ = 15 °C, p₀ = 101,325 Pa
- Lapse rate: 1.98 °C per 1,000 ft
- R (air) = 287 J/(kg·K)

## Equations
1. V = KTAS × 0.5144
2. T_ISA = 15 − 1.98 × (h / 1,000); T = T_ISA + 20
3. p = 101,325 × (1 − 6.8756×10⁻⁶ × h)^5.2559   (h in ft)
4. ρ = p / (R · T)   (T in K)
5. Mass flux = ρV
6. q = ½ρV²
7. ITD = T_coolant,in − T_air

## Calculation: climb
1. V = 75 × 0.5144 = 38.58 m/s
2. T_ISA = 15 − 1.98 × 5 = 5.1 °C; T = 25.1 °C = 298.3 K
3. 6.8756×10⁻⁶ × 5,000 = 0.034378
   1 − 0.034378 = 0.965622
   0.965622^5.2559 = 0.83205
   p = 101,325 × 0.83205 = 84,307 Pa
4. ρ = 84,307 / (287 × 298.3) = 0.985 kg/m³
5. ρV = 0.985 × 38.58 = 38.0 kg/(m²·s)
6. q = ½ × 0.985 × 38.58² = ½ × 0.985 × 1,488.4 = 733 Pa
7. ITD = 70 − 25.1 = 44.9 °C

## Calculation: cruise
1. V = 120 × 0.5144 = 61.73 m/s
2. T_ISA = 15 − 1.98 × 8 = −0.8 °C; T = 19.2 °C = 292.3 K
3. 6.8756×10⁻⁶ × 8,000 = 0.055005
   1 − 0.055005 = 0.944995
   0.944995^5.2559 = 0.74278
   p = 101,325 × 0.74278 = 75,262 Pa
4. ρ = 75,262 / (287 × 292.3) = 0.897 kg/m³
5. ρV = 0.897 × 61.73 = 55.4 kg/(m²·s)
6. q = ½ × 0.897 × 61.73² = ½ × 0.897 × 3,810.6 = 1,709 Pa
7. ITD = 70 − 19.2 = 50.8 °C

## Checks
- Pressure rule of thumb (~3.4 kPa per 1,000 ft): 5,000 ft ≈ 84 kPa ✓; 8,000 ft ≈ 74 kPa ✓
- Units: kg/m³ × m²/s² = kg/(m·s²) = Pa ✓
- q ratio: (120/75)² × (0.897/0.985) = 2.33; 1,709/733 = 2.33 ✓
- Hot-day density is 7% below standard-day table value (1.056 at 5,000 ft) ✓ expected

## Results
| Quantity | Climb | Cruise |
|---|---|---|
| V | 38.6 m/s | 61.7 m/s |
| T | 25.1 °C | 19.2 °C |
| p | 84.3 kPa | 75.3 kPa |
| ρ | 0.985 kg/m³ | 0.897 kg/m³ |
| ρV | 38.0 kg/(m²·s) | 55.4 kg/(m²·s) |
| q | 733 Pa | 1,709 Pa |
| ITD | 44.9 °C | 50.8 °C |

## Notes
- Standard atmosphere tables give standard-day density; always compute
  hot-day density from ρ = p/(RT).
- Pressure is unaffected by the temperature offset at fixed pressure altitude.