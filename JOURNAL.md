## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/163

**Issue title:** Review creation does not verify profile ownership

**Tier:** [x] Tier 2

**Problem summary:**
The POST /reviews endpoint accepts an authenticated user's request but doesn't verify that the profile belongs to that user. An attacker can create reviews on any profile by supplying another user's profile ID. The fix should add ownership checks to create_review(), matching the scoping already used in get_review() and list_reviews().

**Branch name:** fix/163-review-profile-ownership

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/ascherj/pathreview/commit/6171fe1

**Reproduction summary:**
Added test `test_create_review_missing_ownership_check()` documenting the vulnerability: `create_review()` service accepts any `profile_id` without verifying it belongs to the current user. Unlike `get_review()` and `list_reviews()` which join with Profile and filter by user ownership, `create_review()` has no ownership check.

**PLAN.md link:** [PLAN.md](./PLAN.md)

**Walkthrough video (recommended):** (Not recorded)

**Blockers or open questions:**
- Clarify if non-existent profile should return 403 or 404
- Check if background task `process_review()` needs ownership verification too