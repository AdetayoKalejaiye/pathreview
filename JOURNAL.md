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

**Reproduction commit link:** https://github.com/AdetayoKalejaiye/pathreview/commit/6171fe1

**Reproduction summary:**
Added test `test_create_review_missing_ownership_check()` documenting the vulnerability: `create_review()` service accepts any `profile_id` without verifying it belongs to the current user. Unlike `get_review()` and `list_reviews()` which join with Profile and filter by user ownership, `create_review()` has no ownership check.

**PLAN.md link:** [PLAN.md](./PLAN.md)

**Walkthrough video (recommended):** (Not recorded)

**Blockers or open questions:**
- Clarify if non-existent profile should return 403 or 404
- Check if background task `process_review()` needs ownership verification too

## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
- ✅ Sub-task 1: Added ownership verification to `create_review()` service function
  - Queries Profile by id and verifies `profile.user_id == user_id`
  - Returns None if ownership check fails
- ✅ Sub-task 2: Updated `create_review_endpoint()` to handle ownership verification
  - Checks if `create_review()` returns None
  - Raises HTTPException with 403 Forbidden status code
- ✅ Sub-task 3 (partial): Added comprehensive tests
  - `test_create_review_rejects_wrong_owner`: Verifies ownership check blocks attacker
  - `test_create_review_allows_owner`: Verifies owner can create reviews
  - `test_create_review_returns_none_for_nonexistent_profile`: Verifies non-existent profile handling

**Next steps:**
- Run make check and make test-unit to verify all tests pass
- Get peer/mentor feedback on draft PR
- Finalize PR and submit

**Blockers:**
None - implementation on track