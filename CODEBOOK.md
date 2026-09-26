# AIYucha Research Export Codebook

This codebook documents the current public research-export contract implemented by AIYucha Research.

Protocol DOI: https://doi.org/10.5281/zenodo.22962144

Research page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study

Current manifest schema: `aiyucha-research-export-v1`

## Scope

The exporter reads existing AIYucha Growth evidence and only accepts a payload when:

`publicly_citable == true`

It does not trigger a paid query to fill missing evidence.

The default release mode pseudonymizes domains. Raw domains are retained only when the export is explicitly run with `--include-domain`.

## Input file

The CLI input is a UTF-8 text file with one domain per line.

Blank lines and lines beginning with `#` are ignored.

Each remaining domain is normalized before collection and before subject-ID generation.

## Successful record JSONL

Each successful line in the dataset JSONL is one JSON object.

### `subject_id`

Type: string

Always present.

Default form:

`d_<20 lowercase hexadecimal characters>`

It is derived from the normalized domain using HMAC-SHA256 with a private research key. The public value contains only the prefix plus the first 20 hex characters of the digest.

The same normalized domain and the same research key produce the same `subject_id`.

### `source`

Type: string

Current value:

`AIYucha Growth API`

This value is set by the research exporter.

### `publicly_citable`

Type: boolean when retained from the source payload.

A record is eligible for export only if the source payload had this field set to `true`.

### `domain`

Type: string

Default: absent.

Present only when the exporter is intentionally run with `--include-domain`.

When domain inclusion is disabled, the top-level raw domain is removed and occurrences of the same domain inside nested string values are recursively replaced with `subject_id`.

### `observation_id`

Not published.

The source `observation_id` is explicitly removed during sanitization.

### Evidence fields

The remaining evidence fields are the publicly citable fields supplied by the AIYucha Growth evidence contract after recursive sanitization.

The exporter deliberately does not flatten every evidence family into one fixed table. This allows historical, backlink, ICP-related, mainland-access, WeChat-access, DNS, and other public evidence objects to retain their source structure.

For any concrete dataset release, the release notes should state which evidence families are present and the observation window used.

## Removed fields

The exporter recursively removes keys in its execution/secret denylist. Current categories include:

- provider and provider-status fields;
- execution backend/path fields;
- node, worker, job, task, attempt, and trace identifiers;
- cache, proxy, gateway, relay, and upstream details;
- API cost fields;
- token, secret, password, and authorization fields;
- internal error type, diagnostics, and detailed execution metadata.

These fields are operational metadata, not public research evidence.

## Failure JSONL

Failures are written separately so a research sample does not silently shrink.

### `subject_id`

Type: string

Always present.

Uses the same HMAC-derived identifier rule as a successful record.

### `status_code`

Type: integer

Present for HTTP-status failures.

### `reason`

Type: string

For HTTP status failures:

`growth_api_http_error`

For handled request, validation, or runtime failures, the value is the exception class name rather than internal diagnostic detail.

## Manifest JSON

The manifest is a single JSON object.

### `schema`

Type: string

Current value:

`aiyucha-research-export-v1`

### `input_count`

Type: integer

Number of non-empty, non-comment input domains after input parsing.

### `record_count`

Type: integer

Number of successful records written to the dataset JSONL.

### `failure_count`

Type: integer

Number of failure records written to the failure JSONL.

Expected relationship for the current single-pass collector:

`input_count = record_count + failure_count`

### `paid_queries_triggered`

Type: integer

Current invariant:

`0`

The research collector reads existing public evidence and does not invoke the paid-query path.

### `pseudonymized`

Type: boolean

`true` by default.

`false` only when the exporter is intentionally run with `--include-domain`.

### `dataset_sha256`

Type: string

Lowercase SHA-256 hex digest of the exact dataset JSONL file bytes.

### `failures_sha256`

Type: string

Lowercase SHA-256 hex digest of the exact failure JSONL file bytes.

## State semantics

This codebook does not redefine source evidence states into a single global score.

Use these rules when analyzing exported evidence:

- missing is not zero;
- unknown is not safe;
- failure is not absence;
- an observed association is not a causal conclusion.

Where a release contains an explicit evidence status, preserve that status in analysis rather than forcing it into a binary safe/unsafe or present/absent variable.

## JSONL and hashing details

Successful and failure records are UTF-8 JSONL with one object per line.

Keys are serialized in deterministic sorted order.

SHA-256 values in the manifest are calculated from the exact file bytes after writing.

## Versioning

This document describes the current `aiyucha-research-export-v1` contract.

If the exporter changes in a way that alters field meaning, pseudonymization semantics, failure semantics, or manifest structure, the public schema identifier and codebook should be revised together.

## Related resources

- Protocol DOI: https://doi.org/10.5281/zenodo.22962144
- Research page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study
- AIYucha tools: https://aiyucha.com
- Reproducibility notes: [REPRODUCIBILITY.md](REPRODUCIBILITY.md)
