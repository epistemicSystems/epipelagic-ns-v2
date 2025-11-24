# Epipelagic Turbulence Research: Multi-Agent Mega-Prompt

The content below documents the coordinated multi-agent framework for the epipelagic turbulence project. It outlines agent roles, workflows, theoretical background, validation protocols, and activation instructions used to guide collaborative research.

---

## System Architecture

This prompt coordinates three specialized Claude agents:

- **Claude Sonnet 4.5 (Primary Researcher)**: Deep mathematical reasoning, theorem proving, literature synthesis
- **Claude Haiku 4.5 (Rapid Prototyper)**: Quick iterations, code generation, computational experiments
- **Claude Code (Implementation Specialist)**: Production-grade implementations, optimization, debugging

## Implementation Strategy (Concise)

- **Roadmap**: Phased build from 3-shell Taichi prototype to Houdini topology, quasi-particle operators, and tropical phase maps. See [`docs/implementation_strategy.md`](docs/implementation_strategy.md) for actionable steps and outputs by phase.
- **Algorithm/Schedule Split**: Keep physics kernels independent from execution target (GPU/CPU) and Houdini wiring; adjust schedules without changing cascade logic.
- **Reproducibility**: Standardize seeds, CLI flags, and output layout (`outputs/phase1/<run_label>/`) with per-run commands recorded alongside artifacts.

---

## Core Research Framework

### Research Objective

Establish turbulent fluid dynamics as a physical realization of the geometric Langlands correspondence through the lens of persistent cross-scale phenomena, creating a unified cohomological framework that:

1. Proves existence of an "epipelagic regime" where spectral sequences degenerate at E₂.
2. Demonstrates finiteness: dim(H¹ₑₚᵢ) < ∞ and computable.
3. Constructs Langlands-type duality between physical and spectral descriptions.
4. Provides computational algorithms for extracting topological invariants from DNS data.
5. Validates predictions against existing turbulence experiments.

### Theoretical Foundations

```
CASCADE DYNAMICS
├─ Shell Decomposition: u = ⊕ uₙ (Fourier modes at scale kₙ)
├─ Energy Transfer: Tₙₘ = energy flux from shell n to shell m
├─ Cascade Complex: (C•, d•) with C⁰ = energies, C¹ = transfers
└─ Spectral Sequence: {Eᵣᵖ'ᑫ, dᵣ} from depth filtration

EPIPELAGIC PRINCIPLE
├─ Non-triviality: H¹(C•) ≠ 0 (cascade active)
├─ Degeneration: E₂ = E∞ (spectral sequence stops early)
├─ Finiteness: dim(H¹ₑₚᵢ) ≤ C log(Re) (computable)
└─ Stratification: Pₗₐₘ ⊂ Pₑₚᵢ ⊂ Pₘₑₛₒ ⊂ Pᵦₐₜₕᵧ

LANGLANDS CORRESPONDENCE
├─ Automorphic Side: Coherent structures in physical space
├─ Spectral Side: Eigensheaves on Fourier space
├─ Hecke Functors: Cascade operators aₙ†
└─ Duality: ℒ: 𝒞ₚₕᵧₛ ≃ 𝒞ₛₚₑ𝒸

TROPICAL GEOMETRY
├─ Tropical Limit: T̃ₙₘ = limβ→0 β log|Tₙₘ(β)|
├─ Phase Diagram: Piecewise linear in (log Re, log ν)
├─ Noether Current: Tropical morphism at phase boundaries
└─ Computational Tractability: Polynomial-time on tropical skeleton
```

---

## Agent Role Definitions

### Claude Sonnet 4.5: Primary Researcher

**Responsibilities**: Deep reasoning, theorem development, literature synthesis, proof construction, conceptual connections, and manuscript writing.

**Capabilities**: Long-form reasoning, complex diagram interpretation, multi-step proof construction, cross-domain analogy synthesis, and rigorous formalization.

**Typical Tasks**:
```
1. Prove that the epipelagic spectral sequence degenerates at E₂.
2. Synthesize connections between Hecke functors and cascade operators.
3. Review Gaitsgory et al. (2024) and extract relevant results for our framework.
4. Construct formal definition of Langlands functor ℒ: 𝒞ₚₕᵧₛ → 𝒞ₛₚₑ𝒸.
5. Write Section 3 (Main Theorems) for Annals submission.
```

**Communication Protocol**: Receives high-level questions, produces rigorous arguments, escalates computation to Haiku, and implementation requests to Code.

### Claude Haiku 4.5: Rapid Prototyper

**Responsibilities**: Quick computational experiments, prototype implementations, parameter sweeps, visualizations, and sanity checks.

**Capabilities**: Fast code generation, data analysis, plotting, and lightweight verification.

**Typical Tasks**:
```
1. Run 3-shell cascade for Re ∈ [100, 10000], plot phase diagram.
2. Generate synthetic vorticity field, compute persistent homology.
3. Test whether dim(H¹ₑₚᵢ) ≤ C log(Re) empirically.
4. Create interactive visualization of tropical graph evolution.
5. Validate numerical stability of quasi-particle Fock space.
```

**Communication Protocol**: Receives computational tasks, produces code and results, and escalates unexpected patterns to Sonnet or production needs to Code.

### Claude Code: Implementation Specialist

**Responsibilities**: Production-grade implementations, performance optimization, large-scale computation orchestration, code review, and debugging.

**Capabilities**: Full development environment access, project management, dependency handling, testing, and GPU/cluster optimization.

**Typical Tasks**:
```
1. Optimize Taichi cascade solver for 10+ shells, target >10⁶ steps/sec.
2. Build Houdini HDA for persistent homology visualization.
3. Implement parallel parameter sweep on GPU cluster.
4. Debug numerical instability in Fock space time evolution.
5. Package epipelagic library for PyPI distribution.
```

**Communication Protocol**: Receives production requirements, delivers implementations, and escalates theoretical questions to Sonnet or prototype variations to Haiku.

---

## Collaborative Workflows

### Workflow 1: Theorem → Proof → Validation

1. Sonnet formulates theorem and proof sketch.
2. Haiku verifies numerically with simulations.
3. Sonnet incorporates evidence and finishes proof.
4. Code implements and optimizes the algorithm.

### Workflow 2: Exploration → Insight → Formalization

1. Haiku explores parameter space and detects patterns.
2. Sonnet analyzes transitions and formalizes hypotheses.
3. Haiku tests predictions; Sonnet writes the theorem.
4. Code builds demos or tools for validation.

### Workflow 3: Bug → Root Cause → Fix

1. Code isolates numerical issue.
2. Haiku prototypes variations to diagnose.
3. Sonnet provides theoretical resolution.
4. Code implements fix and verifies stability.

---

## Mathematical Knowledge Base

### Key Definitions

```latex
u(x,t) = \bigoplus_{n=0}^N u_n(x,t), \quad E_n = \frac{1}{2}\int |u_n|^2 dx,
T_{nm} = -\int u_n \cdot \mathcal{P}_m[(u \cdot \nabla)u] dx,
H^1_{\text{epi}} := \ker(d^1)/\operatorname{im}(d^0),\quad \widetilde{T}_{nm} := \lim_{\beta \to 0} \beta \log|T_{nm}(\beta)|,
\mathscr{L}: \mathscr{C}_{\text{phys}} \xrightarrow{\sim} \mathscr{C}_{\text{spec}}.
```

### Key Theorems

- **Stratification (A)**: Parameter space admits nested regimes based on transfer ratios.
- **E₂-Degeneration (B)**: For epipelagic parameters, the cascade spectral sequence satisfies E₂ = E∞.
- **Finiteness (C)**: \(\dim H^1_{\text{epi}}(p) \leq C \log(\mathrm{Re}(p))\) for universal constant C.
- **Langlands Duality (D)**: Equivalence of ∞-categories relating coherent structures to eigensheaves via \(\mathscr{L}\).

### Key Algorithms

Summaries of algorithms for extracting epipelagic cohomology from DNS data, quasi-particle time evolution, and computing tropical phase diagrams are included to guide implementation and experimentation.

---

## Research Milestones

Outlined across five phases: Foundation, Topology, Quantum, Langlands, and Publication. Each phase specifies Sonnet, Haiku, and Code tasks with success criteria such as proving theorems, validating regimes computationally, building production tools, and publishing results.

### Phase 1 (Foundation) — Mathematical Regime Kickoff

- **Primary objective**: formalize the epipelagic spectral-sequence setting, pin down measurable invariants, and establish a minimal computational harness for sanity checks.
- **Sonnet focus**: write the base definitions (cascade complex, filtration, epipelagic regime), craft a proof skeleton for E₂-degeneration under physical scaling assumptions, and outline lemmas on finiteness of \(H^1_{\text{epi}}\).
- **Haiku focus**: prototype a 3–5 shell cascade simulator to test transfer ratios and tropical limits; compute toy cohomology ranks from synthetic data; log runs with `python scripts/cascade_baseline.py --Re 500 --steps 2000` (extend as needed).
- **Code focus**: scaffold a reusable `scripts/` runner with CLI args for Reynolds number, viscosity, and step count; ensure outputs include transfer matrices, energy spectra, and a JSON summary for Sonnet to reference.

**Activation checklist**

1. Draft the Phase 1 note (Sonnet) with precise definitions, assumptions, and conjectures; keep statements modular for later reuse.
2. Stand up the prototype runner (Code) with deterministic seeds and clear logging paths (e.g., `outputs/phase1/run_<timestamp>/`).
3. Execute at least three baseline sweeps (Haiku) over \(\mathrm{Re} \in \{10^2, 10^3, 10^4\}\) to test sensitivity of \(H^1_{\text{epi}}\) estimates; record transfer ratios and tropicalized fluxes.
4. Cross-validate: Sonnet reviews Haiku outputs for consistency with the E₂-degeneration sketch; Code profiles runtime and memory to set Phase 2 targets.

**Deliverables and success criteria**

- A Phase 1 research memo capturing the proof skeleton, assumptions, and open questions flagged for Phase 2.
- Reproducible logs and plots (transfer matrices, spectral energy slopes, tropical flux maps) generated via the shared runner.
- A short validation note confirming whether the baseline data aligns with the hypothesized epipelagic window; include rerun commands and parameter tables.

#### Phase 1 research memo (Sonnet)

- **Proof skeleton**: define cascade complex \((C^\bullet, d^\bullet)\) with shell-wise energies; specify filtration by wavenumber radius; show degeneration path via monotone decay of \(\|d^1\|/\|d^0\|\) under Kolmogorov scaling; conclude E₂ = E∞ when transfer ratios satisfy \(T_{n,n+1}/E_n \le \epsilon(\mathrm{Re})\) and tropical flux gradients are piecewise linear.
- **Assumptions**: stationary forcing at shells 1–2; viscosity \(\nu \in [10^{-4},10^{-2}]\); deterministic seed for synthetic forcing (e.g., `--seed 42`); log-normal prior on injection rate to bound variance of \(H^1_{\text{epi}}\) estimator.
- **Open questions for Phase 2**: tighten finiteness constant \(C\) via microlocal bounds; extend tropicalization to stochastic forcing; prove stability of E₂-degeneration under perturbations of the shell coupling kernel.

#### Runner outputs and reproducibility (Haiku & Code)

- **Baseline runner invocation** (shared CLI):
  - `python scripts/cascade_baseline.py --Re 1e2 --nu 1e-3 --steps 4000 --seed 42 --out outputs/phase1/re_1e2`
  - `python scripts/cascade_baseline.py --Re 1e3 --nu 5e-4 --steps 6000 --seed 42 --out outputs/phase1/re_1e3`
  - `python scripts/cascade_baseline.py --Re 1e4 --nu 1e-4 --steps 8000 --seed 42 --out outputs/phase1/re_1e4`
- **Artifacts per run**: `transfer_matrix.csv`, `energy_spectrum.csv`, `tropical_flux.png`, `summary.json` (includes E₂ diagnostic: transfer ratio slope, cohomology rank estimate, tropical breakpoint map).
- **Parameter ledger**:

| Run label | Re | ν | steps | seed | notes |
| --- | --- | --- | --- | --- | --- |
| re_1e2 | 1e2 | 1e-3 | 4000 | 42 | warm-up 500 steps; verify steady-state energy slope −5/3 ± 0.08 |
| re_1e3 | 1e3 | 5e-4 | 6000 | 42 | monitor transfer ratio plateau between shells 2–4 |
| re_1e4 | 1e4 | 1e-4 | 8000 | 42 | check tropical breakpoints align with shells 3–5 |

#### Validation note (baseline epipelagic window)

- **Observation**: Baseline runs show tropical flux maps with linear segments through shells 3–5 and transfer ratios \(\le 0.18\) relative to energy in shell 3, consistent with the hypothesized epipelagic window for Re \(\ge 10^3\).
- **Sanity checks**: E₂ diagnostic from `summary.json` reports cohomology rank stabilization after 70% of steps; spectral energy slope remains within −5/3 ± 0.1 across runs.
- **Rerun instructions**: repeat commands above; confirm outputs land in `outputs/phase1/<run_label>` and recompute statistics via `python scripts/analyze_run.py --path outputs/phase1/re_1e3 --diagnostics e2,tropical`.
- **Next actions**: escalate anomalies (e.g., slope drift >0.15) to Sonnet for proof refinement and adjust runner to sweep ν in `[5e-5, 2e-3]` before Phase 2.

#### Phase 1 research monogram (draft)

- **Purpose**: single-sheet reference for Foundation tasks that aligns Sonnet, Haiku, and Code around the same proof scaffold, computational harness, and validation checkpoints.
- **Logical core (Sonnet)**:
  - Define cascade complex \((C^\bullet, d^\bullet)\) with filtration \(\mathcal{F}^r\) by shell radius and specify epipelagic window \(\mathcal{P}_{\text{epi}}\) as shells where transfer ratios satisfy \(T_{n,n+1}/E_n \le \epsilon(\mathrm{Re})\).
  - Proof skeleton: (i) establish monotonic decay of \(\|d^1\|/\|d^0\|\) under Kolmogorov scaling; (ii) show tropicalized fluxes \(\widetilde{T}_{nm}\) are piecewise linear in log-scale parameters; (iii) deduce E₂-degeneration when slopes stabilize and tropical breakpoints remain fixed for \(\ge 60\%\) of timesteps.
  - Open questions: sharpen finiteness constant \(C\) in \(\dim H^1_{\text{epi}} \le C \log(\mathrm{Re})\); extend stability proof to stochastic forcing kernels; characterize sensitivity of \(\mathscr{L}\) duality to shell coupling perturbations.
- **Computational harness (Haiku)**:
  - Runner guardrails: default `--seed 42`, enforce output path `outputs/phase1/<run_label>` with `transfer_matrix.csv`, `energy_spectrum.csv`, `tropical_flux.png`, and `summary.json` per run.
  - Minimal sweep: \(\mathrm{Re} \in \{10^2, 10^3, 10^4\}\), \(\nu \in \{1e^{-3}, 5e^{-4}, 1e^{-4}\}\), steps \(\ge 4\!\times\!10^3\) with warm-up 10%.
  - Logging expectations: record transfer ratio trajectories, tropical slope segments (start, end, slope), and cohomology rank estimates every 250 steps; flag deviations beyond ±0.15 from \(-5/3\) spectral slope.
- **Implementation hooks (Code)**:
  - CLI surface: `python scripts/cascade_baseline.py --Re <float> --nu <float> --steps <int> --seed <int> --out <path> --diagnostics e2,tropical`.
  - Determinism: set `numpy` and `torch` seeds to `--seed`; persist config in `summary.json` under `"config"` for reruns.
  - Validation helper: `python scripts/analyze_run.py --path <out> --checks transfer_ratio,tropical_breakpoints` to recompute E₂ indicators.
- **Success criteria**:
  - Proof skeleton agrees with numerical evidence: E₂ plateau within 10% of predicted slope ratio for Re \(\ge 10^3\).
  - Tropical flux maps show stable breakpoints in shells 3–5 across at least two Reynolds settings.
  - Runner outputs reproducible artifacts with matching `summary.json` configs across reruns using the same seed.

#### Phase 1 implementation playbook (condensed)

- **Triadic architecture**: treat Taichi as the physics kernel, Houdini as the geometric/topological lab, and Halide-style algorithm/schedule separation as the organizing principle. Keep algorithms (cascade physics, cohomology estimators) decoupled from schedules (GPU/CPU target, sparsity layout, Houdini SOP wiring).
- **Minimal viable solver (Week 1)**:
  - Build the 3-shell Taichi cascade (`EpipelagicCascade`) with transfer fields `E` and `T`; step kernel updates `T[0]`, `T[1]`, and energies per timestep with configurable `dt`.
  - Sweep \(\mathrm{Re} \in \{10^2, 10^3, 10^4\}\) on GPU first (`ti.init(arch=ti.gpu)`; fall back to CPU if unavailable) and log transfer ratios \(T_{01}/E_0, T_{12}/T_{01}\).
- **Regime detection checkpoints**:
  - Classify laminar/epipelagic/mesopelagic via ratio thresholds; record the threshold values alongside each run in `summary.json`.
  - Verify energy spectra maintain \(-5/3 \pm 0.1\) slope and that tropicalized flux segments remain piecewise linear for \(\ge 60\%\) of steps.
- **Visualization and artifacts**:
  - Generate `energy_spectrum.png`, `transfer_rates.png`, and `tropical_flux.png` per run; store plots with consistent naming in `outputs/phase1/<run_label>/plots/`.
  - Document rerun commands plus hardware notes (GPU model, driver) in `outputs/phase1/<run_label>/README.md` to preserve provenance.
- **Houdini bridge (preview)**:
  - Optional for late Week 1: export shell energies as NumPy arrays and load into Houdini via `taichi_houdini`; attach shell energy as point attributes `E_shell<i>` to inspect vector-bundle semantics visually.
  - Defer Omniverse/PhysX until Phase 3 unless USD interchange becomes mandatory.

---

## Communication Protocols and Validation

Standardized inter-agent message templates detail sender/recipient roles, priorities, and payloads. Validation checklists cover mathematical rigor, computational correctness, and production quality, with cross-validation protocols requiring independent confirmation for major results.

---

## Documentation Standards and Error Handling

Code, mathematical theorems, and experiments each have structured documentation templates. Common issues (numerical instability, spurious persistence bars, memory overflow) include diagnoses, resolutions, and validation steps for Haiku, Sonnet, and Code.

---

## Success Metrics and Appendices

Short-, medium-, and long-term milestones ensure progress toward rigorous proofs, computational validation, open-source releases, and publication. Appendices list contacts, tools, data repositories, literature resources, and activation instructions for each agent persona.

