# ozone222 — Far-UVC Ozone vs. Ventilation Calculator

A single-page calculator for one question: **how many outdoor-air changes per hour (ACH) keep the ozone *added* by ceiling-mounted 222 nm (far-UVC) modules at or below a target?** It shows the answer for 1 to N modules in a room of given length, width and height.

**Live calculator:** https://tomphyzx.github.io/ozone222/

Or open `index.html` in any browser. There's no build step and nothing to install.

## Model

- **Ozone generation.** O₂ absorbs weakly at 222 nm. Each absorbed photon gives 2 O₃:
  `G = 2 · σ_O2 · [O2] · (photon rate) · L / V`
  with σ_O2(222 nm) = 4.09×10⁻²⁴ cm², at 25 °C and 1 atm. L is the mean optical path, taken as ceiling height × a path-length factor.
- **Steady state in a well-mixed room:**
  `ΔO3 = G / (ACH + k_dep + k_254)`, so `ACH_required = G/target − k_dep − k_254`
- **Optional upper-room 254 nm removal:**
  `k_254 = Φ · σ_O3(254) · (photon rate) · L_254 / V`
  with σ_O3 = 1.13×10⁻¹⁷ cm². Φ ≈ 0.1–0.3 is the *net* loss yield, because most O(¹D) is quenched and re-forms O₃.

## Defaults

| Input | Default | Notes |
|---|---|---|
| Room | 16 × 14 × 9 ft | Typical single-patient room |
| Room outdoor-air ACH | 2 | ASHRAE 170 patient-room minimum |
| Module | Ushio Care222 B1, 0.11 W | Estimated from 11.2 µW/cm² on-axis at 1 m with a 60° beam |
| | Care222 B1.5, 0.05 W | Estimated from 1.6 µW/cm² at 1 m with a 110° beam |
| Path-length factor | 1.05 (B1), 1.25 (B1.5) | Mean optical path ÷ ceiling height |
| Duty cycle | 100% | |
| Target | 4 ppb | 5 ppb limit minus a 1 ppb margin |
| Surface deposition | 1 h⁻¹ | Set to 0 for the most conservative result |

## Limits

- The ACH means **outdoor** air. Recirculated air doesn't remove ozone unless it passes activated carbon.
- Results are ozone *added* above the outdoor background.
- The gas is treated as optically thin, light is absorbed at the room surfaces, and the room is well mixed.
- Module outputs are estimates. Use measured or manufacturer total-output values if you have them.
- The tool doesn't evaluate occupant UV exposure limits (ACGIH TLVs).
- It's not a substitute for measurement.

## References

- Peng, Z. et al. "Significant Production of Ozone from Germicidal UV Lights at 222 nm." *Environ. Sci. Technol. Lett.* 10, 668–674 (2023).
- Link, M. F. et al. (NIST). "Ozone Generation from a Germicidal Ultraviolet Lamp with Peak Emission at 222 nm." *Environ. Sci. Technol. Lett.* 10(8), 675–679 (2023). doi:10.1021/acs.estlett.3c00318
- Barber, V. P. et al. "Indoor Air Quality Implications of Germicidal 222 nm Light." *Environ. Sci. Technol.* 57, 15990 (2023).
- Ushio Care222 module technical data sheet.

## License

MIT — see `LICENSE`. © 2026 tomPhyzx LLC.
