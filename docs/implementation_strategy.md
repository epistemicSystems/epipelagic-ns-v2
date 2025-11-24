# Epipelagic Turbulence: Implementation Strategy

This guide distills the triadic architecture and phased roadmap for building the epipelagic turbulence framework. It emphasizes actionable steps, algorithm/schedule separation, and reproducibility.

## Triadic Architecture (Halide-Style Separation)
- **Taichi (Physics Kernel)**: GPU-first cascade solvers with sparse SNodes; DiffTaichi for optimization.
- **Houdini (Geometry/Topology Lab)**: SOP/DOP networks for vorticity fields, attribute-based vector bundles, and visualization; Python/VEX scripting for discrete differential geometry.
- **Halide Principles (Design Pattern)**: Keep physics algorithms independent from execution schedule (CPU/GPU target, sparsity layout, Houdini wiring). Adjust schedules without altering core physics logic.
- **Optional Omniverse (Phase 3+)**: USD interchange and PhysX integration only if multi-tool collaboration or RTX viz becomes mandatory.

## Phased Roadmap
1. **Phase 1: Minimal Viable Prototype (Weeks 1-4)**
   - Implement 3-shell `EpipelagicCascade` in Taichi with transfer ratios and regime detection.
   - Sweep Reynolds numbers (1e2, 1e3, 1e4); log `transfer_matrix.csv`, `energy_spectrum.csv`, `tropical_flux.png`, `summary.json` under `outputs/phase1/<run_label>/`.
   - Plots: energy spectrum, transfer rates, tropical flux; classify laminar/epipelagic/mesopelagic via ratio thresholds.

2. **Phase 2: Geometry & Topology (Weeks 5-8)**
   - Bridge Taichi → Houdini via `taichi_houdini`; persist solver state in `hou.session`.
   - Export shell energies/fields as geometry attributes; compute vorticity, level sets, and persistent homology (Ripser/Gudhi).
   - Visualize vector-bundle semantics through attributes and barcodes.

3. **Phase 3: Quasi-Particle Formalism (Weeks 9-16)**
   - Implement Fock-space operators (`create`, `annihilate`) and Hamiltonian components (free, interaction, dissipation) in Taichi.
   - Map Houdini node graphs to Feynman diagrams; traverse for amplitudes.
   - Track spectral-sequence convergence (E² → E∞) alongside cascade rates.

4. **Phase 4: Tropical Geometry & Phase Diagrams (Weeks 17-24)**
   - Tropicalize transfer laws; build piecewise-linear phase space over (Re, ℓ, time window).
   - Compute Noether currents and track changes at tropical phase boundaries.

5. **Phase 5: Validation & Publication (Weeks 25-40)**
   - Compare with DNS datasets (e.g., Johns Hopkins); verify H¹_epi estimates and −5/3 spectra.
   - Produce manuscripts, interactive demos, and Houdini HDAs.

## Immediate Next Actions (Week 1)
- **Environment**: `pip install taichi numpy scipy matplotlib sympy ripser`; install Houdini 19.5+ and `taichi_houdini` if available.
- **Sanity Checks**: run Taichi fractal demo; create a minimal Houdini SOP network; validate `taichi_houdini` MPM example.
- **Prototype**: build the 3-shell Taichi solver (`ti.gpu` preferred, fallback `ti.cpu`); sweep Re and log artifacts; record commands and hardware notes per run.

## Reproducibility Checklist
- Default seed `42`; capture run config in `summary.json` (`config` block with Re, ν, steps, seed, hardware).
- Use consistent output layout: `outputs/phase1/<run_label>/plots/` for images and root for CSV/JSON artifacts.
- Document rerun commands (CLI invocations) alongside artifacts; prefer GPU-first schedule, falling back to CPU only when necessary.

## Agent Alignment
- **Sonnet**: maintain proof skeleton, finiteness bounds, and E²-degeneration criteria; flag open questions for stochastic forcing and coupling perturbations.
- **Haiku**: own parameter sweeps, plotting, and tropical breakpoint detection; surface anomalies beyond ±0.15 spectral slope drift.
- **Code**: harden CLI (`cascade_baseline.py`, `analyze_run.py`), enforce determinism, and optimize Taichi schedules; keep hooks ready for Houdini export and Phase 3 operators.

