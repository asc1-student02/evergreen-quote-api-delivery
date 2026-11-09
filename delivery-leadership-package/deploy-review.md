# Deploy Review: Evergreen Site (S3 Path)

**Date:** 11-9-2026
**Author:** Angela Jeske
**Scope:** Review of the marketing site's deploy artifacts. No AWS account used; no live deploy performed.

## Artifacts reviewed

- `deploy/infrastructure.md`
- `deploy/bucket-policy.json`
- `deploy/iam-policy.json`
- `deploy/deploy-to-s3.sh` (syntax check with `bash -n`: no output, exit code 0, parses)
- Local preview of `site/` at http://localhost:8080

## What does it do?

The deploy copies four static files (`index.html`, `styles.css`, `app.js`, `quotes.json`) into one S3 bucket with static website hosting turned on. That publishes the Evergreen page at a public web address with no server to patch or scale. It does not provide HTTPS, a custom domain, or edge caching. Those would come with CloudFront in production, which is out of scope this week.

## Who can read?

Everyone on the internet, by design. The bucket policy grants one action, `s3:GetObject`, to all principals, on the objects in this one bucket. Visitors can download pages but cannot list, change, or delete anything.

## Who can write?

Only an identity that has the deploy policy attached. The policy allows upload, delete, and list (`s3:PutObject`, `s3:DeleteObject`, `s3:ListBucket`) on the `evergreen-quote-site` bucket only. It grants nothing on other buckets, servers, or services. The files do not say which person, role, or pipeline holds this policy.

## Findings and follow-up questions

1. **Bucket name mismatch.** The bucket policy uses the placeholder `BUCKET-NAME` while the deploy policy names `evergreen-quote-site`. Question for the engineering owner: confirm the real bucket name and that both policies use it before any live deploy.
2. **Unknown holder of write access.** Question for the engineering owner: which role or pipeline holds the deploy policy, and who can assume it?
3. **Site and API disagree on price.** In the local preview, the site showed $400.00 for auto, age 35, $50,000 coverage, while the API returns $450 at the sponsor's rates. The site's script still has the old rates and does not call the API yet. Logged as risk R3 in the risk register; proposed roadmap fix: the site calls the API so there is one source of rates.
4. **Recent-quotes panel is static.** The panel shows hard-coded sample quotes, not live data from the API.

## Decision

The review is complete for the required path. No live deploy this week unless the instructor confirms there is time. Nothing in the artifacts blocks a live deploy once finding 1 is resolved.