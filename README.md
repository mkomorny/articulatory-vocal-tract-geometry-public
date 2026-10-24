# Articulatory & Vocal Tract Geometry

> **Tri-Platform Agent Skill** for Claude Desktop / Code, Grok CLI, and Google Antigravity / Gemini.  
> Generates exhaustive Articulatory & Vocal Tract Geometry reports modeling estimated vocal tract length (VTL cm), pharyngeal volume, velopharyngeal port dynamics, larynx height, lip protrusion, and cross-sectional area functions for physical and parametric synthesis.

---

## Overview

Traditional speech acoustic reports simply measure formant frequencies ($F1 - F4$). However, physically-based vocoders, articulatory synthesizers (VocalTractLab, Pink Trombone), and advanced Klatt cascade resonators require solving the inverse acoustic problem: estimating the physical dimensions and postures of the human vocal apparatus that produced those formants.

**`articulatory-vocal-tract-geometry`** translates acoustic spectral measurements into concrete physical parameters: Vocal Tract Length (VTL in cm), oral-to-pharyngeal volume ratios, velopharyngeal nasal coupling, and dynamic vertical larynx excursion.

---

## Core Geometric Parameters

### 1. Estimated Vocal Tract Length (VTL) & Scaling
- **Formant Dispersion ($F_{\text{disp}}$)**: Mean spacing between consecutive resonance poles:
  $$\Delta F = \frac{F4 - F1}{3}$$
- **Anatomical VTL ($L$)**: Calculated via the quarter-wave acoustic tube approximation:
  $$L = \frac{c}{2 \cdot \Delta F} \quad (c = 35000\text{ cm/s})$$
- **VTL Warping Factor**: Scalar relative to standard adult reference vocal tract ($17.0\text{ cm}$).

### 2. Lip Geometry & Labial Aperture
- **Lip Protrusion Bias**: Longitudinal acoustic vocal tract lengthening via labial extension (mm).
- **Labial Aperture Area ($\text{cm}^2$)**: Neutral resting aperture, spread aperture (FLEECE), and rounded constriction (GOOSE).

### 3. Velopharyngeal Port & Nasal Coupling
- **Port Seal**: Tightness of velopharyngeal closure during non-nasal vowels.
- **Nasal Coupling Area ($\text{mm}^2$)**: Acoustic aperture during nasalized phonemes.
- **Acoustic Pole/Zero Pairs**: Extra nasal resonance pole ($F_N$ ~250–450 Hz) and antiformant zero ($Z_N$ ~500–1800 Hz).

### 4. Laryngeal Vertical Posture & Excursion
- **Resting Larynx Height**: Baseline vertical posture (elevated, neutral, or depressed).
- **Dynamic Vertical Displacement**: Vertical shift ($\pm\text{mm}$) during pitch accents and high-intensity oratorical delivery.

---

## Machine Output Schema (`vocal_tract_geometry.json`)

```json
{
  "$schema": "https://json-schemas.voice/vocal-tract-geometry.v1.json",
  "speaker_id": "SPEAKER_ID",
  "vocal_tract_dimensions": {
    "estimated_vtl_cm": 17.2,
    "formant_dispersion_hz": 1018,
    "vtl_warping_scalar": 1.012,
    "oral_to_pharyngeal_length_ratio": 1.05
  },
  "lip_metrics": {
    "neutral_aperture_cm2": 2.2,
    "lip_protrusion_bias_mm": 1.5,
    "rounding_coefficient": 1.08
  },
  "velopharyngeal_port": {
    "port_status": "OCCASIONAL_MICRO_LEAKAGE",
    "coupling_area_mm2": 8.5,
    "nasal_pole_fn_hz": 320,
    "nasal_zero_zn_hz": 1650,
    "nasal_bandwidth_hz": 140
  },
  "larynx_posture": {
    "resting_posture": "MILDLY_ELEVATED",
    "dynamic_displacement_mm": {"f0_peak": 4.5, "f0_floor": -2.0},
    "pharyngeal_constriction_index": 0.62
  }
}
```

---

## Tri-Platform Architecture

Zero duplicate code across tools. Canonical source resides in `.agents`:
- **Canonical**: `C:\Users\<you>\.agents\skills\articulatory-vocal-tract-geometry`
- **Claude**: `C:\Users\<you>\.claude\skills\articulatory-vocal-tract-geometry` (NTFS Junction)
- **Grok**: `C:\Users\<you>\.grok\skills\articulatory-vocal-tract-geometry` (NTFS Junction)
- **Antigravity**: `C:\Users\<you>\.gemini\config\skills\articulatory-vocal-tract-geometry` (NTFS Junction)

---

## Documentation Suite

- [`HOW_TO_USE.txt`](file:///C:/Users/<you>/.agents/skills/articulatory-vocal-tract-geometry/HOW_TO_USE.txt): Standardized user guide and prompt templates.
- [`IMPLEMENTATION_PLAN.md`](file:///C:/Users/<you>/.agents/skills/articulatory-vocal-tract-geometry/IMPLEMENTATION_PLAN.md): Feature checklist and roadmap.
- [`App Changes Tracker.html`](file:///C:/Users/<you>/.agents/skills/articulatory-vocal-tract-geometry/App%20Changes%20Tracker.html): Interactive visual version log.
- [`SKILL.md`](file:///C:/Users/<you>/.agents/skills/articulatory-vocal-tract-geometry/SKILL.md): Agent system instructions and triggers.
