# Kipchoge Marathon Biokinesiology Project

Materials for a biokinesiology project on the biomechanics and physiology of Eliud Kipchoge's marathon records.

## Contents

| File | Description |
|---|---|
| `kipchoge_marathon_biokinesiology_report.pdf` | The written report (8 sections plus sources). |
| `kipchoge_races.csv` | Official finish times for three landmark marathons, with derived speed and pace. |
| `model_speed_sweep.csv` | Modeled gait, loading and energy values for speeds from 10 to 22 km/h. |
| `glycogen_curves.csv` | Modeled glycogen remaining by kilometer for four fueling and equipment scenarios. |
| `README.md` | This file. |

An interactive version of the model (animated leg model and race/fuel simulator) accompanies the project as the "Kipchoge Marathon Biomechanics Lab" web page.

## Data provenance

- **Measured / official:** only `kipchoge_races.csv` (race name, date, location, finish time, record eligibility). Speed and pace columns are arithmetic derived from the finish time and the 42,195 m distance.
- **Modeled:** everything in `model_speed_sweep.csv` and `glycogen_curves.csv`. These are estimates from a simplified model, **not measurements of Kipchoge**.

## Column dictionary

### kipchoge_races.csv
`race`, `date` (ISO), `location`, `finish_time_hms`, `finish_time_s`, `avg_speed_m_s`, `avg_speed_km_h`, `pace_min_per_km`, `pace_min_per_mile`, `record_eligible` (yes/no), `notes`.

### model_speed_sweep.csv
| Column | Meaning |
|---|---|
| `speed_km_h`, `speed_m_s` | Running speed |
| `cadence_steps_min` | Fixed at 182 steps/min for the sweep |
| `step_length_m` | Speed divided by step rate |
| `contact_time_ms` | Ground contact time, modeled as 0.30 s - 0.0165 x speed(m/s), floored at 0.14 s |
| `flight_time_ms` | Step time minus contact time |
| `peak_grf_bw` | Peak ground reaction force in body weights, modeled as 1.6 + 0.18 x speed(m/s) |
| `foot_strikes_per_leg` | Marathon distance / step length / 2 |
| `impulse_per_leg_bw_s` | Foot strikes x (0.64 x peak GRF x contact time), a half-sine approximation, in body-weight seconds |
| `finish_time_hms` | Marathon time at that constant speed |
| `energy_kcal_52kg` | About 1 kcal per kg per km x 52 kg x 42.195 km |
| `carb_fraction` | Share of energy from carbohydrate: 0.55 + 0.0275 x (speed - 10 km/h), clamped to 0.55 to 0.90 |
| `carbs_burned_g_52kg` | Energy x carb fraction / 4 kcal per g |

### glycogen_curves.csv
`scenario`, `speed_km_h` (Vienna average), `mass_kg`, `carb_intake_g_h` (absorption capped at 90 g/h in the model), `carbon_shoes` (4% lower energy cost), `drafting` (3% lower energy cost), `km`, `glycogen_g` (starts at 450 g, clamped to 0 to 500 g).

## Key assumptions and limitations

- Energy cost of about 1 kcal per kg per km is a rule of thumb; real running economy varies between athletes.
- The 450 g glycogen store, 4% shoe benefit and 3% drafting benefit are illustrative values informed by the literature (for example Hoogkamer et al., 2018), not individual measurements.
- Gait relationships (contact time, ground force) are linear approximations meant for teaching.
- Cadence is held constant across the sweep; real runners change cadence and step length with speed.
- Validate any figure against primary sources before using it in assessed work.

## Suggested citation

Biokinesiology Project (2026). Kipchoge marathon biomechanics dataset and report. Data derived from official race results plus a simplified teaching model.

## License

Add the license your instructor or institution requires. Official race times are public facts; modeled values are free to reuse with attribution.
