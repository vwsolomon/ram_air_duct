# Project Log: Ram-Air Duct

## 2026-09-26
- **Did:** Set up repo and folder structure. Wrote design case (Step 1).
  Calculated air properties for climb and cruise. Answered homework 1–3.
  See [Calc 01](../02_HandCalcs/calc_01_air_properties.md) for full calculations.
- **Broke:** Pressure calculations were off at first. Fix: work the formula
  in four steps and keep 5–6 significant figures until the final answer.
- **Learned:**
  - Hot day hurts twice: lower density and smaller temperature difference (ITD).
  - Table density is standard-day; always calculate ρ = p/(RT) for hot day.
  - Climb has less than half the dynamic pressure of cruise, so climb sizes the core.
  - Ram air gives zero cooling on the ground; ground ops need a separate solution.
- **Next:** Step 2, energy balance (coolant and air mass flow).

### Homework answers
1. Pressure altitude is defined by static pressure, so at a given pressure
   altitude the pressure is fixed; a hot day changes only temperature and
   therefore density.
2. Air is pushed through the heat exchanger by dynamic pressure recovered from
   forward speed. Climb has less than half the dynamic pressure of cruise
   (733 vs 1,710 Pa), so climb sets the core size, while cruise passes excess
   air (and drag) unless the exit area is variable, like cowl flaps.
3. With V = 0, ram-air mass flow is zero, so the duct gives no cooling on the
   ground. A separate method is needed (fan, prop wash, thermal mass with a
   time limit, or power limits), and a hot-day ground hold may be the true
   sizing case.

