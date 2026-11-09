# Delivery Review: Evergreen Quote
## Slide 1: Delivery goal & did we hit it?

- Hit? ☒ Yes  ☐ Partially  ☐ No
- Goal: By Thursday end of day, the Evergreen Quote API (REST and GraphQL, MongoDB-backed) is merged to `main` with a green CI run and demonstrated in a container and on Kubernetes, so that the website and partners have one reliable place to store and retrieve quotes.
- Why: The API is merged to `main` through a reviewed PR with green CI, and runs in a container and on a three-pod local cluster. The live S3 deploy was reviewed, not run, as planned.

## Slide 2: What shipped

A curl transcript or screenshot of the running Evergreen Quote API on `main`: the health route and one quote response.
  - `GET /` → `{"message":"Evergreen Quote API","status":"ok"}`
  - `GET /api/quotes` → the six seeded quotes
  - Cluster: `POST /api/quote` (home, age 45, $200,000) → `monthlyPremium: 2700`
- **By the numbers:** 9 of 9 tests passing · 3 of 3 API pods Running behind one Service · 6 of 6 seeded quotes returned
- Link to the merged PR: https://github.com/asc1-student02/evergreen-quote-api-delivery/pull/19
- Link to the green CI run (install from the lock file + tests against a throwaway database): (https://github.com/asc1-student02/evergreen-quote-api-delivery/actions/runs/42674881010)

## Slide 3: Two key decisions

- **Decision 1:** Said no to renters coverage this week and scheduled it for the next round. Why it mattered: it needs a sponsor-approved rate and touches six places, and it would have put Thursday's delivery at risk.
**Decision 2:** Shipped this week on the current base image and will upgrade next week. Why it mattered: the flagged issue is moderate severity, the API is not internet-exposed this week, and holding would have blocked the container build and cluster demo.

## Slide 4: Risks & injects

- Top risk we tracked: The API returned a tidy 201 while the premium was wrong ($0.35 for $50,000). The tests caught it; the demo could not. (R1 in `risk-register.md`)
- Inject #1 (Tue): The sponsor asked for renters coverage plus a flagged base image. I said no to renters with a next-round slot, asked for the rate by a stated time, and recommended shipping on the current image.
- Inject #2 (Wed): Customers were rejected by an age minimum of 110 and `main` was red. I did not touch the validator. I asked engineering what was deployed and whether the hotfix went around the pipeline, since a red run ships nothing. Go/no-go: go with conditions.

## Slide 5: What I'd do differently next round

- **Settle the rates before the work starts.** The site still quoted $400 while the API quoted $450, and renters stalled for lack of an approved rate. Next round I'd get every rate approved first, and make the site call the API so there is one source of prices.
- **Protect the gate.** The incident showed a bad change can reach customers around a red pipeline. I'd ask who holds deploy permission, and turn on branch protection for `main` so only green runs can ship.
- **Clear the stage before every demo.** Stale processes holding port 3000 cost me time more than once. I'd add a pre-demo checklist: free ports, a seeded database, and no leftover containers.

## Q&A prep: likely questions

- "Why didn't you ship renters?" It needs a sponsor-approved rate and touches six places. I didn't want to put an unapproved price in front of a partner.
- "The demo returned quotes all week; why does one red test matter?" The demo returned a clean 201 with a $0.35 premium. A demo shows that something responds; a test checks that the answer is right.
- "Why didn't you fix the validator during the incident?" Fixing it wasn't my role. My job was to find out what was actually deployed, who owned the next step, and whether to keep merging.
- "Why go with conditions rather than no-go?" My branch was green and didn't contain the hotfix, so holding it gave customers nothing. The condition protected the merge.
- "What would you cut if Thursday came early?" The live S3 deploy first, then GraphQL for partners.
