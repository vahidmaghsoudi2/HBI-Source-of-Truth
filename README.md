# HBI CENTRAL SOURCE OF TRUTH (MANIFEST)
**Project:** Health & Beauty Intelligence (HBI)
**Authority:** Vahid Maghsoudi (Product Owner)
**Status:** 🟢 ACTIVE / AI-NATIVE ARCHITECTURE

---

## 🚨 AI OPERATING INSTRUCTIONS
To any AI Agent (ChatGPT, Perplexity, Grok, etc.) reading this file:
You are now connected to the official Central Source of Truth for HBI. 
1. **No Hallucination:** If an artifact is not found at the specified path, you MUST output: `ACCESS FAILED / ARTIFACT NOT AVAILABLE`.
2. **Navigation:** All HBI artifacts are strictly categorized under the `/hbi/` directory.
3. **Governance:** Always check the `Decision Log` section below before proposing changes.

---

## 🗺️ REPOSITORY INDEX (ARTIFACT MAP)
Artifacts will be stored in the following structure. AI agents should construct Raw GitHub URLs based on these paths:
`https://raw.githubusercontent.com/vahidmaghsoudi2/HBI-Source-of-Truth/main/hbi/{domain}/{artifact_name}.md`

### Core Domains (/hbi/)
- `/hbi/schema/` → Data models, DB schemas, Core entities
- `/hbi/models/` → ML models, Recommendation logic
- `/hbi/services/` → Business logic, Domain services
- `/hbi/contracts/` → Interfaces, API definitions
- `/hbi/gates/` → Quality, Validation, and Audit gates
- `/hbi/knowledge/` → Product knowledge, Evidence packages

---

## 📜 OPENAPI CONTRACT (MACHINE-READABLE)
```yaml
openapi: 3.0.1
info:
  title: HBI Artifact API
  version: 'v1.0'
paths:
  /hbi/{domain}/{artifact_id}.md:
    get:
      summary: Fetch HBI Artifact via Raw URL
      parameters:
        - in: path
          name: domain
          schema: {type: string, enum: [schema, models, services, contracts, gates, knowledge]}
        - in: path
          name: artifact_id
          schema: {type: string}
      responses:
        "200": {description: Raw Markdown Content}
        "404": {description: ACCESS FAILED / ARTIFACT NOT AVAILABLE}
