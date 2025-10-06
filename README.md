# GRAV-Bench: General Relativistic Visualization Benchmark

A comprehensive benchmark for testing LLM and developer capabilities in simulating black hole physics through general relativistic ray tracing.

## Overview

GRAV-Bench evaluates the ability to implement physically accurate black hole visualizations using the Schwarzschild metric and geodesic equations. This benchmark tests deep understanding of general relativity, numerical methods, computer graphics, and performance optimization.

**Difficulty Level:** Graduate-level physics + Professional software engineering

**Estimated Time:** 20-40 hours for full implementation

## Benchmark Requirements

### Tier 1: Core Physics (40 points - Required)

#### Schwarzschild Metric Implementation (10 pts)
- Correct implementation of the Schwarzschild metric: `ds² = -(1-2M/r)dt² + (1-2M/r)⁻¹dr² + r²dΩ²`
- Proper coordinate handling (Boyer-Lindquist or equivalent)
- No numerical instabilities at the event horizon (r = 2M)
- Correct asymptotic behavior (flat spacetime as r → ∞)

**Validation:** Compare metric components at r = 3M, 5M, 10M against analytical values

#### Geodesic Integration (15 pts)
- Implementation of null geodesic equations for photon paths
- Runge-Kutta 4th order (RK4) or equivalent integration method
- Correct computation of Christoffel symbols Γ^μ_νρ
- Energy conservation along geodesic (drift < 1%)
- Angular momentum conservation (drift < 1%)

**Validation:**
```
Circular photon orbit at r = 3M should remain stable for 100+ orbits
Verify: L/E = 3√3 M at photon sphere
```

#### Critical Radii (10 pts)
- Event horizon located at exactly r = 2M (Schwarzschild radius)
- Photon sphere at exactly r = 3M (1.5 × Schwarzschild radius)
- Innermost stable circular orbit (ISCO) at r = 6M for massive particles
- Visual rendering consistent with these physical boundaries

**Validation:** Ray with impact parameter b = 3√3 M should orbit the photon sphere

#### Ray Tracing Architecture (5 pts)
- Backward ray tracing from camera position implemented
- Correct handling of rays falling into the event horizon (proper termination)
- Correct handling of rays escaping to infinity
- Proper affine parameter integration

---

### Tier 2: Visual Features (30 points - Must pass 4 of 5)

#### Gravitational Lensing (8 pts)
- Background star field shows visible distortion near black hole
- Light bending angle matches Schwarzschild predictions
- Primary and secondary images visible for aligned sources
- Smooth interpolation without pixelation artifacts

**Validation:** Star at 45° elevation should appear at approximately 50-55° when viewed near horizon

#### Einstein Ring Formation (8 pts)
- Perfect ring forms when source, black hole, and observer are aligned
- Ring radius approximately √(2.6M × D_s) where D_s is source distance
- Ring brightness correctly conserves surface brightness
- Ring is sharp and well-defined

**Validation:** Perfectly aligned star source must produce circular ring

#### Black Hole Shadow (8 pts)
- Dark central region clearly visible
- Shadow radius approximately 2.6M (photon sphere projection)
- Sharp boundary (not artificially blurred)
- Shadow is perfectly circular for Schwarzschild metric

**Validation:** Measure shadow angular radius: θ_s ≈ √27 M/D_obs

#### Accretion Disk with Doppler Shifting (8 pts)
- Rotating accretion disk visible
- Blue shift on approaching side (appears brighter)
- Red shift on receding side (appears dimmer)
- Correct frequency shift: ν_obs/ν_emit = √[(1-2M/r)/(1-v²)]

**Validation:** Approaching side should be >2× brighter than receding side at high rotation speeds

#### Multiple Image Formation (8 pts)
- Same source appears multiple times around black hole
- At least one "backwards" image (photon that orbited the hole)
- Image positions match theoretical predictions
- Brightness decreases exponentially for higher-order images

**Validation:** Star at specific position should produce 2 or more distinct images

---

### Tier 3: Advanced Features (20 points - Must pass 3 of 7)

#### Relativistic Beaming (3 pts)
- Disk brightness asymmetry with ratio > 5:1 at v ~ 0.5c
- Follows Doppler boosting formula: I ∝ δ³

#### Gravitational Redshift Visualization (3 pts)
- Visible color shift near event horizon
- Correct redshift factor: z = 1/√(1-2M/r) - 1

#### Time Dilation Effects (3 pts)
- Visualization of clock slowdown near horizon
- Display time ratio: dt/dτ = 1/√(1-2M/r)

#### Kerr Metric Support (5 pts)
- Spin parameter a ∈ [0, 1] controllable
- Frame dragging effects visible (asymmetric lensing)
- Ergosphere boundary displayed
- Correct event horizon: r₊ = M + √(M² - a²)

#### Effective Potential Display (2 pts)
- Graph of V_eff(r) = (1-2M/r)(1 + L²/r²)
- Updates dynamically with parameter changes

#### Backwards Star Field (2 pts)
- Stars visible "behind" the observer (photons that orbited black hole)
- Physically correct positions and brightness

#### Ray Path Step-Through (2 pts)
- Visualization of individual ray trajectories
- Ability to pause and inspect integration steps

---

### Tier 4: Interactive Controls (15 points - Required)

#### Camera Controls (5 pts)
- Orbital camera system (rotate around black hole)
- Zoom in and out functionality
- Smooth movement without jitter

#### Parameter Adjustment (5 pts)
- Black hole mass M adjustable in real-time
- Accretion disk temperature and rotation speed controllable
- Spin parameter a/M slider for Kerr metric (if implemented)

#### Comparison Mode (5 pts)
- Toggle between Newtonian and relativistic rendering
- Side-by-side or overlay comparison
- Clear visual differences demonstrable

---

### Tier 5: Performance (10 points - Required)

#### Resolution and Speed (10 pts)
- Handles 1920×1080 resolution
- Renders single frame in < 10 seconds (< 5 seconds ideal)
- Uses adaptive step sizing near event horizon (step size < 0.01M at r = 2M)
- GPU acceleration (CUDA/OpenCL) or equivalent optimization

**Validation:** Render 1080p frame with 10,000+ rays in under 10 seconds

---

### Bonus Tier: Optional Features (10 points extra credit)

#### ISCO Visualization (2 pts)
- Shows innermost stable circular orbit at r = 6M

#### Penrose Diagram (3 pts)
- Correct conformal spacetime structure
- Shows event horizon, singularity, and infinity regions

#### Gravitational Waves (3 pts)
- Binary black hole merger visualization
- Waveform amplitude display

#### Tidal Forces (2 pts)
- Demonstrates spaghettification on test object
- Shows differential gravitational force visualization

---

## Scoring System

### Point Distribution

| Tier | Points | Status |
|------|--------|--------|
| Tier 1: Core Physics | 40 | Required |
| Tier 2: Visual Features | 30 | 4 of 5 required |
| Tier 3: Advanced | 20 | 3 of 7 required |
| Tier 4: Interactivity | 15 | Required |
| Tier 5: Performance | 10 | Required |
| Bonus Features | 10 | Optional |
| **Total** | **125** | **Pass: 75+** |

### Grading Scale

| Grade | Points | Requirements |
|-------|--------|--------------|
| A+ (Outstanding) | 100+ | All tiers + 3+ bonus features |
| A (Excellent) | 90-99 | All tiers, some bonus |
| B (Good) | 80-89 | All Tier 1-4, most Tier 5 |
| C (Pass) | 75-79 | All Tier 1, most Tier 2-3 |
| F (Fail) | < 75 | Incomplete core physics |

### Automatic Failure Conditions

Even with sufficient points, implementations automatically fail if:

1. Event horizon position incorrect (not at r = 2M)
2. Photon sphere position incorrect (not at r = 3M)
3. Energy or momentum conservation error > 5%
4. Program crashes when rays approach horizon
5. No visible gravitational lensing effect

---

## Validation Test Suite

### Test 1: Photon Sphere Orbit
```python
# Ray with impact parameter b = 3√3 M should orbit at r = 3M
assert abs(min_radius - 3*M) < 0.01*M
```

### Test 2: Deflection Angle
```python
# Light grazing at r = 3M should deflect by approximately 141.3 degrees
assert abs(deflection_angle - 2.466) < 0.05  # radians
```

### Test 3: Shadow Size
```python
# Shadow radius for observer at infinity
shadow_radius = measure_shadow_pixels() * pixel_to_M_ratio
assert abs(shadow_radius - 2.6*M) < 0.1*M
```

### Test 4: Gravitational Redshift
```python
# At r = 3M, gravitational redshift z approximately 0.732
measured_z = (wavelength_obs - wavelength_emit) / wavelength_emit
assert abs(measured_z - 0.732) < 0.05
```

### Test 5: Doppler Shift Asymmetry
```python
# Disk rotating at 0.5c should show approximately 3:1 brightness ratio
ratio = max_brightness / min_brightness
assert 2.5 < ratio < 4.0
```

### Test 6: Conservation Laws
```python
# Energy drift over 10 orbital periods
energy_drift = abs(E_final - E_initial) / E_initial
assert energy_drift < 0.01  # 1% tolerance
```

---

## Implementation Guidelines

### Required Mathematical Components

**Schwarzschild Metric Components:**
```
g_tt = -(1 - r_s/r)
g_rr = 1/(1 - r_s/r)
g_θθ = r²
g_φφ = r² sin²θ

where r_s = 2GM/c² (Schwarzschild radius)
```

**Geodesic Equations (null paths):**
```
d²x^μ/dλ² + Γ^μ_νρ (dx^ν/dλ)(dx^ρ/dλ) = 0

where λ is the affine parameter
```

**Conserved Quantities:**
- Energy: E (from time translation symmetry)
- Angular momentum: L (from rotational symmetry)

**Impact Parameter:**
```
b = L/E

Critical value at photon sphere: b_crit = 3√3 M
```

### Numerical Integration Requirements

- **Method:** Runge-Kutta 4th order minimum (RK4, RK45, or Dormand-Prince)
- **Step size:** Adaptive, with smaller steps near event horizon
- **Typical step:** Δλ ~ 0.1M far from hole, Δλ ~ 0.001M near r = 2M
- **Precision:** Double precision (float64) required
- **Termination:** Stop at r < 2.01M (fallen in) or r > 1000M (escaped)

### Ray Tracing Strategy

1. **Backward Integration:** Trace rays from camera backward in time
2. **Initial Conditions:** Set position at camera, direction toward pixel
3. **Integration:** Evolve along null geodesic until termination
4. **Intersection Testing:** Check for hits with accretion disk, stars
5. **Color Assignment:** Apply Doppler shift, gravitational redshift

### Common Pitfalls

1. **Coordinate Singularity:** The metric appears singular at r = 2M but spacetime is smooth. Handle numerically with care.
2. **Sign Errors:** Pay attention to signature convention (-,+,+,+) vs (+,-,-,-)
3. **Units:** Work in geometric units (G = c = 1) or be explicit about conversions
4. **Affine Parameter:** Don't confuse affine parameter λ with coordinate time t
5. **Integration Direction:** Camera rays go backward (negative λ direction)

---

## Reference Materials

### Key Papers

- Luminet, J. (1979). "Image of a spherical black hole with thin accretion disk." *Astronomy and Astrophysics*, 75, 228-235.
- Cunningham, C. T., & Bardeen, J. M. (1973). "The optical appearance of a star orbiting an extreme Kerr black hole." *The Astrophysical Journal*, 183, 237-264.
- James, O., von Tunzelmann, E., Franklin, P., & Thorne, K. S. (2015). "Gravitational lensing by spinning black holes in astrophysics, and in the movie Interstellar." *Classical and Quantum Gravity*, 32(6), 065001.

### Textbooks

- Misner, C. W., Thorne, K. S., & Wheeler, J. A. (1973). *Gravitation*. Freeman.
- Carroll, S. M. (2004). *Spacetime and Geometry: An Introduction to General Relativity*. Pearson.
- Chandrasekhar, S. (1983). *The Mathematical Theory of Black Holes*. Oxford University Press.

### Online Resources

- [Schwarzschild Geodesics - SageMath](https://doc.sagemath.org/html/en/reference/manifolds/sage/manifolds/differentiable/examples/schwarzschild.html)
- [Geodesic Integration Tutorial](https://einsteintoolkit.org/)
- [Event Horizon Telescope](https://eventhorizontelescope.org/)

---

## Submission Requirements

### Code Requirements

1. **Language:** Python, C++, or CUDA/OpenCL (specify)
2. **Dependencies:** List all libraries and versions
3. **Documentation:** Include theory document explaining implementation
4. **Build Instructions:** Clear steps to compile and run
5. **Test Suite:** Include validation tests

### Deliverables

1. **Source Code:** Complete, commented, version-controlled
2. **Rendered Images:** At least 5 example outputs showing different features
3. **Performance Report:** Frame times, optimization techniques used
4. **Theory Document:** 2-5 pages explaining physics implementation
5. **Demo Video:** 30-60 seconds showing interactive features

### File Structure
```
grav-bench-submission/
├── README.md
├── requirements.txt
├── src/
│   ├── metric.py (or .cpp/.cu)
│   ├── geodesic.py
│   ├── ray_tracer.py
│   ├── renderer.py
│   └── main.py
├── tests/
│   ├── test_metric.py
│   ├── test_geodesic.py
│   └── validation_suite.py
├── docs/
│   └── theory.pdf
├── images/
│   ├── example1.png
│   ├── example2.png
│   └── ...
└── demo.mp4
```

---

## Expected Visual Output

A successful implementation should produce images qualitatively similar to:

- The black hole "Gargantua" from the movie *Interstellar*
- Event Horizon Telescope M87 image (2019)
- Classic Luminet (1979) black hole visualization

### Visual Checklist

- Dark circular shadow in center
- Bright ring surrounding shadow (photon sphere glow)
- Warped background star field
- Asymmetric accretion disk (one side significantly brighter)
- Einstein rings for aligned light sources
- Multiple images of same source at different positions

---

## Evaluation Criteria Summary

### Physics Accuracy (40%)
- Correct implementation of general relativity
- Numerical stability and precision
- Conservation laws maintained

### Visual Quality (30%)
- All required features visible and correct
- Physically accurate rendering
- Smooth, artifact-free output

### Performance (15%)
- Meets resolution and speed requirements
- Efficient algorithms
- Scalable architecture

### Interactivity (10%)
- Responsive controls
- Real-time parameter adjustment
- Intuitive user interface

### Code Quality (5%)
- Clean, readable, well-documented
- Proper error handling
- Comprehensive testing

---

## FAQ

**Q: Can I use existing physics engines or libraries?**
A: You may use standard numerical libraries (NumPy, SciPy, Eigen) and rendering libraries (OpenGL, Vulkan), but you must implement the core GR physics yourself.

**Q: What coordinate system should I use?**
A: Boyer-Lindquist coordinates are recommended for Schwarzschild. For Kerr, you must use Boyer-Lindquist.

**Q: How do I handle the coordinate singularity at r = 2M?**
A: Use adaptive step sizing and careful numerical handling. The singularity is coordinate-based, not physical.

**Q: Is GPU acceleration required?**
A: Not strictly required, but highly recommended to meet performance targets at 1080p resolution.

**Q: Can I submit a partial implementation?**
A: Yes, but you need minimum 75 points to pass. Focus on Tier 1 (required) first.

**Q: How long should this take?**
A: Expect 20-40 hours for a complete implementation, depending on experience level.

---

## License

GRAV-Bench is released under MIT License. Implementations may use any license.

---

## Contact & Contributions

For questions, clarifications, or to submit your implementation:
- Open an issue on the benchmark repository
- Submit a pull request with improvements
- Share your results and visualizations
