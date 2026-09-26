# Historical Assets and China-Market Risk Signals in Pre-Release Domains: Research Protocol

**Markdown companion to the published AIYucha Research technical note**

- Version: 1.0
- Publication date: 2026-09-25
- Creator: AIYucha Research
- DOI: https://doi.org/10.5281/zenodo.22962144
- Zenodo record: https://zenodo.org/records/22962144
- Research page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study
- AIYucha tools: https://aiyucha.com
- License: CC BY 4.0

> The Zenodo record and its PDF are the canonical publication. This Markdown file is a repository-friendly companion that organizes the same research problem, evidence semantics, and reproducibility rules for developers and downstream researchers.

## 1. Research problem

Pre-release and previously used domains are not blank technical identifiers. They can retain public historical traces, external links, prior website content, registration/lifecycle evidence, China-market accessibility signals, and other residual information.

Those signals are useful for domain due diligence, but they are easy to overstate.

A large backlink count is not automatically a large usable asset. A missing metric is not automatically zero. A failed accessibility observation is not evidence that a domain is safe. A historical association is not a causal relationship.

The protocol therefore asks:

**How can historical-domain assets and China-market risk signals be collected and represented in a way that is useful, auditable, and reproducible without turning uncertainty into false certainty?**

## 2. Scope

The protocol is designed for domain-level research involving pre-release, previously used, or historically active domains.

The current evidence model is relevant to researchers and practitioners working on:

- domain intelligence;
- domain due diligence;
- historical website analysis;
- backlink and referring-domain analysis;
- prior-use and residual-value research;
- ICP-related public evidence;
- mainland-China accessibility;
- WeChat accessibility;
- DNS-related observations;
- multi-signal domain screening.

The protocol does not define one universal investment score or one universal risk score.

## 3. Unit of observation

The primary unit is a domain observed through one or more evidence families at a defined observation time or observation window.

A domain can have multiple evidence families with different coverage, timestamps, and statuses.

The presence of a strong observation in one family does not erase uncertainty in another family.

## 4. Evidence dimensions

The research workflow can organize evidence from the following major dimensions.

### 4.1 Registration and lifecycle

Examples include registration timing, lifecycle status, and other publicly usable domain-registration traces.

These observations establish domain-history context but do not by themselves establish current commercial value.

### 4.2 Historical website and public-web traces

Historical web evidence can show whether a domain had prior websites, what kinds of content were publicly visible, and how use changed over time.

Historical traces should be treated as observations of past public presence, not as proof that past traffic, reputation, ownership, or ranking persists today.

### 4.3 Backlinks and referring domains

Backlink research can include link counts, referring-domain counts, and other public link-profile evidence.

The protocol distinguishes the existence of historical link evidence from the stronger claim that every link is active, valuable, trustworthy, indexable, or transferable to a new use.

### 4.4 ICP-related evidence

ICP-related public records can provide China-market historical context.

Historical ICP evidence should be represented with its observed status and time context rather than simplified into an unsupported statement about current eligibility or current ownership.

### 4.5 Mainland-China accessibility

Mainland accessibility observations should preserve what was actually observed.

A mainland failure is not automatically proof of blocking. If a domain is also unavailable elsewhere, the stronger explanation may be an unavailable site, stopped service, or unreachable origin rather than China-specific blocking.

When evidence is insufficient, the state should remain unresolved.

### 4.6 WeChat accessibility

WeChat-related accessibility is represented as its own evidence family.

An unresolved or failed observation must not be recoded as a safe result.

### 4.7 DNS-related observations

DNS observations can provide useful operational and risk context, but they should remain distinct from website availability, mainland accessibility, and WeChat accessibility.

### 4.8 Residual historical assets

A previously used domain can retain combinations of historical content, link structure, search remnants, old entry points, or brand memory.

These are candidate residual assets, not guaranteed future performance.

## 5. Observation-state semantics

The most important methodological rule is to preserve state meaning.

### 5.1 Missing is not zero

A metric that was not obtained is missing.

It must not be silently converted to a numeric zero unless the measurement contract explicitly proves that zero is the observed value.

This distinction matters for summary statistics, filtering, comparisons, thresholds, and downstream modeling.

### 5.2 Unknown is not safe

An unresolved risk or accessibility state is unknown.

It must not be represented as a clean, safe, negative, or passed result.

### 5.3 Failure is not absence

A failed collection request means the observation process did not return a usable observation.

It does not prove that the underlying website, backlink, record, risk, or historical trace does not exist.

### 5.4 Observed absence is different from unobserved data

Where a source contract can explicitly state that an observed quantity is absent or zero, that result may be represented as such.

That is methodologically different from a missing or failed observation.

## 6. Correlation and causal limits

This research framework is observational.

Relationships between domain age, historical web presence, backlinks, ICP-related records, accessibility signals, DNS observations, or other variables can support descriptive and comparative analysis.

They do not by themselves establish causal effects.

Any causal claim requires a separate identification strategy, assumptions, and evidence beyond this protocol.

## 7. Research data boundary

Public research releases are limited to evidence that is explicitly marked publicly citable by the AIYucha research data path.

The public research exporter rejects payloads that are not marked `publicly_citable = true`.

The research release path is intentionally separated from internal execution metadata and secrets.

## 8. Privacy-preserving identifiers

Default public research exports pseudonymize domains.

A normalized domain is transformed into a stable HMAC-SHA256-derived identifier using a private research key.

The public identifier uses the form:

`d_<20 lowercase hexadecimal characters>`

The secret key is never included in the public repository or dataset.

Because raw domains can appear in nested strings such as URLs or embedded records, replacement is recursive rather than top-level only.

Raw-domain release is possible only as an explicit opt-in methodological choice.

## 9. Failure retention and sample integrity

The collector preserves failures in a separate JSONL file.

This prevents a cohort from silently changing from:

"all intended domains"

into:

"only the domains that happened to return successfully."

A reproducible release therefore reports at least:

- input count;
- successful record count;
- failure count;
- dataset checksum;
- failure-file checksum.

## 10. No paid-query side effect

The current public research collector reads existing Growth evidence.

It does not trigger a paid query merely to populate a research export.

The manifest records:

`paid_queries_triggered: 0`

This makes cost behavior auditable and helps keep a research export distinct from active commercial data acquisition.

## 11. Release artifacts

A complete dataset release should normally include:

- successful-record JSONL;
- failure JSONL;
- manifest JSON;
- codebook;
- methodological/reproducibility notes;
- checksums;
- analysis code or notebooks when a concrete analysis is published.

The current export contract is documented in:

- [../REPRODUCIBILITY.md](../REPRODUCIBILITY.md)
- [../CODEBOOK.md](../CODEBOOK.md)

## 12. Recommended analysis practice

Researchers using an AIYucha research export should:

1. preserve source status semantics;
2. report denominators and coverage for each evidence family;
3. distinguish zero from missing;
4. distinguish unknown from safe;
5. keep collection failures visible;
6. avoid treating all historical backlinks as equivalent usable assets;
7. avoid collapsing distinct China-market signals into one unsupported binary variable;
8. state observation windows;
9. verify SHA-256 hashes before analysis;
10. separate descriptive association from causal interpretation.

## 13. Practical domain inspection

This research protocol is connected to working domain-intelligence tools.

To inspect a real domain rather than only read the protocol:

- AIYucha: https://aiyucha.com
- Research page and tool links: https://aiyucha.com/zh/publications/pre-release-domain-risk-study

The research page links to the relevant history, backlink, ICP, mainland-access, WeChat-access, DNS, custom workflow, and deeper-analysis entry points.

## 14. Citation

Suggested citation:

AIYucha Research. (2026). *Historical Assets and China-Market Risk Signals in Pre-Release Domains: Research Protocol* (Version 1.0). Zenodo. https://doi.org/10.5281/zenodo.22962144

Machine-readable citation metadata is available at [../CITATION.cff](../CITATION.cff).

## 15. Licensing

The published technical note is licensed under Creative Commons Attribution 4.0 International.

Repository research text follows the scope described in [../LICENSE](../LICENSE).
