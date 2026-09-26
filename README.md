# AIYucha Research

**Reproducible research assets, methods, and datasets for domain intelligence and domain due diligence.**

AIYucha Research documents how historical domain assets and China-market risk signals can be collected, represented, and interpreted without turning missing observations into false zeros or unknown states into false safety.

- **DOI:** https://doi.org/10.5281/zenodo.22962144
- **Research page:** https://aiyucha.com/zh/publications/pre-release-domain-risk-study
- **AIYucha tools:** https://aiyucha.com
- **Zenodo record:** https://zenodo.org/doi/10.5281/zenodo.22962144

> Want to inspect a real domain rather than only read the protocol? Use the live domain-intelligence tools at **https://aiyucha.com**. The research page links directly to the relevant history, backlink, ICP, mainland-access, WeChat-access, DNS, custom-workflow, and deeper-analysis entry points.

## What this project studies

Pre-release and previously used domains often carry historical assets and historical risk signals at the same time. A domain may retain years of public web history, backlinks, referring domains, prior registration or ICP traces, search remnants, brand memory, and other externally observable evidence. At the same time, some signals can be unavailable, contradictory, stale, or simply not observed.

The project therefore focuses on a practical research problem:

**How can multi-source domain evidence be represented reproducibly without overstating what the evidence proves?**

The initial technical note is:

**Historical Assets and China-Market Risk Signals in Pre-Release Domains: Research Protocol**

Permanent identifier: **10.5281/zenodo.22962144**

## Evidence dimensions

The current protocol and AIYucha research workflow organize evidence across several domain-intelligence dimensions, including:

- registration and lifecycle history;
- historical website and public web traces;
- backlinks and referring-domain evidence;
- ICP-related public records;
- mainland-China accessibility signals;
- WeChat accessibility signals;
- DNS-related observations;
- historical asset and residual-value indicators.

These dimensions are not treated as a single infallible score. Each observation has its own coverage, status, timestamp, and evidentiary limits.

## Why `missing != 0`

A missing value means that the workflow did not obtain a usable observation for that field. It does **not** mean the underlying quantity is zero.

For example, if a backlink metric is unavailable in a particular export, encoding it as `0` would silently convert an observation failure or coverage gap into a factual statement about the domain. That can bias descriptive statistics, comparisons, thresholds, and downstream models.

The research assets therefore preserve missingness explicitly.

## Why `unknown != safe`

An unknown risk state is not evidence of safety.

If a mainland-access, WeChat-access, DNS, or related signal cannot be determined, the correct representation is an unresolved observation with its own status—not a negative finding and not a clean bill of health.

This matters because false-safe recoding can be more damaging than simply retaining uncertainty.

## Correlation is not causation

Observed associations between historical assets, access signals, backlink structure, prior use, or other domain characteristics do not by themselves establish causal relationships.

The protocol is designed for reproducible observation and comparison. Any causal interpretation requires a separate identification strategy and supporting evidence.

## Public and non-public data boundary

This repository is for **publicly citable research assets**.

Research exports are designed to use already-available, publicly citable Growth evidence. The export path does not automatically trigger paid queries merely to populate a research dataset.

Where domain-level examples require privacy-preserving publication, the exporter can replace raw domains with stable HMAC-SHA256-derived subject identifiers. Recursive sanitization is used so that original domains do not remain embedded inside nested URLs or record structures.

Internal operational details are not research data and are excluded from public exports. Examples include provider identifiers, node/job identifiers, tokens, costs, internal diagnostics, and similar execution metadata.

Failure observations are retained separately rather than silently discarded.

## Reproducible workflow

A typical research release follows this sequence:

1. Define the domain cohort and observation window.
2. Read existing publicly citable domain evidence.
3. Preserve each evidence dimension with explicit status and timestamp semantics.
4. Separate missing, unknown, failed, and observed states.
5. Pseudonymize domain identifiers when the release design requires it.
6. Recursively sanitize nested records.
7. Preserve failure records.
8. Generate a manifest describing the export.
9. Compute SHA-256 checksums for released artifacts.
10. Publish the protocol, codebook, dataset notes, and analysis assets together.

See [REPRODUCIBILITY.md](REPRODUCIBILITY.md) and [CODEBOOK.md](CODEBOOK.md) for the repository-level documentation.

## Using AIYucha on a real domain

The protocol is connected to a working domain-intelligence product rather than being only a conceptual paper.

- Research landing page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study
- AIYucha homepage and tools: https://aiyucha.com
- Custom multi-signal workflow and deeper domain analysis are linked from the research page.

AIYucha supplies the research tooling, evidence organization, and reproducibility path used by this project. Researchers, domain investors, SEO practitioners, and site operators can use the live tools to inspect real domains and compare the protocol's concepts with actual observations.

## Planned research releases

This repository will grow only as real assets are ready. Planned additions include:

- a pilot dataset release produced from the research-export workflow;
- a versioned codebook/data dictionary;
- reproducible analysis scripts or notebooks where appropriate;
- release manifests and SHA-256 checksums;
- methodological notes created from observed data-quality issues.

Planned items are not represented as already published datasets.

## Suggested citation

AIYucha Research. (2026). *Historical Assets and China-Market Risk Signals in Pre-Release Domains: Research Protocol* (Version 1.0). Zenodo. https://doi.org/10.5281/zenodo.22962144

Machine-readable citation metadata is available in [CITATION.cff](CITATION.cff).

## License

Unless a file states otherwise, the research text and documentation in this repository are made available under **Creative Commons Attribution 4.0 International (CC BY 4.0)**, aligned with the Zenodo technical note.

Future software code, if published, may carry a separate software license stated in the relevant file or directory. A documentation/content license is not automatically asserted as a software license.

See [LICENSE](LICENSE).

## Project links

- AIYucha Research page: https://aiyucha.com/zh/publications/pre-release-domain-risk-study
- AIYucha: https://aiyucha.com
- DOI: https://doi.org/10.5281/zenodo.22962144
- Zenodo: https://zenodo.org/doi/10.5281/zenodo.22962144

---

## 中文说明

AIYucha Research 是爱域查围绕域名历史资产、外链、备案、中国大陆访问、微信访问、DNS 等证据开展的公开研究与复现项目。这里强调一个很朴素但经常被忽略的原则：**缺失值不是 0，未知状态也不等于安全。**

如果你想直接检查一个真实域名，不必只读研究协议，可以进入 **https://aiyucha.com** 使用对应工具；研究背景、DOI 和各工具入口集中在：

https://aiyucha.com/zh/publications/pre-release-domain-risk-study
