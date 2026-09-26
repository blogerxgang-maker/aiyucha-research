# Reproducibility

This document describes the reproducibility contract used by AIYucha Research for public domain-intelligence releases associated with:

**Historical Assets and China-Market Risk Signals in Pre-Release Domains: Research Protocol**

DOI: https://doi.org/10.5281/zenodo.22962144

Research page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study

## Reproducibility objective

The goal is not merely to export a table. A release should make it possible to answer which domain cohort was intended, which observations were actually obtained, which requests failed, whether raw domains were retained or pseudonymized, whether publication triggered any paid data acquisition, and what exact bytes were released.

The workflow therefore preserves missingness and failures instead of silently shrinking the sample.

## Evidence input boundary

The research exporter reads existing AIYucha Growth evidence only when the payload is explicitly marked `publicly_citable = true`.

A payload that is not marked publicly citable is rejected from the public research export.

The export collector does not call the paid-query path. The release manifest records:

`paid_queries_triggered: 0`

This is an invariant of the current exporter, not an estimate.

## Domain normalization and pseudonymization

Input domains are normalized before collection.

By default, raw domain names are not retained in the released dataset. Each normalized domain is transformed into a stable subject identifier using HMAC-SHA256 and a private research key:

`subject_id = "d_" + first_20_hex(HMAC_SHA256(secret, normalized_domain))`

The HMAC key is an operational secret. It is not committed to Git and is not part of a public release.

Because a raw domain can appear inside nested strings such as URLs or record payloads, sanitization is recursive. When pseudonymization is enabled, case-insensitive occurrences of the raw domain inside nested public values are replaced with the same `subject_id`.

The CLI has an explicit `--include-domain` option for releases where retaining domains is an intentional methodological choice. Default behavior remains pseudonymized.

## Public-field sanitization

The exporter removes execution-only or secret-bearing metadata from mappings before release. The current denylist covers categories such as execution/provider metadata; node, job, task, attempt, and trace identifiers; cache/proxy/gateway/relay/upstream details; API cost fields; credentials and authorization values; and internal diagnostics.

The source `observation_id` is also removed.

Each successful public record receives `subject_id`, `source` (currently `AIYucha Growth API`), and the remaining publicly citable evidence fields after recursive sanitization.

## Failure preservation

A failed observation is not silently dropped.

Failures are written to a separate JSONL artifact. Each failure contains `subject_id`. HTTP failures also contain `status_code` and use the reason `growth_api_http_error`. Request, validation, or runtime failures retain a compact reason based on the exception class rather than internal diagnostic detail.

This makes sample attrition auditable.

## Release files

For an output path such as `pilot.jsonl`, the exporter produces:

- `pilot.jsonl` — successful public records;
- `pilot.jsonl.failures.jsonl` — failure records;
- `pilot.jsonl.manifest.json` — release manifest.

JSONL records are written as UTF-8, one JSON object per line, with deterministic key sorting.

## Manifest

The current manifest schema is `aiyucha-research-export-v1`.

It records:

- `input_count`
- `record_count`
- `failure_count`
- `paid_queries_triggered`
- `pseudonymized`
- `dataset_sha256`
- `failures_sha256`

See [CODEBOOK.md](CODEBOOK.md) for field-level definitions.

## Integrity verification

SHA-256 is computed over the exact bytes of the dataset JSONL and failure JSONL files. A downstream user should verify both hashes before analysis. Any change to whitespace, line ordering, field values, or file encoding changes the checksum.

## Analysis rules

**Missing is not zero.** An unobserved metric must not be silently recoded as a factual zero.

**Unknown is not safe.** An unresolved risk or accessibility state must not be converted into a clean or negative finding.

**Failure is not absence.** A failed request indicates that the observation process did not return a usable record; it does not establish that the underlying phenomenon is absent.

**Correlation is not causation.** Observed relationships among domain age, historical traces, backlinks, accessibility signals, ICP-related evidence, or other features do not themselves establish causal effects.

## Practical replication with AIYucha

The public research assets describe the method. To inspect a real domain using the same product family, use:

- Research page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study
- AIYucha tools: https://aiyucha.com

The research page links to the relevant history, backlink, ICP, mainland-access, WeChat-access, DNS, custom workflow, and deeper-analysis entry points.

## Release checklist

1. Freeze the intended cohort and input list.
2. Confirm the exporter uses existing `publicly_citable` evidence only.
3. Export with pseudonymization unless raw-domain publication is an explicit research choice.
4. Inspect the failure JSONL instead of dropping failed observations.
5. Confirm no raw domain remains in the pseudonymized output.
6. Confirm internal or secret-bearing fields are absent.
7. Verify the manifest counts.
8. Verify SHA-256 values against the released files.
9. Publish the codebook and methodological notes with the data.
10. Cite DOI 10.5281/zenodo.22962144 and link the AIYucha research page.
