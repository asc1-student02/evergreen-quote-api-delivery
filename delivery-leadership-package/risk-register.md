# Risk Register

> Copy to `delivery-leadership-package/risk-register.md`. At least 5 rows. **No boilerplate**; your peers will grade you on whether these are real.

|
#
| Risk | Owner | Likelihood (L/M/H) | Impact (L/M/H) | Mitigation | Trigger to escalate |

  R1 | The API returns tidy 201s while a number inside is wrong. The AI-drafted POST handler returned a clean 201 with a $0.35 Premium for $50,000 of auto coverage, and the demo looked fine. | Angela Jeske (Delivery Lead) | M | H | Run `npm test`
 after every assembly step, not just before merge. CI runs the suite on every push. The premium test checks the API against the shared rate table, so it holds up when rates change. | Any red test on `delivery/lead` or `main` → hold the push and name it at check-in |
 | R2 | Bad data outlives bad code. The $0.35 quote created before the fix is still in the database after the route was corrected. | Engineering team | H | M | Logged here. `npm run seed`resets to the six known quotes before Thursday's cluster demo. For a real system: query for and correct affected records, not just fix the code. | A bad record shows up in any demo or in the cluster database → stop and reset before presenting |
| R3 | The site and the API quote different prices. The marketing site's script still carries the old rates while the API now uses the sponsor's (auto 90, home 135, life 70). | Website team (engineering lead to confirm) | H | M | Treat as a roadmap item: the site calls the API so there is one source of rates. Until then, state the mismatch in demos and in the status update. | Anyone outside the team sees the site and the API disagree → raise with the sponsor the same day |
| R4 | The container and the cluster behave differently from the dev server. They are separate environments, and only environment variables carry configuration. | Engineering team | M | H | Use the same image everywhere and verify `SERVICE_NAME` and the database URI in each environment. Compare the container's answers to the dev server's before Thursday. | Container or pod answers differ from the dev server → fix the configuration, not the code |
| R5 | A passing dry run is mistaken for a correct release. `kubectl apply --dry-run` proves the manifests parse, not that he elease works. | Angela Jeske (Delivery Lead) | M | M | Don't call the cluster done until three API pods are Running and a real POST comes back through the Service. | Pods stuck in `ContainerCreating` or `CrashLoopBackOff`, or the Service returns errors → treat as no-go for the demo |

|

## How I'll use this register

I'll re-read it at each morning check-in and again at the 15:30 sponsor check-in, and add a row whenever an inject, a test failure, or a surprise shows up. It lives in `delivery-leadership-package/` in the repo, so the instructor and my pair can read it at any time. By Thursday I'll mark which risks happened, which didn't, and what I'd change, and that becomes the "risks and how I handled the injects" slide for Friday.
