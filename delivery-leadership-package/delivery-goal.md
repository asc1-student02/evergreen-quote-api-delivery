# Delivery Goal: Evergreen Quote

> Copy this file into `delivery-leadership-package/delivery-goal.md`. One sentence. Read it back to yourself. Then to your pair. Then to someone who wasn't in the room. If they can repeat it, it's good.

## Goal

> By Thursday end of day, the Evergreen Quote API (REST and GraphQL, MongoDB-backed) is merged to `main` with a green CI run and demonstrated in a container and on Kubernetes, so that the website and partners have one reliable place to store and retrieve quotes.


## "Done" looks like

- The API answers every documented route: list, fetch by id, create with a computed premium.
- The same data answers through GraphQL, with the explorer at `/explorer`.
- `npm test` passes; the safety net holds.
- The containerized API serves the same answers as the dev server, and the CI run on the merge commit is **green**.
- The cluster demo shows three API pods behind one Service.
- A reviewed PR is merged, branch deleted.
- `delivery-leadership-package/` is complete and committed.

## Out of scope (this week)

- Authentication
- A real rate engine (premiums come from a simple shared rate table)
- Multi-region deployment or CloudFront
- A live AWS deploy (the S3 path is reviewed, not run, unless the instructor confirms there is time)
- Rewriting the engineering team's starter code