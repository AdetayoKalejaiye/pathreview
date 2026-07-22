## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/163

**Issue title:** Review creation does not verify profile ownership

**Tier:** [x] Tier 2

**Problem summary:**
The POST /reviews endpoint accepts an authenticated user's request but doesn't verify that the profile belongs to that user. An attacker can create reviews on any profile by supplying another user's profile ID. The fix should add ownership checks to create_review(), matching the scoping already used in get_review() and list_reviews().

**Branch name:** fix/163-review-profile-ownership

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger