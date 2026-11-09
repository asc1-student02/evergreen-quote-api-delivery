# Decision Memo 1: Renters coverage
**Date:** November 9, 2026
**Author:** Angela Jeske
**Decision area:** Day 2 scope tradeoff: renters coverage request

## Context

At 2:00 pm Tuesday, the sponsor passed along a partner's request to quote renters coverage through the API by Thursday. The partner called it "one more dropdown option." The API currently accepts only auto, home, and life, and this morning it rejected an unknown type. We also have no approved renters rate.

## Options considered

1. **Option A: Say yes and build it this week.** The partner gets what they asked for. But the change touches six places (the allowed types, the rate table, the starting data, the tests, the partner interface, and the website dropdown), needs a rate nobody has approved, and would take time from work already committed for Thursday.
2. **Option B: Say yes with a placeholder rate.** This is the fastest way to test. But it puts an unapproved price into a system a partner would quote from, so customers could see a number nobody signed off on.
3. **Option C: Say no for this week and schedule it for the next round.** We protect Thursday's delivery and give the sponsor time to set a rate. The partner waits, but nothing breaks.

## Recommendation

Option C. Defer renters to the next delivery round, keep it on the board as a tracked item, and ask the sponsor for the renters rate by 11:00 am Wednesday so we can size the work and start as soon as the round opens.

## Why

Renters is a pricing decision before it is a coding task, and pricing belongs to the sponsor. Quoting a real customer from a number nobody approved is a bigger risk than making a partner wait one round.

## What would change my mind

If the sponsor provides an approved renters rate by Wednesday 11:00 am and names a week-one item to drop in exchange, I would revisit and consider adding renters this week.

# Decision Memo 2: Base image vulnerability

**Date:** November 9, 2026
**Author:** Angela Jeske
**Decision area:** Day 2 risk tradeoff: shipping on a base image with a flagged vulnerability

## Context

The platform team's monthly scan flagged a moderate-severity vulnerability in node:22-alpine, the base image the API's container is built on. The patched version arrives in their normal upgrade window next week, and they can't move it sooner. Their note says the API is not exposed to the internet this week. We containerize on Wednesday and demonstrate on Thursday.

## Options considered

1. **Option A: Ship this week on the current image.** We keep the schedule and the demo. The risk is a known, moderate issue in a service that isn't reachable from the internet this week, and it can be fixed by changing one line next week.
2. **Option B: Hold the container work until the patched image arrives.** This removes the flagged issue, but it blocks Wednesday's container build and Thursday's cluster demo, which depend on it, and gains little protection for a service nobody outside can reach.
3. **Option C: Use a different base image now.** This avoids the flagged one, but an untested base image this late in the week introduces new unknowns we haven't had time to check.

## Recommendation

Option A. Ship this week on the current image, record the issue on the board, and upgrade to the patched tag in next week's window.

## Why

The risk is real but small and short-lived: moderate severity, no internet exposure, and a fix already scheduled. Holding the delivery would cost the whole week's container and cluster work to remove a risk that is already contained.

## What would change my mind

If the service becomes reachable from the internet before the patched tag lands, or the platform team raises the severity, I would stop and move to the patched image immediately.