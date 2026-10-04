# ENT: documentary errata and reproducibility notes

**Prepared 2 October 2026. Source-specific documentary supplement; not a revised theory or a software release.**

## Scope and preserved formulation

This note separates reproducible calculations, reported interpretations and unresolved evidence in the source snapshot identified below. It does not replace ENT's axioms, seven-constraint architecture, Structurism, cross-domain scope, operational definitions or proposed thresholds. Existing manuscripts and executable files are retained without alteration by this documentary update. A limitation of an inspected implementation is not, by itself, a disproof of the entire theory. Equally, preserving the theory does not make an unsupported result established.

The baseline is [repository commit `0dee4f916dd5f8f594907a816a1fc0a0b847736a`][baseline]. Manuscript locations below refer to the 17-page [K84 Complete Manuscript][manuscript] in that snapshot, Git blob `5ef9f38efb23f5cfafea76e2c80a0059bd7045cf`. Statements about available files are limited to this repository snapshot, not private work or every external archive version.

The narrow errata below qualify the specified numerical, implementation and reproduction statements. They do not silently select a new interpretation where publications use different definitions. No unchanged or improved empirical efficacy is established by this documentary update.

## D1. Missing mathematical content in the PDF

**Location:** K84 pp. 4 and 6, sections 3.1-3.3 and 3.7.

Several equations and inline symbols introduced by the surrounding prose are absent from the inspected rendered PDF. This is not merely a text-extraction omission. Until a source-exact restoration is approved, readers should not reconstruct the missing expressions by selecting a different formula from another paper. No equation is restored or replaced by this note. [Source: K84][manuscript].

**Effect:** identifies a documentary defect; does not choose a mathematical definition.

## D2. Quantum script: implementation and execution status

**Location:** [Simulationa/Quantum_validation.py][quantum], `simulate_qubit_decoherence`, especially the measurement, statistic and return block; K84 sections 4.3 and 7.2.

The source constructs an Aer simulation from backend information; it is not itself a record of executing these circuits on quantum hardware. The circuit prepares an excited state, waits and measures its population. The measured `p1` is estimated from simulated counts. The value `0.5` is a prescribed reference probability used in `tau_c`, not a hard-coded measured result.

The source contains an unmatched parenthesis in the `critical_time` expression and does not parse as written. A simulation result cannot be attributed to successful execution of this exact file without an identified working version or other reproducible provenance. This note does not repair the syntax, change probability handling, alter the noise model or rerun a device experiment.

For the implemented positive-probability formula, `kappa_R = -ln(p1)/ln(2)`, probabilities 1, 0.5 and 0.25 give 0, 1 and 2 respectively. Thus decreasing excited-state population raises this particular statistic. The reported all-zero trace does not, without a verified simulation and measurement mapping, establish that physical passive decay cannot cross the defined cutoff. This is a statement about the inspected statistic, not a replacement definition of structural emergence. [Source code][quantum]; [reported results in K84][manuscript].

**Effect:** corrects source attribution and documents an unresolved execution problem. All executable changes remain separate work.

## D3. QAOA operator maximum versus a proposed cutoff

**Location:** K84 section 7.6; [complete simulation script][complete], Simulation 3.

For the operator as written, `H = -Z tensor Z tensor I - I tensor Z tensor Z`, the eigenvalues are `(-2, -2, 0, 0, 0, 0, 2, 2)`. Therefore the maximum of the objective `-<H>` over states is **2**, not 1.5. The two commuting terms each have eigenvalues +1 or -1; the state `|000>` attains `-<H> = 2`.

This is a local correction to the theoretical-maximum statement. It does **not** replace the separately assigned `tau_c_quant = 1.5`, change the Hamiltonian, establish a new threshold or report a new optimizer/hardware result. An operator maximum, an achieved optimizer value and a decision threshold must be identified separately. [Operator and cutoff][complete]; [K84 section 7.6][manuscript].

**Effect:** corrects a specific algebraic claim without changing the model or its cutoff.

## D4. Synthetic vacuum selection and exponential statistic

**Location:** [complete simulation script][complete], Simulation 1; K84 sections 4.5 and 7.4.

The script generates two arrays from absolute-valued normal samples using seed 42, defines their ratio and applies `tau_c_vac = 1.8`. Reproducing this numerical block yields **2,642 of 10,000 selected cases (26.42%)**. K84 section 7.4 already reports the rounded 26.4%; that rounded fraction is not an additional error.

The implemented expression uses the median of the **below-threshold subset**:

`exp(1.8 - median(tau_vacua[~stable_mask])) = 1.7198325285...`

Using the median of the **whole sample instead** gives approximately `1.4587381730`. That is a different estimator, not the value produced by the published expression. This comparison does not establish the historical provenance of an earlier 1.46 claim.

The arrays are synthetic inputs. The code does not derive a physical energy unit for either exponential result. Its printed TeV label does not supply the missing physical mapping. The selection fraction and exponential value should therefore be attributed to this constructed numerical model; they do not by themselves establish a SUSY mass prediction. No cutoff, estimator, input distribution or physics hypothesis is replaced here. [Source][complete].

**Effect:** makes the calculation and its evidential scope explicit while retaining the original scientific question.

## D5. Gravitational sensitivity calculation

**Location:** [complete simulation script][complete], Simulation 2; K84 sections 3.7 and 7.5.

The source chooses a Gaussian profile, calculates its numerical second derivative and inserts `ligo_bound = 1e-19`. Dividing this input by the maximum absolute derivative gives approximately `1.125068889e-19`, rounded to `1.13e-19`. This block neither loads gravitational-wave observations nor performs detector-level inference.

The numerical agreement is reproducible arithmetic under chosen inputs, not an independently estimated observational limit. The script's `m^2` label and the manuscript's dimensionless convention also require a documented physical/unit mapping. This note does not choose a replacement convention, modify the field equation or establish a detector prediction. [Calculation][complete]; [K84 equations and interpretation][manuscript].

**Effect:** qualifies observational attribution; no new gravitational model or parameter value is introduced.

## D6. Neural data provenance and statistic

**Location:** [Simulationa/Neural_validation.py][neural]; K84 sections 4.2, 5.1 and 7.1.

When data loading fails, the script prints a notice and substitutes a `1200 x 50` Gaussian random array. It is therefore inaccurate to call the fallback literally silent. It is also inaccurate to treat an output produced by that branch as an empirical HCP measurement. The final reporting label does not distinguish those cases adequately.

The quantity labeled KL divergence is computed from mean absolute connectivity values without explicitly normalizing them to sum to one, and uses a negative sum. That expression is not the standard normalized positive KL divergence as labeled. Selecting a different normalization, sign, null distribution or zero-value rule would change the measurement and requires separate review; none is selected here.

Synthetic fallback data do not by themselves establish sleep/wake, EEG or awareness thresholds. This evidential limitation does not remove neural or consciousness-related hypotheses from ENT's research scope. [Source][neural]; [K84 discussion][manuscript].

**Effect:** distinguishes actual inputs and implemented arithmetic from physiological interpretation; code and thresholds remain unchanged.

## D7. Constructed IIT correlation and sample count

**Location:** [Simulationa/iit_correlation.py][iit]; K84 section 7.3.

The source creates **100** equally spaced `phi` values and generates `kappa_R` as `0.85*phi + 0.3` plus Gaussian noise. Reproducing that construction gives `r = 0.9804777823...`, slope `0.8576629263...` and intercept `0.2905930647...`.

Those numbers describe a deliberately constructed relationship. The file does not independently compute IIT's Phi across 120 observations or eight system types. The corresponding K84 sample-count and system-type attribution is not supported by this inspected generator. The local correction is **N = 100 for this generator**, not a replacement dataset for a different study. Independently measured ENT and IIT quantities would be needed to support a cross-theory empirical correlation. [Generator][iit]; [reported study description][manuscript].

**Effect:** corrects the attribution and count for a specified calculation, not the theory's relationship to IIT.

## D8. Protein-model provenance

**Location:** [Simulationa/protein_validation.py][protein].

The inspected script defines a simplified two-dimensional potential and a constructed FRET-like mapping. It does not load measured folding trajectories or experimental FRET observations. Its reported quantities therefore describe that synthetic construction rather than empirical protein-folding validation. The physical mapping, threshold interpretation and units need their own specification. No force field, folding definition, threshold or computational rule is changed by this note. [Source][protein].

**Effect:** identifies the model actually implemented and the evidence not supplied by it.

## D9. Reproducibility references, intervals and software environment

**Location:** K84 section 4.6, section 4.7, Table 2 and Appendix A; [baseline file inventory][inventory].

K84 prints `XXXX` as a commit placeholder and presents dataset references ending in `1234567` and `2345678`. Those strings have not been verified as the stated supporting datasets and should not be relied upon as such. Its promised `repro.sh`, `requirements.txt`, `/seeds` contents, calibration JSONs and units-crosswalk script were not located in the inspected repository inventory. This is a public-availability statement, not a claim that no private artifacts exist.

The inspected scripts also do not supply the complete reported trial, bootstrap and interval-generation analyses. Those reported statistics remain unverified until each is linked to its data, sampling unit, run settings and analysis. They are not replaced with newly invented intervals.

K84 declares a Qiskit 1.0 environment, while the [complete script][complete] uses legacy imports including `qiskit.opflow` and `qiskit.algorithms`. The [official Qiskit migration guide][qiskit-migration] documents the removal of those interfaces from the main package. This note does not migrate dependencies or assert that the existing installation instructions reproduce every script successfully. A working pinned environment and a complete execution record remain separate requirements.

**Effect:** corrects availability and reproducibility representations without inventing artifacts, changing dependencies or claiming successful execution.

## Unresolved questions are not silently decided

Different tau/resilience definitions, their signs and normalization, numerical-band universality, hysteresis interpretation, minimality of seven constraints, geometric interpretation and necessity under representation changes remain separate scientific questions. This note does not replace necessity with ordinary robustness, remove axes or domains, or treat one redundant proxy as disproof of every resilience formulation.

Likewise, this supplement does not replace Structurism with another ethics framework, equate internal coherence with moral correctness, alter SERI's guards or event conventions, or certify operational safety. Original accountability aims and explicitly provisional hypotheses remain available for testing.

A prescribed threshold can be a legitimate preregistered hypothesis. Synthetic data can test a model or algorithm. The evidence problem arises when an assumption or label-generation rule is reported as an independently discovered empirical result. Disagreements must be tested at the relevant level: theory, measurement, implementation, data or interpretation. This distinction does not excuse a failed prediction from being recorded as a failure.

## Retrieval limits and next decisions

This note does not certify the latest bytes of every PhilArchive or Zenodo record, publish corrections to those archives, or update the separate GitHub wiki. The earlier Stage-1 table allegation and ENT-Bench raw-generator/ablation allegations remain outside these errata because the necessary original evidence was not fully inspected in this review. No conclusion about those unseen materials is substituted here.

Repairing execution, choosing among mathematical definitions, restoring absent equations, changing thresholds or expanding validation requires a separately specified and approved change. Until then, this document is an errata/provenance layer only. Its existence is neither proof of ENT's empirical efficacy nor a blanket rejection of the programme.

## Source references

All repository links below identify the inspected commit, rather than a moving default branch.

[baseline]: https://github.com/MUESdummy/Emergent-Necessity-Theory-ENT/tree/0dee4f916dd5f8f594907a816a1fc0a0b847736a
[inventory]: https://api.github.com/repos/MUESdummy/Emergent-Necessity-Theory-ENT/git/trees/0dee4f916dd5f8f594907a816a1fc0a0b847736a?recursive=1
[manuscript]: https://github.com/MUESdummy/Emergent-Necessity-Theory-ENT/blob/0dee4f916dd5f8f594907a816a1fc0a0b847736a/ENT%E2%80%94%20Complete%20Manuscript.%20K84.%20%20.pdf
[complete]: https://github.com/MUESdummy/Emergent-Necessity-Theory-ENT/blob/0dee4f916dd5f8f594907a816a1fc0a0b847736a/ENT_Py.Code%20for%20Complete%20Simulations.py
[quantum]: https://github.com/MUESdummy/Emergent-Necessity-Theory-ENT/blob/0dee4f916dd5f8f594907a816a1fc0a0b847736a/Simulationa/Quantum_validation.py
[neural]: https://github.com/MUESdummy/Emergent-Necessity-Theory-ENT/blob/0dee4f916dd5f8f594907a816a1fc0a0b847736a/Simulationa/Neural_validation.py
[iit]: https://github.com/MUESdummy/Emergent-Necessity-Theory-ENT/blob/0dee4f916dd5f8f594907a816a1fc0a0b847736a/Simulationa/iit_correlation.py
[protein]: https://github.com/MUESdummy/Emergent-Necessity-Theory-ENT/blob/0dee4f916dd5f8f594907a816a1fc0a0b847736a/Simulationa/protein_validation.py
[qiskit-migration]: https://quantum.cloud.ibm.com/docs/en/migration-guides/qiskit-1.0-features
