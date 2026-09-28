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

## 2026-09-27
- **Did:** Step 2 energy balance: coolant and air mass flows, heat capacity
  rates, frontal area check, ΔT_h sensitivity. Worked all steps on paper.
  See [Calc 02](../02_HandCalcs/calc_02_energy_balance.md) for full calculations.
- **Broke:** Notation: first labeled the coolant C_c. Fix: textbook convention
  is h = hot (coolant), c = cold (air).
- **Learned:**
  - At steady state, energy in = energy out; any imbalance is stored and
    raises temperature until a new balance forms.
  - Halving ΔT_h doubles flow, roughly quadruples pressure drop, and raises
    pump power about eightfold.
  - Air is C_min, which is why air-cooled heat exchangers are large.
  - The 60 °C coolant limit traces back to semiconductor junction
    temperature minus the junction-to-coolant temperature rise.
- **Next:** Step 3, heat exchanger core sizing (effectiveness-NTU).

### Homework answers
1. At steady state nothing changes with time, so energy in must equal energy
   out. If the coolant gained 10 kW but lost only 8 kW, the extra 2 kW would
   be stored and the temperature would rise until the heat exchanger rejected
   the full 10 kW, possibly above the 60 °C limit.
2. Halving ΔT_h from 10 to 5 °C doubles coolant flow (16.4 → 32.8 L/min).
   The electronics see cooler, more uniform coolant, but pressure drop
   roughly quadruples (violating the 35 kPa limit), pump power rises about
   eightfold, and the heat exchanger needs about 9% more area.
3. At 8 m/s face velocity, the 0.10 m² limit requires ΔT_c ≥ 12.6 °C.
   Larger ΔT_c reduces air flow and frontal area but requires higher
   effectiveness (a deeper, heavier core). The optimum lies between about
   13 and 30 °C, to be found in the trade study.