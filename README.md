# career-engine

An embedding-driven job-discovery and résumé-assembly pipeline. Built for myself, in public so the architecture is reviewable.

The system maps a structured candidate profile to a corpus of job descriptions using **modern semantic retrieval** (OpenAI `text-embedding-3-small`, 1536d) with a cached, reproducible scoring pipeline.

> Public scope: methods, architecture, and tooling discipline only. The candidate profile, target-company list, salary bands, and per-company fit scores are not part of this public surface.

## What's in it

- **Embeddings-as-default retrieval.** OpenAI `text-embedding-3-small` over atomic candidate units × JD corpus, with sha256-cached requests for reproducible runs and bounded cost.
- **Kind-weighted scoring.** Cosine ranking with per-source-type weighting and centroid + max-pool aggregation across heterogeneous candidate-evidence kinds.
- **Greedy submodular selection.** Diversity-aware top-k over evidence atoms — selects a set that jointly covers JD demands, not k repeats of the same point.
- **Soft title whitelist + anti-pattern filters.** Title-noise control without hard-blocking adjacent roles.
- **Reproducible diagnostics.** Iterative model refinement (`v1 → v2 …`) with stable per-pair score-deltas for every change.

## Engineering discipline

- **One-canonical-source architecture.** A single evidence-card library is informed by the union of JD demands across all targets; per-target rendering tailors framing only — fabrications are blocked at validator time.
- **Validator-first pipeline.** A LaTeX render is refused until a structural validator (claim-tier checks, banned-claims substring, schema conformance) is green.
- **Drill-card defensibility.** Every rendered bullet generates anticipated-question cards for mock interview — if a phrase can't be defended, it's cut.
- **Reproducible artifacts.** Every render pinned to spec version, code SHA, and registry build hash.

## Stack

`Python · numpy · OpenAI text-embedding-3-small · LaTeX · jsonschema` · validator + render modules · per-company strategy YAML.

## Status

Active. Used to produce the author's own application portfolio.

## Author

Hamidreza (Reza) Hasani, PhD — computational imaging + production ML.
[scholar.google.com](https://scholar.google.com/citations?user=IcdIQXUAAAAJ) · [github.com/iHamidHasani](https://github.com/iHamidHasani)
