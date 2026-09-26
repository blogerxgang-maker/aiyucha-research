# Pilot Analysis Plan

Status: planned, not yet executed  
Target sample size: 100 domains  
Protocol DOI: https://doi.org/10.5281/zenodo.22962144  
Research page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study

This document freezes the analysis rules for the first 100-domain AIYucha Research pilot before a pilot dataset is published. It is an operational analysis plan, not a formal preregistration.

## Purpose

The pilot is intended to test whether the research-export contract, evidence-state semantics, and descriptive analysis workflow remain usable when applied to a fixed cohort rather than a one-record smoke test.

The pilot is not designed to estimate the value of all domains, establish causal effects, or validate a universal domain-investment score.

## Cohort rule

The 100-domain cohort must be selected from a fixed, publicly describable source using a rule that does not depend on AIYucha evidence values or research outcomes.

The source, retrieval date, ordering rule, inclusion/exclusion rules, and final input-file SHA-256 must be recorded before the evidence export is analyzed.

Domains must not be selected because they already appear to have strong backlinks, favorable accessibility states, known historical value, or unusually complete AIYucha records.

If the fixed source yields invalid or non-domain entries, exclusions must be mechanical and documented before evidence inspection.

## Evidence acquisition boundary

The pilot export must use the existing AIYucha research exporter.

Only Growth evidence explicitly marked:

`publicly_citable = true`

is eligible for successful research records.

The export must not trigger paid queries merely to fill missing pilot observations.

The release manifest must report:

`paid_queries_triggered: 0`

Any domain for which a usable public record cannot be obtained remains part of the intended cohort and is represented through the failure artifact rather than silently removed.

## Identifier policy

Default publication mode is pseudonymized.

Raw domains are normalized and transformed into stable HMAC-SHA256-derived `subject_id` values using the private research key. The key is not published.

The public release must be checked for residual raw-domain strings, including raw domains embedded in nested URLs or record values.

Raw domains may be published only if a later release explicitly states that retaining them is methodologically necessary and appropriate.

## Frozen state semantics

The pilot analysis must preserve these distinctions:

- missing is not zero;
- unknown is not safe;
- failure is not absence;
- observed absence is different from an unobserved value;
- association is not causation.

No analysis step may silently coerce missing, unknown, or failed states into a favorable or unfavorable binary outcome.

## Primary pilot outputs

The first pilot report should be descriptive.

For each evidence family actually present in the released records, report:

1. the intended cohort denominator;
2. successful observation count;
3. missing or unavailable count where the evidence contract exposes it;
4. unknown/unresolved count where applicable;
5. failure count;
6. coverage rate using an explicitly stated denominator;
7. descriptive distributions for quantitative fields only among observations for which those fields are actually observed.

Evidence families may include registration/lifecycle history, historical web traces, backlink/referring-domain evidence, ICP-related evidence, mainland-China accessibility, WeChat accessibility, DNS observations, and other publicly citable fields present in the Growth contract.

The pilot must not invent fields merely to make every evidence family symmetrical.

## Secondary exploratory analysis

Exploratory comparisons may examine whether observed historical-asset indicators co-occur with other evidence states.

Any such comparison must:

- report its usable sample size;
- identify variables with substantial missingness;
- avoid causal wording;
- avoid presenting a single composite score as a validated outcome;
- be clearly labeled exploratory.

No ranking model, predictive model, or causal model is a required output of the first pilot.

## Failure and attrition accounting

The intended cohort size is 100.

For the current single-pass exporter, the release should satisfy:

`input_count = record_count + failure_count`

If this equality does not hold, the release must be investigated before publication.

Failure reasons remain compact and non-secret. Internal execution diagnostics, provider identifiers, job IDs, node IDs, tokens, costs, and similar operational fields must not be added to the public release.

## Reproducibility artifacts

A publishable pilot release should include:

- frozen input-source description and input-file SHA-256;
- successful-record JSONL;
- failure JSONL;
- manifest JSON;
- CODEBOOK.md;
- REPRODUCIBILITY.md;
- analysis script or notebook;
- generated tables/figures used in the pilot report;
- environment/dependency information sufficient to rerun the analysis;
- SHA-256 checksums for released data artifacts.

The canonical research protocol remains DOI 10.5281/zenodo.22962144.

## Interpretation limits

The pilot tests the workflow and produces descriptive evidence for its fixed cohort.

It must not be generalized beyond the cohort without an explicit sampling argument.

A high backlink count is not automatically a high-value transferable asset. Historical website presence is not proof of current traffic or reputation. An unresolved accessibility state is not evidence of safety. Associations among observed evidence dimensions do not establish causality.

## Publication rule

The pilot dataset and analysis should be released only after:

- the cohort rule has been frozen;
- the export manifest passes integrity checks;
- pseudonymization checks pass;
- failure accounting is complete;
- analysis code reproduces the published tables/figures from the released artifacts.

Until those conditions are met, the repository should describe the pilot as planned rather than published.

## Practical tooling

Readers who want to inspect a real domain with AIYucha can use:

- https://aiyucha.com
- https://aiyucha.com/zh/publications/pre-release-domain-risk-study

Repository reproducibility documentation:

- [REPRODUCIBILITY.md](REPRODUCIBILITY.md)
- [CODEBOOK.md](CODEBOOK.md)
- [docs/protocol.md](docs/protocol.md)
