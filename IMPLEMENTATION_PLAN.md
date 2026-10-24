# Implementation Plan: Articulatory & Vocal Tract Geometry

Generates exhaustive Articulatory & Vocal Tract Geometry reports modeling estimated vocal tract length (VTL cm), pharyngeal volume, velopharyngeal port dynamics, larynx height, lip protrusion, and cross-sectional area functions for physical and parametric synthesis.

---

## Deliverables Checklist

### v1.0.0 — Initial Release
- [x] **Vocal Tract Length (VTL) Estimator**: Formant dispersion formula $L = c / (2 \cdot \Delta F)$ and warping scalar calculation relative to 17.0 cm reference. ✅ done in v1.0.0
- [x] **Lip Geometry & Labial Aperture Model**: Neutral, spread, and rounded aperture areas ($\text{cm}^2$) and protrusion bias (mm). ✅ done in v1.0.0
- [x] **Velopharyngeal Port & Nasal Coupling**: Coupling area ($\text{mm}^2$), nasal resonance pole ($F_N$ ~250–450 Hz), and antiformant zero ($Z_N$ ~500–1800 Hz). ✅ done in v1.0.0
- [x] **Vertical Larynx Mobility Model**: Resting larynx height baseline and dynamic excursion ($\pm\text{mm}$) during pitch peaks. ✅ done in v1.0.0
- [x] **Machine-Readable JSON Schema**: Standardized `vocal_tract_geometry.json` output block. ✅ done in v1.0.0
- [x] **Tri-Platform Accessibility**: Canonical `.agents` installation linked to Claude, Grok, and Antigravity via NTFS junctions. ✅ done in v1.0.0
- [x] **Standard Documentation Suite**: `SKILL.md`, `HOW_TO_USE.txt`, `README.md`, `App Changes Tracker.html`, and `dev-notes-v1.0.0.md`. ✅ done in v1.0.0

---

## Roadmap & Future Enhancements

### v1.1.0 — 1D Tube / Area Function Generator
- [ ] Export 44-section vocal tract cross-sectional area functions ($A(x)$ in $\text{cm}^2$) compatible with Pink Trombone and VocalTractLab.
- [ ] Acoustic impedance matching at the lips.
- [ ] Automated integration with Praat script formant extraction.
