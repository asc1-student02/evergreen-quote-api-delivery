
## Go / No-Go: Merge Decision

> Copy to `delivery-leadership-package/go-no-go.md`. Make this call **from** the CI result, not in spite of it.

**Date / time:** November 9, 2026, 11:27am
**Decision:** ☐ GO   ☐ NO-GO   ☒ GO WITH CONDITIONS

## CI evidence

- Latest run on `delivery/lead`: **green** · link: [paste the Actions run URL]
- Latest run on `main` (Run #31, "Hotfix: widen the age range for the senior campaign"): **red**. It failed at the test step: the hotfix set the minimum age to 110 instead of raising the maximum, so 2 of 7 tests that create real quotes returned 400. Checkout, Node setup, the Mongo container, and the install all passed. Nothing was built or shipped from this run.
- Workflow file: `.github/workflows/ci.yml`
- What the workflow actually checked: checks out the code, sets up Node 22, installs from the lock file (`npm ci`), and runs `npm test` against a throwaway `mongo:7` service container (9 tests on `delivery/lead`; 7 in the Run #31 log)

## What "GO" would mean

- Merge `delivery/lead` → `main`, squash, delete branch.
- Tag the merge commit `phase-3`.

## What "NO-GO" would mean

- Hold the merge until: `main` is green again **and** engineering has confirmed what is deployed in front of customers and how the hotfix reached them.
- Owner of that condition: Engineering lead
- Re-evaluate at: Thursday 9:00 am check-in

## My call

Go with conditions. My branch is green and does not contain the hotfix, so my work continues; I will not merge onto a red `main`. The one thing that drove it: a red run ships nothing, so the rule rejecting customers reached them some other way, and that is a question for engineering, not something my merge can fix or worsen today. The condition for Thursday's merge is that `main` is green again and engineering has confirmed what is deployed and how the hotfix got there. It flips to no-go if `main` is still red Thursday morning, or if the investigation shows the problem touches code on my branch.

## Update: November 9, 2026, 11:47am

The incident was a simulated exercise. The Run #31 failure was a handout, not a run in this repository, so the real `main` was green when I opened the PR. My PR's CI run was green. The condition on this merge is considered met, and I merged.