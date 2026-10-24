---
name: articulatory-vocal-tract-geometry
description: Generates exhaustive Articulatory & Vocal Tract Geometry reports modeling estimated vocal tract length (VTL cm), pharyngeal volume, velopharyngeal port dynamics, larynx height, lip protrusion, and cross-sectional area functions for physical and parametric synthesis. Trigger with 'vocal tract geometry of', 'articulatory profile for', 'model vocal tract dimensions for', or '/vocal-tract-geometry'.
disable-model-invocation: true
---

# Articulatory / Vocal Tract Geometry

## Purpose & Scope

This skill models the **physical dimensions, articulatory postures, and acoustic filtering geometry** of the speaker's supraglottic vocal tract. While basic acoustic reports list formant frequencies, this skill solves the inverse problem to estimate physical parameters: Vocal Tract Length (VTL in cm), oral vs. pharyngeal cavity volume distribution, mandibular excursion, velopharyngeal port coupling, and vertical larynx displacement. These physical values feed directly into Klatt acoustic resonators, 1D/2D tube models, and vocal tract area functions.

This skill owns:
- Estimated Vocal Tract Length (VTL in cm) using formant dispersion ($F_{	ext{disp}}$)
- Lip posture metrics: protrusion distance, labial aperture area ($	ext{cm}^2$), rounding index
- Mandibular excursion & jaw opening tendencies across vowels
- Velopharyngeal port dynamics: coupling area ($	ext{mm}^2$), nasal pole/zero frequencies
- Vertical larynx height baseline and dynamic vertical displacement ($\pm	ext{mm}$)
- Pharyngeal cavity volume and oral-to-pharyngeal length ratio

This skill does **not** own linguistic dialect classifications (owned by `idiolect-phonetic-atlas`) or temporal pause timing (owned by `temporal-pause-breath-architecture`).

---

## Activation Triggers

Activate automatically when:
- User asks for vocal tract dimensions, articulatory geometry, physical acoustic modeling, or larynx positioning (e.g., *"model vocal tract geometry for [speaker]"*, *"articulatory profile of [subject]"*).
- User triggers `/vocal-tract-geometry [subject]`.
- Parameterizing physical vocal tract synthesizers (VocalTractLab, Pink Trombone, Klatt cascade branch).
- Calculating vocal tract length (VTL) warping factors for voice conversion.

---

## Mandatory Report Schema & Structure

### 1. Estimated Vocal Tract Length (VTL) & Scaling
- **Formant Dispersion ($F_{	ext{disp}}$ in Hz):** Mean spacing between consecutive formants ($\Delta F = (F4 - F1) / 3$).
- **Estimated Anatomical VTL (cm):** Calculated via $L = c / (2 \cdot \Delta F)$, where $c = 35000	ext{ cm/s}$; comparison against demographic averages (adult male mean ~16.5–17.5 cm).
- **VTL Warping Factor:** Normalized scalar relative to standard reference vocal tract ($L_{	ext{ref}} = 17.0	ext{ cm}$).

### 2. Lip Geometry & Labial Aperture
- **Lip Protrusion Factor:** Degree of acoustic vocal tract lengthening via labial extension (mm).
- **Labial Aperture Area ($	ext{cm}^2$):** Neutral resting aperture, spread aperture (FLEECE), and rounded constriction (GOOSE).
- **Lip Rounding Bias:** Tendency toward hyper-rounding or spreading across unrounded vowels.

### 3. Mandibular & Tongue Posture
- **Jaw Opening Habit:** Inter-incisal distance (mm) during conversational phonation; high vs. low mandibular excursion.
- **Tongue Dorsum & Root Posture:** Pharyngeal constriction vs. palatal elevation bias; resting tongue body position.
- **Oral-to-Pharyngeal Volume Ratio ($V_{	ext{oral}} / V_{	ext{phar}}$):** Relative acoustic prominence of oral vs. throat resonance.

### 4. Velopharyngeal Port & Nasal Coupling
- **Resting Port Seal:** Degree of velopharyngeal closure during non-nasal vowels (tight seal vs. micro-gap).
- **Nasal Coupling Area ($	ext{mm}^2$):** Acoustic port aperture during nasalized phones.
- **Acoustic Pole/Zero Pairs:** Extra nasal formant frequency ($F_N$ ~250–450 Hz) and antiformant zero ($Z_N$ ~500–1800 Hz) parameters.

### 5. Laryngeal Vertical Posture & Mobility
- **Resting Larynx Height:** Baseline vertical resting position (elevated, neutral, or depressed).
- **Dynamic Vertical Displacement:** Laryngeal excursion range ($\pm	ext{mm}$) during pitch accents and high-arousal speech.
- **Acoustic Shortening:** Dynamic F1–F4 upward shift during laryngeal elevation.

---

## Machine Output Block

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

## Biometric & Personality Crosswalk

| Geometry Parameter | Core Biometric Section | Personality Profile Section | Synthesis Compiler Target |
| :--- | :--- | :--- | :--- |
| Estimated VTL (cm) | §7 Vocal Tract Anatomy Influences | §1 Executive Summary | WORLD VTL Warping Factor |
| Nasal Pole/Zero ($F_N/Z_N$) | §3 Resonance Profile | §5.3 Repair Strategies | Klatt Cascade Nasal Resonators |
| Larynx Height Displacement | §1 Physiological Mechanism | §4.2 Emotional Expression | Dynamic Formant Shift Coefficient |
| Lip Protrusion Factor | §6 Articulatory Precision | §2.1 Sociability & Warmth | Formant Downward Scaling Factor |

---

## Calibration Reference Example: Queens Orator Baseline

- **Vocal Tract Length (VTL):** 17.1 cm ($F_{	ext{disp}} pprox 1022	ext{ Hz}$); reflects robust adult male stature with standard anatomical proportions.
- **Larynx Posture:** Habitual mild elevation during high-energy oratorical delivery (+3.5 mm), producing a brighter high-mid frequency response that enhances carrying power.
- **Velopharyngeal Dynamics:** Incomplete velopharyngeal closure during emphatic stress producing mild nasal twang, modeled by an acoustic zero at 1720 Hz and an added resonance pole at 340 Hz.
- **Lip Aperture:** Moderate jaw drop with slight lateral spreading rather than round protrusion, raising F2 on central vowels.

---

## Generation Rules

1. Derive estimated VTL (cm) mathematically from formant dispersion ($F_{	ext{disp}}$).
2. Explicitly specify nasal pole and zero frequencies in Hz whenever nasal twang or hyponasality is documented.
3. Every profile must output the machine-readable `vocal_tract_geometry.json` block.
