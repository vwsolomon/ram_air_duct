# Design Case: Ram-Air Cooling Duct and Heat Exchanger

**Author:** Vernon Solomon
**Date:** 2026-09-26
**Revision:** A

## 1. Purpose
Size a ram-air duct and heat exchanger that rejects the drivetrain heat
load of a small hybrid-electric aircraft, and quantify the cooling drag.

## 2. Heat load
| Item | Value | Rationale |
|---|---|---|
| Heat to reject | 10 kW, continuous | ~150 kW electric drivetrain at ~93% combined motor/inverter efficiency |
| Duty | Steady state | Worst case is sustained climb power |

## 3. Coolant loop
| Item | Value | Rationale |
|---|---|---|
| Coolant | 50/50 ethylene glycol–water | Freeze protection at altitude |
| Max temperature entering electronics | 60 °C | Typical power-electronics coolant limit |
| Coolant temperature rise across electronics | 10 °C | Starting assumption; revisit in Step 2 |
| Coolant into heat exchanger | 70 °C | 60 °C + 10 °C rise |
| Coolant out of heat exchanger | 60 °C | Must meet electronics inlet limit |
| Max coolant-side pressure drop across HX | 35 kPa | Keeps pump small; starting assumption |
| Coolant flow | 0.286 kg/s (16.4 L/min) | From Calc 02 |

## 4. Sizing condition: hot-day climb
| Item | Value |
|---|---|
| Airspeed | 75 KTAS = 38.6 m/s |
| Pressure altitude | 5,000 ft |
| Temperature | ISA + 20 °C = 25.1 °C (298.3 K) |
| Static pressure | 84.3 kPa |
| Air density | 0.985 kg/m³ |

## 5. Check condition: cruise
| Item | Value |
|---|---|
| Airspeed | 120 KTAS = 61.7 m/s |
| Pressure altitude | 8,000 ft |
| Temperature | ISA + 20 °C = 19.2 °C (292.3 K) |
| Static pressure | 75.3 kPa |
| Air density | 0.897 kg/m³ |

## 5a. Derived quantities
| Quantity | Climb | Cruise | Meaning |
|---|---|---|---|
| Mass flux ρV | 38.0 kg/(m²·s) | 55.4 kg/(m²·s) | Air per m² of inlet |
| Dynamic pressure q = ½ρV² | 733 Pa | 1,710 Pa | Push available to drive air through the core |
| ITD (70 °C − air temp) | 44.9 °C | 50.8 °C | Temperature difference driving heat transfer |

Conclusion: climb has less push, less airflow, and a smaller ITD,
so hot-day climb is the in-flight sizing case.
Full calculations: [Calc 01](../02_HandCalcs/calc_01_air_properties.md)

## 6. Constraints
- HX core frontal area ≤ 0.10 m² (packaging assumption; revisit after Step 3)
- Diffuser half-angle ≤ 7° to avoid separation

## 7. Assumptions
- Steady state; no heat soak or transients
- Radiation and heat loss from duct walls neglected
- Uniform freestream flow at the duct inlet; no boundary-layer ingestion
  or aircraft installation effects

## 8. Success criteria
- Coolant enters electronics at ≤ 60 °C at the sizing condition
- Cooling drag quantified across the design space (trade plot)
- Hand calculations and CFD agree within about 25%, or the gap is explained

## 9. Open questions
- Ground operations: V = 0, so no ram airflow. Options: fan, prop wash,
  thermal mass with a time limit, or power limits. Evaluate after Step 3.
  - Confirm the 60 °C coolant inlet limit against actual inverter and motor
  datasheets (junction temperature limit minus junction-to-coolant rise).