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