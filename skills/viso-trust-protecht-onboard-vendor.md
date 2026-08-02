---
name: Onboard a vendor and start an assessment
description: Create a VISO TRUST vendor relationship by domain and kick off a risk assessment, then retrieve its summary.
api: openapi/viso-trust-protecht-openapi-original.json
operations: [createRelationshipAsCurrentUserByDomain, createAssessment, getAssessment, getAssessmentSummary]
generated: '2026-07-21'
method: generated
---

# Onboard a vendor and start an assessment

Base URL: `https://app.visotrust.com`. Authenticate every request with
`Authorization: Bearer <token>`, where the token is generated from an **Admin**
or **Program Manager** account (Contributor/Viewer tokens are rejected).

## Steps

1. **Create the relationship by domain** — `POST /api/v1/relationships/domain`
   (`createRelationshipAsCurrentUserByDomain`). Pass the vendor's domain plus
   the business case (context type) and data types shared. This anchors all
   assessments and scoring for the vendor.
2. **Start an assessment** — `POST /api/v1/assessments` (`createAssessment`)
   referencing the new relationship. VISO TRUST's Artifact Intelligence begins
   analyzing available security documents.
3. **Poll the assessment** — `GET /api/v1/assessments/{id}` (`getAssessment`)
   until it reaches a completed state. To receive completion events instead of
   polling, register a webhook for `ASSESSMENT_COMPLETED` (see the register-webhook skill).
4. **Read the summary** — `GET /api/v1/assessments/{id}/summary`
   (`getAssessmentSummary`) for the LLM-generated risk summary, or
   `GET /api/v1/assessments/{id}/summary/export` to export it as a PDF.

## Notes
- Pagination on list endpoints uses `page` and `size` query params.
- The spec documents only 200 responses; handle standard bearer-auth failures
  (401 unauthenticated, 403 insufficient role) defensively.
