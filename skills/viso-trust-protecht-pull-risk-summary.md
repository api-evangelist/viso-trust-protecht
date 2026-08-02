---
name: Look up a vendor's risk summary
description: Resolve a vendor in the VISO TRUST directory and pull its risk summary and external intelligence reports.
api: openapi/viso-trust-protecht-openapi-original.json
operations: [getVendorDirectoryByDomainOrUrl, getVendorRiskSummaryByNameOrDomain, getIntelligenceReportsByVendor]
generated: '2026-07-21'
method: generated
---

# Look up a vendor's risk summary

Base URL: `https://app.visotrust.com`. Send `Authorization: Bearer <token>` on
every request.

## Steps

1. **Resolve the vendor** — `GET /api/v1/directory/search`
   (`getVendorDirectoryByDomainOrUrl`) with the vendor's domain or URL to find
   its VISO TRUST vendor profile.
2. **Get the risk summary** — `GET /api/v1/vendors/risk-summary`
   (`getVendorRiskSummaryByNameOrDomain`) by name/domain, or
   `GET /api/v1/vendors/{id}/risk-summary` (`getVendorRiskSummaryById`) when you
   already hold the vendor id. Returns aggregate control-domain summaries and the
   relationships you hold with the vendor.
3. **Pull external intelligence** — `GET /api/v1/external-intelligence-reports/vendor/{vendorDomain}`
   (`getIntelligenceReportsByVendor`) to list BitSight / Recorded Future /
   SecurityScorecard reports, or `.../latest/{source}` (`getLatestIntelligenceReport`)
   for the newest from one source.

## Notes
- The risk summary is read-only; use the onboard-vendor skill to create a
  relationship and drive a full assessment.
