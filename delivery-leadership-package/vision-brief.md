## Product
**Name:** Evergreen Quote API (Phase 3 service delivery)
**Delivery week:** 3
**Delivery Lead:** Angela Jeske
**Engineering team (represented by):** [link to evergreen-quote-api-delivery repo]
**GitHub Project board:** [link]

## Who is the customer?
Three groups depend on this service. The Evergreen website team needs a place to
store and retrieve quotes instead of computing them in the browser and losing
them. A partner-integration pilot needs to pull quotes into its own systems and
request only the fields it needs. The operations team needs a service they can
actually ship: tested automatically, packaged in a container, and runnable on
the company's Kubernetes platform. Today none of them has a shared source of
quotes to build on.

## What pain does Evergreen Quote remove?
Phases 1 and 2 shipped a page that computes a number and then forgets it. A
customer who gets a quote cannot come back to it, a partner has nothing to
connect to, and operations has nothing safe to run. The Quote API remembers
every quote, rejects bad ones before they are saved, and gives the website and
partners one consistent answer, with the same data and the same premium math,
through two doors (REST and GraphQL).

## What does "good" look like at end of the week?
- Every route answers with the documented shapes, over REST and GraphQL.
- Invalid quotes (for example, an age under 18) are rejected with a clear message.
- The test suite is green locally and in CI, including on the merge to `main`.
- The container returns the same answers as the dev server.
- The cluster demo shows three pods behind one Service with a database.
- The work reached `main` through a reviewed PR, with the official service name
  and sponsor rates set by configuration.

## What are we explicitly NOT doing this week?
- Authentication
- A real rate engine (premiums come from a simple shared rate table)
- Multi-region deployment or CloudFront
- A live AWS deploy (the S3 path is reviewed, not run, unless the instructor
  confirms there is time)
- Rewriting the engineering team's starter code

## How will we know if it worked?
- 7 of 7 tests passing in CI on the merge to `main`.
- 3 of 3 API pods Running behind one Service in the cluster demo.
- 6 seeded quotes returned identically by the dev server and the container.