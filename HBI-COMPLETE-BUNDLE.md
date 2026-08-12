# HBI-COMPLETE-BUNDLE
**Artifact ID:** HBI-COMPLETE-BUNDLE-001
**Version:** 2.0
**Status:** 🟢 COMPLETE & LOCKED
**Last Updated:** 2026-08-12
**Owner:** Vahid Maghsoudi

---

## Overview

This master bundle contains **all 6 core layers** of the Health & Beauty Intelligence (HBI) system, matching the architecture defined in README.md. AI agents reading this file have access to the complete HBI artifact stack in a single document.

**Layer Order:** schema → models → services → contracts → gates → knowledge

---

## 1. SCHEMA (Data Models & Core Entities)

### Core Entities

#### Product
- **product_id:** UUID
- **name:** string
- **category:** enum [skincare, haircare, wellness, nutrition]
- **ingredients:** Array of IngredientReference
- **benefits:** Array of strings
- **contraindications:** Array of strings
- **evidence_level:** enum [clinical, anecdotal, theoretical]

#### Ingredient
- **ingredient_id:** UUID
- **name:** string
- **chemical_composition:** object
- **mechanism_of_action:** string
- **safety_profile:** object
- **interaction_warnings:** Array of strings

#### SkinProfile
- **profile_id:** UUID
- **user_id:** UUID
- **skin_type:** enum [oily, dry, combination, sensitive, normal]
- **concerns:** Array of strings
- **allergies:** Array of strings
- **current_routine:** Array of ProductReference

#### Recommendation
- **recommendation_id:** UUID
- **user_profile:** SkinProfileReference
- **recommended_products:** Array of ProductReference
- **reasoning:** string
- **confidence_score:** number (0-1)
- **evidence_sources:** Array of strings

### Relationships
- **Product ↔ Ingredient** (many-to-many)
- **SkinProfile → Product** (one-to-many via Recommendation)
- **Recommendation ↔ Evidence** (many-to-many)

### Validation Rules
1. All UUIDs must be RFC 4122 compliant
2. `confidence_score` must be between 0 and 1
3. `evidence_level` must match `evidence_sources`
4. No circular dependencies in product recommendations

---

## 2. MODELS (Recommendation Logic)

### Core Logic
- **Matching:** Match SkinProfile concerns with Product benefits
- **Filtering:** Exclude products with matching contraindications or user allergies
- **Scoring:** `confidence_score = (evidence_level × match_strength)`

### Evidence Levels
- **Clinical:** Peer-reviewed studies, FDA approval
- **Anecdotal:** User testimonials, traditional use
- **Theoretical:** Hypothetical mechanisms, unproven

### Scoring Formula
