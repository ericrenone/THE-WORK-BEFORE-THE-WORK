# THE-WORK-BEFORE-THE-WORK

**2027 Outlook: Why Enterprise AI Is Costing More to Install Than It Has Had Time to Earn**

Eric Ren · ERI Labs · Jersey City, New Jersey · October 2026 · github.com/ericrenone

---

## Executive Summary

The enterprise AI market is entering 2027 in a condition that no standard model of technology adoption describes. Spending is rising at a rate the sector has not seen since the build-out of the internet. Returns, measured honestly, are concentrated in a small minority of firms. The gap between the two is not a lag. It is a structure, and the structure has a name: the work before the work.

Every AI deployment generates a quantity of implementation work — infrastructure, data repair, integration, governance, retraining — before it generates a dollar of return. In an ordinary technology cycle that work is paid off over a payback horizon of two to four years, and the technology holds still long enough to be paid off. This cycle is different. The technology does not hold still. The model, the tooling, and the pattern of use refresh on a horizon of nine to eighteen months. When the refresh horizon is shorter than the payback horizon, the deployment is re-implemented before it is profitable, and the implementation work renews while the return does not.

That is the central finding of this outlook, and the six findings beneath it follow from it.

**Finding 1 — Spending will rise faster than returns through 2027, and the gap is structural.** The most widely cited forecast puts worldwide AI spending at roughly $2.6 trillion in 2026 and $3.5 trillion in 2027, with infrastructure the largest category in both years. Against that, a survey of ten thousand companies found that nearly all have active AI initiatives, one in twenty say their data is ready, and roughly a quarter report broad or strong returns. The spending is real. The returns are real for the quarter that has them. The rest are paying for the work before the work.

**Finding 2 — There are four bills, and most budgets count two.** Infrastructure and people are budgeted. Integration headcount and data remediation are not, because they arrive as surprises after the first two are spent. Finding 2 sizes all four.

**Finding 3 — Companies are hiring to shrink.** The headcount story of 2026 was reduction attributed to AI. The headcount story underneath it is a sharp rise in roles that exist only to make AI work: forward-deployed engineers, integration engineers, data engineers, evaluation specialists, AI governance staff. Net headcount in the integration layer is rising. The reduction and the rise are in different departments and are reported on different slides.

**Finding 4 — The plumbing was built for reports, not for models.** Enterprise data pipelines were designed to deliver monthly aggregates to dashboards. AI requires row-level data with known provenance, delivered continuously, with lineage that can be audited. The gap between the two is the single largest hidden cost in enterprise AI, and it is where the majority of "integration" hours actually go.

**Finding 5 — The work multiplier is above one in the first six quarters of every deployment.** For every hour of work an AI workflow removes, the organization performs more than one hour of work to build, evaluate, govern, integrate, and maintain it, for a period that in most cases exceeds the life of the model version it was built on.

**Finding 6 — 2027 is the year the horizon crossing becomes visible.** Deployments begun in 2024 and 2025 reach the point in 2027 where their payback would have arrived — and discover that they have already been rebuilt once or twice on new model generations, resetting the payback clock each time. The firms that see this will separate from the firms that do not, and the separation will not show up in AI spending. It will show up in what the spending was pointed at.

The outlook closes with a framework for reading one's own position — the Four Bills, the Lineage Gap, the Work Multiplier, and the Horizon Crossing — and a short set of principles for leaders who intend to be in the quarter that profits rather than the three quarters that pay.

---

# PART ONE: THE BILLS

## 1. The Forty-Third Pipeline

Call the company Meridian. It is a regional property-and-casualty insurer with about six thousand employees, a two-hundred-million-dollar technology budget, and a board that asked, in the spring of 2025, what the company was doing about AI.

What Meridian did was reasonable. It licensed a frontier model through its cloud provider. It stood up an AI center of excellence with a head, four engineers, and a change-management lead. It picked a first use case that everyone agreed was safe and valuable: claims triage. A model would read the first notice of loss, extract the facts, score the claim for complexity and fraud risk, and route it to the right adjuster. The adjusters would spend less time reading and more time adjusting. The business case was eleven million dollars a year in productivity, against a build cost of about three million. Payback in four months. The board approved it in June.

The team began in July. By September they had a prototype that worked beautifully on the two hundred claims someone had pulled by hand into a spreadsheet. By October they had discovered why nobody had ever automated claims triage before.

The claim data lived in four systems. The policy data lived in two more, one of them a mainframe application from 1997 that exported a nightly flat file. The adjuster assignment logic lived in a business-rules engine nobody had modified since the person who built it retired. The first notice of loss came in through a web form, a phone transcription service, a broker portal, and email, each with its own schema. None of the six systems agreed on what a "claim" was, because they had been built for six different reports, each of which needed a slightly different definition.

To get the prototype's two hundred hand-pulled claims to flow automatically, the team needed a pipeline. To build the pipeline, they needed the six systems to deliver row-level data continuously, with timestamps, with a record of where each field came from and what had transformed it on the way. None of the six systems had been built to do that. They had been built to produce monthly aggregates for dashboards. The monthly aggregates were fine. The rows beneath them were a mess that the aggregation had been hiding for twenty years.

By the end of 2025, Meridian had built forty-two pipelines. Each one fed one data element from one source system into the staging layer the model read from. Each had taken, on average, three weeks of a data engineer's time, plus the time of someone in the business who knew what the field actually meant. The center of excellence had grown from five people to nineteen. The three-million-dollar build had become seven. The claims-triage model had not yet routed a single live claim.

In January 2026 the cloud provider announced a new model generation. It was substantially better at exactly the kind of extraction Meridian needed. It also had a different context window, different pricing, different failure modes, and a different recommended pattern for the retrieval layer. The team spent February re-evaluating. The evaluation harness they had built in the fall did not transfer cleanly to the new model, because the new model failed in different places. They rebuilt the harness. They re-ran the tests. They migrated. The forty-third pipeline — the one that would carry the model's output back into the assignment engine — was finished in April.

The claims-triage workflow went live in May 2026. It worked. The adjusters liked it. The productivity numbers, when they were finally measured in August, came in at about sixty percent of the business case, because the business case had assumed adjusters would spend the freed time adjusting and about half of them spent it on the backlog of exception reports the new system generated.

In September, the cloud provider announced another model generation.

Meridian's experience is not a failure story. The workflow is live. It will probably pay for itself. But count the clock. The business case said four months. The actual build took ten. The payback, measured from go-live at sixty percent of plan, is about twenty months. And the model it runs on will be two generations old before the twenty months are up — which means the evaluation, the retrieval pattern, and some fraction of the forty-three pipelines will be touched again, and the payback clock will move.

This is the work before the work. It is not a Meridian problem. It is the shape of the market.

## 2. The Four Bills

When a board approves AI spending, it approves two bills. The first is infrastructure: the compute, the licenses, the cloud consumption, the vector store, the observability tooling. The second is people: the upskilling program, the AI literacy curriculum, the center of excellence, the handful of hires with "AI" in the title. These two are visible in advance and they appear in the budget.

Two more bills arrive after the first two are committed. They do not appear in the budget because nobody knew to put them there, and they are, in most organizations, larger than the two that did.

The third bill is integration headcount. Not the AI engineers — those were in bill two — but the people required to connect what the AI engineers build to the systems the business actually runs on. Data engineers to build the pipelines. Integration engineers to wire the model's outputs into the workflow tools. Platform engineers to make the whole thing observable and deployable. Evaluation specialists to tell whether the model is doing what it is supposed to. Governance and risk staff to document all of it for the committees that exist to document things. Change managers, trainers, and the forward-deployed engineers that vendors and consultancies now sell by the team to do what the internal teams discover they cannot do alone.

The fourth bill is the data. Not the data platform — that was infrastructure — but the data itself: the discovery that the rows beneath the company's reports were never fit for a model to read, and the labor of making them so. Lineage, provenance, deduplication, reconciliation across systems that never agreed on definitions, the re-engineering of pipelines built for monthly aggregates into pipelines that deliver continuous, auditable, row-level truth. This bill is paid in data-engineer hours and business-analyst hours, and it is the bill that turns a four-month payback into a twenty-month one.

**Exhibit 1 — The Four Bills, sized for a mid-size enterprise AI program (illustrative model)**

*Assumptions: a company with $150–250M annual technology spend running six to ten production AI workflows by end of 2027. Figures are modeled ranges, not survey results, and are expressed as a share of the originally approved AI budget.*

| Bill | What it covers | Budgeted in advance? | Modeled size, as share of approved budget | When it arrives |
|---|---|---|---|---|
| 1. Infrastructure | Compute, model licensing, cloud consumption, vector stores, observability, security tooling | Yes | 100% (the baseline) | Year 1 |
| 2. People and upskilling | Center of excellence, AI-titled hires, literacy and training programs | Yes | 30–50% | Year 1 |
| 3. Integration headcount | Data, integration, platform, and evaluation engineers; governance staff; forward-deployed and consultancy teams | Rarely | 60–120% | Quarters 2–6 |
| 4. Data remediation | Lineage, provenance, reconciliation, pipeline re-engineering for row-level continuous delivery | Almost never | 80–200% | Quarters 2–8, recurring |
| **Total modeled cost** | | | **270–470% of approved budget** | |

The two bills that were budgeted are the two smallest. The two that were not are the two largest. The ratio is why the market can show record spending and thin returns in the same year without anyone having lied: the spending that was approved is a fraction of the spending that occurs, and the returns are measured against the fraction.

This is consistent with what the broadest available survey shows. Of ten thousand companies asked in 2026, nearly all reported active AI initiatives, but only about thirty percent were scaling anything into production and only a quarter said their returns were broad or strong. Asked what was in the way, half cited access to data, forty percent cited data quality, thirty-eight percent cited lack of integration across systems, and thirty-seven percent cited a shortage of qualified people. Those four answers are bills three and four, described by the people paying them.

## 3. The Spending Curve and the Return Curve

The macro picture is simple to state and hard to look at.

The most widely cited forecast puts worldwide AI spending at about $2.6 trillion in 2026, up roughly forty-seven percent from 2025, and about $3.5 trillion in 2027. Infrastructure — servers, chips, network fabric, AI-optimized cloud — is the largest category, around $1.4 trillion in 2026 and $1.9 trillion in 2027. Services are the second-largest category and software the third. The data-center build-out underneath this is financed by a lending pipeline that one bank sized at roughly $150 billion of required financing over a two-year window beyond what the AI companies fund themselves, against a wire-service tally of about $600 billion borrowed for data centers and related AI investment since the prior year.

Set that against the return side. A quarter of companies report broad or strong returns. Two-thirds report early signs or pockets. One in twenty say their data is ready for the initiatives they are running. The spending curve is near-vertical. The return curve is positive, real, and concentrated.

Ordinary adoption theory says this is normal. Every general-purpose technology shows a productivity J-curve: a period of heavy investment and flat or falling measured output while the complementary assets — the skills, the processes, the data, the organizational redesign — are built, followed by a period in which the output arrives all at once. Electricity took decades to show up in factory productivity because factories had to be rebuilt around it. Computers showed the same pattern in the 1980s and 1990s. The investment is the dip; the return is the rise; patience is the strategy.

The J-curve is the right frame, and it is where the 2027 outlook departs from the consensus. The J-curve assumes that the technology holds still long enough for the complementary assets to be built around it. The factory, once rebuilt around electric motors, stayed rebuilt. The office, once reorganized around the PC, stayed reorganized.

AI does not hold still. The model generation refreshes on a horizon of nine to eighteen months. The tooling refreshes faster. The recommended pattern of use — chat, then retrieval, then agents, then multi-agent orchestration — has changed three times since 2023. Each refresh does not simply improve the technology. It changes the shape of the complementary assets required to use it. The evaluation harness built for one model generation does not transfer to the next. The retrieval architecture built for one context window is wrong for a larger one. The governance framework written for chat assistants does not cover autonomous agents.

So the J-curve's dip does not end. It restarts. Each time the organization approaches the bottom of the curve and begins to climb, the technology refreshes, the complementary assets are partly invalidated, and the climb begins again from a point not much higher than the last one. The shape is not a J. It is a saw.

**Exhibit 2 — The saw: modeled cumulative return on a single enterprise AI workflow across model refreshes (illustrative)**

*Assumptions: build cost indexed to 100; steady-state annual return of 60 (a 20-month simple payback); model refresh every 12 months; each refresh invalidates 30–50% of the complementary build (evaluation, retrieval, integration, governance) and resets that portion of the cost.*

| Quarter from start | Cumulative cost | Cumulative return | Net position | Event |
|---|---|---|---|---|
| Q1–Q3 | 100 | 0 | −100 | Build; pipelines; evaluation |
| Q4 | 100 | 15 | −85 | Go-live at partial plan |
| Q5 | 140 | 30 | −110 | Model refresh: evaluation and retrieval rebuilt |
| Q6–Q8 | 140 | 75 | −65 | Climb |
| Q9 | 185 | 90 | −95 | Second refresh: agentic pattern; governance rewritten |
| Q10–Q12 | 185 | 135 | −50 | Climb |
| Q13 | 230 | 150 | −80 | Third refresh |

Under these assumptions, the workflow never reaches positive net position within three years, even though its steady-state economics — a twenty-month payback — would have cleared in Q8 if the technology had held still. The return is real. The payback is real. The refresh keeps moving the finish line.

The assumptions are deliberately moderate. A refresh that invalidates half the build every nine months, which is what the agentic transition produced in 2026 for many retrieval-based deployments, is worse. A workflow with a thirty-month payback, which is what most of the "transformation" use cases carry, is much worse.

This is the market's structural condition entering 2027. It is not that AI does not work. It is that the work before the work renews faster than the work after it accumulates.

---

# PART TWO: THE WORK

## 4. Hiring to Shrink

The headline employment story of 2026 was reduction. A payments company cut forty percent of its workforce and credited intelligence tools. Others followed with smaller numbers and the same explanation. The implication, drawn by every analyst who read the releases, was that AI was beginning to replace labor at scale.

Underneath the headline there is a second story, and it is told in the job postings.

In the first half of 2026, demand for a role that barely existed in 2024 rose faster than demand for any other technical position: the forward-deployed engineer, the specialist whose job is to take a frontier model and make it work inside one specific company's data and workflows. One executive-search study circulated in July claimed that the share of large companies planning to hire for the role rose from under ten percent at the start of the year to around seventy percent by the end of the second quarter, and that consultancies were growing their deployment teams tenfold. The precise figures are secondhand and should be held loosely. The direction is not in doubt. Vendors, consultancies, and systems integrators spent 2026 building deployment practices by the hundreds of people, and the people they hired were not AI researchers. They were integrators.

The same pattern shows up inside enterprises, one level down from the headlines. For every AI-titled hire in the center of excellence, the organization discovers it needs two to four people whose titles do not say AI: data engineers to build the pipelines, integration engineers to wire the outputs, platform engineers to make it run, evaluation engineers to tell whether it is working, and governance staff to document it for the committees. These are the third bill. They are hired because the first two bills, once spent, revealed that nothing would work without them.

So the enterprise is doing two things at once. It is reducing headcount in the functions AI is supposed to replace, and it is adding headcount in the functions required to make AI replace them. The two numbers live in different departments. The reduction is reported in operations, customer service, and back office. The addition is reported in technology, and it is reported as investment rather than as cost. The net effect on total headcount, at most companies in 2026, is smaller than either number, and at many it is positive.

Call this the Integration Tax: the headcount an organization must add in order to realize headcount reductions elsewhere. It has three properties worth seeing.

It scales with the number of workflows, not with the number of people replaced. Each new AI workflow needs its own pipelines, its own evaluation, its own integration. The integration team grows with the portfolio. The replaced headcount grows with the success of each workflow, which is slower and less certain.

It is more expensive per head than what it replaces. A data engineer or forward-deployed engineer in 2026 costs two to four times what a claims processor or customer-service representative costs. Replacing three of the latter with one of the former is, in the first two years, a cost increase.

It is sticky. The processors, once released, are gone. The integration team, once built, is required for as long as the workflows run, because the workflows refresh — and each refresh is integration work. The tax is not a one-time charge. It is a standing cost of operating AI in an organization whose systems were not built for it.

**Exhibit 3 — Modeled headcount movement for a mid-size enterprise over an AI program's first three years (illustrative)**

*Assumptions: 6,000-employee company; eight production workflows by year 3; each workflow releases 25–40 FTE at steady state and requires 3–5 integration FTE to build and 1.5–2.5 to maintain through refreshes. Cost per head indexed: replaced roles at 1.0, integration roles at 2.5–3.5.*

| | Year 1 | Year 2 | Year 3 |
|---|---|---|---|
| Workflows in production | 1 | 4 | 8 |
| Headcount released (cumulative) | 10 | 90 | 240 |
| Integration headcount added (cumulative) | 18 | 38 | 52 |
| Net headcount change | +8 | −52 | −188 |
| Net cost change, indexed to replaced-role cost | +50 | +35 | −40 |

Under these assumptions, net headcount turns negative in year two and net cost does not turn negative until year three. The organization is paying more in year one and two to employ fewer people in year three — and the year-three figure assumes no refresh resets the maintenance load, which, as Part One showed, is not the assumption to make.

## 5. The Training That Does Not Transfer

The second bill — people and upskilling — is the one boards feel best about approving. It is visible, it is virtuous, and it has a number: the share of the workforce that has completed the AI literacy program. In 2026 that number, at most large companies, was above eighty percent, and it was reported on the same slide as the headcount reductions, as evidence that the organization was taking its people with it.

Look at what the number measures.

An enterprise upskilling program in 2026 had three tiers. The broad tier — most of the workforce — taught people how to use a chat assistant: prompting, summarizing, drafting, the responsible-use policy. The middle tier — analysts, operations staff, product people — taught people how to use the AI features embedded in the tools they already had, and sometimes a low-code workflow builder. The narrow tier — a few hundred engineers and data people — taught retrieval architecture, evaluation, model selection, and the vendor's current recommended pattern.

Now watch what the refresh does to each tier.

The broad tier's content survives, mostly. Prompting a chat assistant in 2027 is not very different from prompting one in 2025. But the broad tier also produces the least return, because a workforce that has learned to summarize meetings is not a workforce that has changed how it works. The survey evidence is consistent: adoption measured as logins or course completion is high nearly everywhere; return measured as changed workflow is concentrated in the quarter.

The middle tier's content depreciates with the tooling. The embedded AI features in the productivity suite, the CRM, the ticketing system — these changed substantially between 2025 and 2026 and will change again. The low-code workflow builder that was taught in the spring was superseded by the vendor's agent builder in the fall. The people trained on the first are not trained on the second. The course is run again.

The narrow tier's content depreciates with the pattern. This is the tier that mattered most and cost the most per head, and it is the one the refresh hits hardest. Engineers trained on retrieval architecture in 2025 were trained on the right thing for 2025. In 2026 the right thing was agentic orchestration, which is not retrieval with more steps; it is a different architecture with different evaluation, different failure modes, and different governance. The 2025 training was not wasted — some of it transfers — but the organization that counted it as a built capability discovered that the capability had a shelf life of about a year, and the shelf life is shortening.

So the second bill, which boards experience as a one-time investment in a durable asset, is in fact a recurring cost with a depreciation schedule tied to the refresh. The broad tier is cheap, durable, and low-return. The narrow tier is expensive, high-return, and depreciates in twelve months. The upskilling program is a saw too.

There is a second problem with the second bill, and it is the one the prior guide in this lineage spent most of its length on. The tier of the organization that most needs to understand the technology — the executives and senior managers deciding what to deploy, which vendor to standardize on, and which workflows to fund — is the tier that upskilling programs touch most lightly. The AI-for-leaders course is a half-day. It teaches vocabulary. It produces fluency, and fluency feels like understanding, and the people who come out of it are no better able to evaluate a business case's Work Multiplier than they were going in. The second bill buys the broad tier durable low-value skills, the narrow tier perishable high-value ones, and the deciding tier a vocabulary. None of those is the thing the organization needed, which was the capacity, at the level where spending is approved, to tell the work before the work from the work.

**Exhibit 3a — Upskilling spend by tier: cost, return, and depreciation (illustrative model)**

*Assumptions: 6,000-employee enterprise; three-tier program as described; cost per head indexed to the broad tier at 1.0; return expressed as the tier's contribution to realized workflow value; depreciation as the share of the tier's content invalidated per refresh cycle.*

| Tier | Headcount reached | Cost per head (indexed) | Share of program cost | Contribution to realized return | Content invalidated per refresh | Effective shelf life |
|---|---|---|---|---|---|---|
| Broad: assistant literacy | ~5,000 | 1.0 | 35% | Low | ~10% | 3+ years |
| Middle: embedded tools and workflow builders | ~800 | 4.0 | 25% | Moderate | ~50% | 12–18 months |
| Narrow: engineering, evaluation, architecture | ~200 | 25.0 | 35% | High | ~40–60% | 9–15 months |
| Deciding: executive AI literacy | ~60 | 12.0 | 5% | Indirect; governs allocation | Vocabulary persists; judgment not acquired | Not applicable |

The tier that produces the return has the shortest shelf life. The tier with the longest shelf life produces the least. And the tier that decides where the other three are pointed acquires, for its five percent, a vocabulary.

A practical consequence follows. Upskilling should be budgeted as an operating cost with a refresh schedule, not as a capital investment in a workforce capability. The narrow tier should be retrained on each pattern refresh and that retraining should be in the Work Multiplier as part of the refresh term. And the deciding tier's program should be replaced with something that is not a course: a contributory practitioner in the room where allocations are made, with authority over the content of the decisions and not just a seat at the review.

## 6. Where the Crossing Is Steepest

The mechanisms in this outlook apply everywhere, but not evenly. The steepness of the saw — how far the refresh horizon sits below the payback horizon — varies by sector, and the variation is mostly a function of two things: how old the data estate is, and how regulated the workflow is.

An old data estate means a wide Lineage Gap, which lengthens payback. A regulated workflow means a large governance term in the Work Multiplier and a slow evaluation cycle, which also lengthens payback. Sectors with both have the longest honest paybacks and are therefore furthest into the crossing. Sectors with neither have paybacks short enough to clear the refresh and are, by and large, where the quarter that profits lives.

**Exhibit 3b — Sector exposure to the Horizon Crossing (indicative, not survey-derived)**

| Sector | Data estate age | Regulatory weight on workflows | Modeled honest payback, first-wave deployments | Refresh ÷ payback | Position |
|---|---|---|---|---|---|
| Insurance (P&C, life) | Old; mainframe-era policy systems | High | 28–40 months | 0.3 | Deep in the crossing |
| Retail banking | Old; layered core systems | Very high | 30–42 months | 0.3 | Deep in the crossing; perimeter also closed to agents |
| Healthcare providers and payers | Old; fragmented clinical and claims data | Very high | 30–48 months | 0.25 | Deepest |
| Public sector | Very old | High | 36+ months | 0.25 | Deepest; longest refresh tolerance may partly offset |
| Manufacturing and industrials | Mixed; OT/IT divide | Moderate | 20–32 months | 0.45 | In the crossing |
| Professional services | Moderate; document-heavy | Low to moderate | 12–20 months | 0.7 | At the edge; narrow workflows clear |
| Software and digital-native | New; built for rows | Low | 6–14 months | 1.0–1.5 | Clears the horizon; the quarter that profits |
| Media and marketing | Mixed | Low | 8–16 months | 0.9 | Near the edge; content workflows clear |

The pattern is the one the first document in this lineage predicted from the other direction. The sectors with the oldest, most reliable, most institutionalized structures — the ones with two-hundred-year-old franchises and record quarters — are the ones whose honest paybacks are longest and whose refresh exposure is highest. They are spending the most on the work before the work, and they are the ones for whom 2027 will be the year the crossing becomes visible on the board slide.

## 7. The Plumbing Was Built for Reports

Return to Meridian's forty-two pipelines, because they are the whole market in miniature.

An enterprise data estate, at nearly every company founded before 2015, was built to answer one kind of question: what happened last month? The answer was a report. The report was a set of aggregates — totals, averages, counts by category — delivered on a schedule to a dashboard or a spreadsheet. The entire apparatus beneath the report — the warehouses, the ETL jobs, the nightly batch windows, the business-intelligence layer — was engineered to produce aggregates reliably, on time, at a level of granularity that a human would read.

Aggregation is forgiving. If three source systems disagree about what a customer is, the monthly count of customers is still approximately right, because the disagreements wash out at scale and nobody checks the rows. If a field was transformed somewhere in the pipeline by a rule nobody remembers, the total is still plausible, and plausible is the standard a dashboard is held to. Twenty years of this produced data estates that were adequate at the aggregate level and unexamined beneath it.

A model does not read aggregates. It reads rows. It reads the specific claim, the specific customer, the specific transaction, and it needs each one to be correct, complete, timestamped, and traceable to its origin, because the model's output will be a decision about that row — route this claim, flag this transaction, answer this customer — and a wrong row produces a wrong decision that a human may never see. Aggregation's forgiveness does not apply. Every discrepancy the dashboards were hiding becomes a defect the model will act on.

And a model needs the rows continuously, not monthly. A claims-triage model that reads last night's batch is making decisions on claims that arrived yesterday, which is useless for routing claims that arrive today. The nightly batch window — the architectural heart of every pre-2015 data estate — is the wrong shape.

So the organization discovers, usually in the second quarter of its first serious deployment, that it does not have a data problem. It has a plumbing problem. The pipes were laid to carry monthly aggregates to dashboards. They now need to carry continuous, row-level, provenance-tagged data to a model. That is not a cleaning job. It is a re-engineering job, pipe by pipe, and it is paid in the most expensive engineering hours the company has.

Call this the Lineage Gap: the distance between the data an enterprise's systems were built to deliver and the data a model requires. It is the fourth bill. It has four components, and each is a separate project.

**Provenance.** Where did this field come from, and what touched it on the way? Most enterprise pipelines cannot answer this for any field, because nobody needed the answer for a dashboard. A model's output cannot be audited, debugged, or defended to a regulator without it.

**Reconciliation.** Six systems, six definitions of a claim. The dashboard tolerated it. The model cannot. Someone has to decide which definition is canonical, and that someone is a business owner who has never been asked, and the deciding takes months.

**Granularity and timing.** From monthly aggregates to continuous rows. From nightly batch to streaming or near-real-time. This is an architectural change to the data layer, not a configuration.

**Quality at the row.** The defects aggregation hid — nulls, duplicates, stale values, silent transformations — surface one at a time, each discovered when a model does something strange and someone traces it back.

The survey evidence lines up exactly. Of the barriers ten thousand companies cited in 2026, the top four were data access, data quality, lack of integration across systems, and shortage of qualified people. The fourth is the third bill. The first three are the Lineage Gap. Only five percent of respondents said their data was ready, and they were almost certainly describing the five percent of companies whose data estates were built after the dashboard era, or rebuilt during it.

One more thing about the Lineage Gap. It does not close with the first workflow. The first workflow fixes the pipes it needs. The second workflow needs different pipes. The third discovers that the first workflow's canonical definition of a customer conflicts with the third's. The gap is closed system by system, field by field, and the closing is a multi-year program that no board approved, because no one knew to propose it, because the dashboards were green.

## 8. The Work Multiplier

Here is the quantity the market is not measuring and should be.

Take a single AI workflow. Count the hours of human work it removes per week once it is running at steady state. Then count the hours of human work the organization performs per week to build it, evaluate it, integrate it, govern it, and maintain it through refreshes. Divide the second by the first.

Call that the Work Multiplier. It is the ratio of work created to work removed, and the claim of this outlook is that it is above one for the first six quarters of nearly every enterprise deployment, and stays above one indefinitely for deployments whose refresh cycle is shorter than their payback.

The multiplier has five terms. Each is a kind of work AI generates that did not exist before AI.

**Build work.** The pipelines, the prompts, the retrieval layer, the integration code. Large, front-loaded, partly reusable across workflows and partly not.

**Evaluation work.** Deciding whether the model is doing what it is supposed to, on an ongoing basis, against a definition of "supposed to" that the business has never previously had to write down. This is new work. No prior technology required the organization to continuously measure whether its software was being truthful. It is also the work most often skipped, and skipping it is how a workflow passes governance and does not work.

**Governance work.** Documenting the model, the data, the risks, the controls, and the decisions for the committees — model risk, responsible AI, architecture review, audit — that exist to document things. Much of it is ceremony. Some of it is necessary. All of it is hours.

**Exception work.** The model handles the eighty percent. The twenty percent it cannot handle becomes a queue of exceptions that a human must review, and the queue is often larger than the work the model removed, because the model surfaces cases that were previously handled silently and badly. Meridian's adjusters spent half their freed time on the exception backlog. That is the exception term.

**Refresh work.** Everything above, partially repeated, each time the model generation, the tooling, or the recommended pattern changes. This is the term that keeps the multiplier above one, because it does not decay.

**Exhibit 4 — Modeled Work Multiplier for a representative enterprise workflow, by quarter (illustrative)**

*Assumptions: workflow removes 400 human-hours per week at steady state; build 2,400 hours over Q1–Q3; evaluation 60 hours/week ongoing; governance 40 hours/week ongoing; exception queue 150 hours/week declining to 80; refresh reinvests 40% of build every four quarters.*

| Quarter | Hours removed / week | Hours created / week | Work Multiplier |
|---|---|---|---|
| Q1–Q3 (build) | 0 | 185 + overhead | ∞ |
| Q4 | 240 | 250 | 1.04 |
| Q5 (refresh) | 240 | 330 | 1.38 |
| Q6 | 320 | 230 | 0.72 |
| Q7 | 400 | 200 | 0.50 |
| Q8 | 400 | 190 | 0.48 |
| Q9 (refresh) | 400 | 270 | 0.68 |
| Q10 | 400 | 190 | 0.48 |

In this model the multiplier crosses below one in Q6 and settles near a half — a real, substantial saving — but each refresh pushes it back toward one, and a more aggressive refresh cadence, or a larger exception queue, keeps it above one for the life of the deployment. The point is not that the multiplier never falls. It is that the market's business cases assume it falls to zero and stays there, and it does not.

The Work Multiplier is the number to put on the slide beside the productivity estimate. It is the honest denominator. A deployment with a projected productivity gain and no Work Multiplier estimate is a deployment whose cost has not been counted.

---

# PART THREE: THE HORIZON

## 9. Two Horizons

Every investment has a payback horizon: the time from first dollar spent to the point where cumulative return equals cumulative cost. Every technology has a refresh horizon: the time from one generation to the next, after which the prior generation is no longer the thing you would build on if you were starting today.

For most of the history of enterprise technology, the second horizon was longer than the first. A core banking system paid back in four years and lasted twenty. An ERP implementation paid back in three and lasted twelve. Even the PC, the fastest-refreshing technology of its era, refreshed on a three-to-four-year hardware cycle against a payback measured in months. The technology held still long enough to pay for itself. That is the condition under which the J-curve works and the productivity arrives.

The AI transition inverts the two horizons. The payback horizon, honestly computed with all four bills and the Work Multiplier, is twenty to thirty-six months for most enterprise workflows. The refresh horizon — the interval between model generations, tooling generations, or shifts in the dominant pattern of use — is nine to eighteen months and compressing. The technology does not hold still long enough to be paid for. The deployment is rebuilt before it is profitable, and the rebuild resets some fraction of the payback clock.

Call this the Horizon Crossing: the condition in which a technology's refresh horizon is shorter than its payback horizon, so that implementation work renews faster than return accumulates. It is the mechanism beneath every finding in this outlook, and it is the reason the J-curve has become a saw.

Three things make the crossing worse than it looks.

The refresh is not optional. An organization can decline to upgrade its ERP for a decade. It cannot decline to move to the next model generation, because the prior generation is deprecated, repriced, or simply outperformed by what competitors are deploying, and because the vendor's roadmap — which, as the first guide in this lineage showed, is usually also the enterprise's borrowed vision — moves on.

The refresh invalidates the expensive parts. A new model generation does not require rebuilding the pipelines; the fourth bill, once paid, mostly stays paid. It requires rebuilding the evaluation, the retrieval architecture, the prompting, the integration logic, and the governance documentation — which is to say, most of the third bill and all of the Work Multiplier's ongoing terms.

The refresh changes the pattern, not just the model. The move from chat to retrieval to agents was not three better versions of one thing. It was three different things, each requiring a different complementary build. An organization that finished its retrieval build in 2025 found in 2026 that the recommended pattern was agentic, and that its retrieval build was now one component inside a larger architecture it had not designed for. The refresh horizon for the pattern is the one that matters, and it has been about twelve months.

**Exhibit 5 — Horizon comparison across technology eras (indicative ranges)**

| Technology | Typical enterprise payback horizon | Refresh horizon | Ratio (refresh ÷ payback) | Condition |
|---|---|---|---|---|
| Core banking / ERP (1990s–2000s) | 36–60 months | 120–240 months | 3–4× | J-curve resolves |
| Enterprise PC and office software | 6–18 months | 36–48 months | 3–5× | J-curve resolves |
| Cloud migration (2010s) | 24–48 months | 48–72 months | 1.5–2× | J-curve resolves slowly |
| Enterprise AI, chat and retrieval (2023–2025) | 18–30 months | 12–18 months | 0.5–0.8× | Horizon crossed |
| Enterprise AI, agentic (2025–2027) | 20–36 months | 9–12 months | 0.3–0.5× | Horizon crossed; saw steepens |

*Payback and refresh ranges are indicative, drawn from the modeled cases in this outlook and general industry experience; they are not survey results.*

The ratio is the diagnostic. Above one, the technology pays for itself before it is replaced, and patience is the right strategy. Below one, it does not, and patience is a strategy for paying the work before the work indefinitely.

## 10. What the Crossing Does to a Business Case

Meridian's claims-triage business case said four months. Here is what each of this outlook's mechanisms did to it, in order.

The four bills turned a $3 million build into a $7 million one. Payback at the original return estimate: nine months.

The Lineage Gap pushed go-live from October to May. Payback clock started seven months late.

The Work Multiplier — the exception queue in particular — held realized return at sixty percent of plan. Payback at realized return: twenty months from go-live.

The Horizon Crossing — a model refresh in January, and another in September — reinvested roughly forty percent of the complementary build each time. Each refresh added four to five months to payback.

Honest payback, computed in October 2026 with two refreshes already behind it and a third expected: about thirty-two months from the June 2025 approval. The board was told four.

Nobody lied. The four-month figure was the right answer to the question the business case asked, which was: if the model works on the sample and nothing else changes, how fast does the productivity pay for the build? The thirty-two-month figure is the answer to the question nobody asked, which was: how fast does the productivity pay for the build, the people, the plumbing, the exceptions, and the rebuilds?

The gap between four and thirty-two is the market in 2027.

Multiply Meridian by every mid-size enterprise that approved a first serious AI deployment in 2024 or 2025. Their original paybacks were due in 2026 and 2027. Their honest paybacks are due in 2028 and 2029, if the refresh cadence does not compress further, which it will. 2027 is therefore the year the crossing becomes visible at scale: the year boards that were promised returns in 2026 ask where they are, and are told, accurately, that the workflow was rebuilt twice and the clock moved.

Three responses will follow, and the market will sort by which one each company chooses.

Some will stop. The spending will be cut, the center of excellence trimmed, the deployment left running on a deprecated model generation until it quietly stops being used. This is the response of boards that read the gap as failure.

Some will double down on the same pattern — more spending, more workflows, more refreshes — on the theory that scale will eventually outrun the saw. This is the response of organizations whose decision-makers sit above the ceiling described in the prior guide, and it is the response the vendor roadmap recommends, because the vendor roadmap is a sales document.

And some will change what they are spending on. This is the subject of Part Four.

## 11. The Three Quarters and the One

The survey arithmetic bears repeating because it is the cleanest statement of where the market stands. Nearly all companies have AI initiatives. About a quarter report broad or strong returns. The other three quarters are somewhere between early signs and nothing.

The consensus reading is that the three quarters are behind the one — on the same curve, earlier. This outlook's reading is different. The one quarter is not ahead on the same curve. It is on a different curve, because it is spending on different things.

What distinguishes the quarter that profits, as far as can be seen from outside, is not the size of the spend, the sophistication of the models, or the number of workflows. It is three structural choices.

**They paid the fourth bill first.** The organizations seeing broad returns are disproportionately those that rebuilt their data layer — provenance, reconciliation, continuous row-level delivery — before or alongside their first model deployment, rather than discovering the Lineage Gap in the second quarter of the build. The five percent who say their data is ready and the quarter who report strong returns overlap heavily. The data layer is the one complementary asset that the refresh does not invalidate. It is the thing worth building because it stays built.

**They chose workflows whose payback beats the refresh.** Not the transformation use case with a thirty-six-month horizon and a board-level narrative. The narrow, high-volume, well-bounded workflow — document extraction, classification, routing, first-draft generation in a constrained domain — where the exception queue is small, the evaluation is tractable, and the honest payback is under twelve months. These clear the horizon before the refresh resets them. They are unglamorous. They are the ones that pay.

**They separated what refreshes from what persists.** The model, the prompting, the orchestration pattern — these refresh, and the quarter that profits treats them as consumables: bought, not built, swapped when the generation changes, with as little custom scaffolding around them as the workflow allows. The data layer, the evaluation discipline, the integration contracts with core systems — these persist, and the quarter that profits treats them as assets: built, owned, and designed so that a model swap does not touch them. The three quarters that pay have the allocation backward. They build elaborate custom scaffolding around a model that will be deprecated in a year, and they leave the data layer to be fixed pipe by pipe as each workflow trips over it.

**Exhibit 6 — Spending allocation: the quarter that profits versus the three that pay (modeled pattern)**

*Shares of total three-year AI program spend. Modeled from the structural choices described above; not survey data.*

| Spending category | Three quarters that pay | Quarter that profits |
|---|---|---|
| Model licensing and compute | 25% | 20% |
| Custom scaffolding around the model (prompting, retrieval, orchestration built in-house) | 25% | 8% |
| Data layer: lineage, reconciliation, continuous delivery | 12% | 35% |
| Evaluation discipline and tooling | 5% | 15% |
| Integration contracts with core systems | 13% | 15% |
| Governance and ceremony | 12% | 5% |
| Upskilling and change management | 8% | 2% |
| **Share of spend invalidated by a model refresh** | **~45%** | **~15%** |

The last row is the one that matters. The three quarters that pay have nearly half their program spend sitting in assets that the next refresh will partly destroy. The quarter that profits has most of its spend in assets the refresh leaves alone. Same technology, same vendors, same year. Different exposure to the saw.

---

# PART FOUR: THE OUTLOOK

## 12. 2027: What the Market Will Do

The forecast is for roughly $3.5 trillion in AI spending in 2027. This outlook does not dispute the number. It disputes what the number means.

Most of it is infrastructure — the chips, the servers, the data centers — and most of that is being bought by a small number of very large technology companies and the firms that build for them. That spending will happen. It is financed, contracted, and under construction. Whether it pays is a question for the lenders and the capital markets, and the first document in this lineage addressed it.

The enterprise share — the services and software and internal spending that companies like Meridian do — is the part this outlook is about, and the claim is that 2027 is the year it splits.

Here is what the split will look like.

**Approved AI budgets will rise modestly. Realized AI spending will rise sharply.** Boards will approve ten to twenty percent increases, reading the prior year's returns as early but promising. Actual spend, once the third and fourth bills arrive on the new workflows, will run two to three times the approved figure, as it did in 2026, and the overrun will be reported as investment.

**The integration layer will keep growing, and it will be renamed.** The forward-deployed engineer will become a permanent enterprise role, not a vendor service. Data engineering headcount will rise faster than AI engineering headcount. "AI platform" teams will absorb what used to be called data platform, integration, and observability, and will be the largest technology function at many companies by headcount. None of this will appear on the slide that reports headcount reductions.

**The Lineage Gap will become a line item.** Enough organizations will have tripped over it enough times that it will get a name in the budget — data readiness, data foundation, AI-ready data — and a multi-year program behind it. This is the single most constructive thing that will happen in 2027. It is the fourth bill being counted in advance for the first time.

**The first wave of honest paybacks will be reported, and they will be long.** Deployments approved in 2024 and 2025 will reach the point where their original business cases promised return. Boards will ask. The honest answer — rebuilt twice, clock moved, thirty months, not six — will be given at some companies and buried under form metrics at others. The companies that give the honest answer will be the ones that change what they are spending on.

**The refresh cadence will compress again.** The agentic pattern of 2026 will be succeeded by whatever the vendors ship in 2027, and the organizations that built elaborate custom scaffolding around 2026's agents will discover that the scaffolding is 2027's technical debt. The saw's teeth will get closer together.

**The quarter that profits will grow to a third, and the gap to the rest will widen.** Not because the rest are failing — they are paying the work before the work, and some of them will eventually cross — but because the third will have shifted their spend toward what persists, and the compounding will begin to show. The split will be invisible in total AI spending, which will rise everywhere. It will be visible in what the spending bought.

**Exhibit 7 — 2027 enterprise AI outlook: modeled scenario ranges**

*Scenario ranges for a representative population of large and mid-size enterprises. Modeled, not forecast from survey data; the macro spending figure is from the published forecast cited in the Executive Summary.*

| Indicator | 2026 (observed or estimated) | 2027 (modeled range) | Direction |
|---|---|---|---|
| Worldwide AI spending (published forecast) | ~$2.6T | ~$3.5T | Up sharply |
| Share of enterprises with active AI initiatives (survey) | ~97% | ~98% | Flat (saturated) |
| Share reporting broad or strong returns (survey) | ~24% | 28–35% | Up modestly |
| Share reporting data ready for AI (survey) | ~5% | 8–15% | Up, from a low base |
| Realized spend ÷ approved budget (modeled) | 2.5–3.5× | 2.0–3.0× | Slight improvement as bills 3 and 4 get budgeted |
| Integration headcount ÷ AI-titled headcount (modeled) | 2–4× | 3–5× | Up |
| Share of program spend invalidated per refresh (modeled, median firm) | ~45% | ~40% | Slight improvement |
| Median honest payback, first-wave deployments (modeled) | 24–36 months | 28–40 months | Longer, as refreshes accumulate |
| Model/pattern refresh interval (observed) | 9–12 months | 6–10 months | Compressing |

The table says, in numbers, what the outlook says in prose. Spending up. Initiatives saturated. Returns improving slowly from a low base. The bills slowly getting counted. The refresh getting faster. And the honest payback getting longer, not shorter, because the work before the work renews faster than the counting of it improves.

## 13. The Framework

This outlook has introduced five instruments. Here they are together, with what each measures and where to look for it in your own organization.

**The Four Bills.** Infrastructure, people, integration headcount, data remediation. The first two are budgeted; the last two are discovered. Modeled total: 270–470 percent of the approved budget. Look at your own AI program's realized spend against its approved spend. The ratio is your bills-three-and-four exposure. If it is above two, you have not yet counted the work before the work.

**The Lineage Gap.** The distance between the data your systems were built to deliver — monthly aggregates to dashboards — and the data a model requires — continuous, row-level, provenance-tagged. Four components: provenance, reconciliation, granularity and timing, quality at the row. Look at how many pipelines your first serious deployment required and how many of them were built after the business case was approved. That number, times three weeks of a data engineer, is the gap's first invoice.

**The Integration Tax.** The headcount you must add to realize headcount reductions elsewhere. Scales with workflows, not with people replaced; costs more per head; sticky. Look at the ratio of integration-layer hires to AI-titled hires in your technology organization over the last eighteen months. If it is above two, you are paying the tax. If nobody has computed it, you are paying it without knowing.

**The Work Multiplier.** Hours of work created per hour of work removed, per workflow, per quarter. Five terms: build, evaluation, governance, exception, refresh. Above one for the first six quarters; pushed back toward one at each refresh. Look at any business case on your desk. If it has a productivity estimate and no Work Multiplier, its cost has not been counted.

**The Horizon Crossing.** The condition where the refresh horizon is shorter than the payback horizon. Ratio below one means the technology does not pay for itself before it is replaced. Look at your longest-horizon AI deployment. Divide the interval between the last two model or pattern refreshes by its honest payback. If the result is below one, patience is not a strategy. Reallocation is.

Together they describe a single mechanism. Every AI deployment generates implementation work — the bills, the gap, the tax, the multiplier — before it generates return. In an ordinary technology cycle the work is paid off because the technology holds still. In this cycle it does not, and the work renews. The organizations that profit are not the ones that spend the most or wait the longest. They are the ones that put their spending where the refresh cannot reach it.

## 14. What Leaders Should Do

Seven principles. Each runs against what a large organization will do by default in 2027.

**Count all four bills before approving the first two.** Any AI business case that does not include integration headcount and data remediation as line items is a business case for a fraction of the cost. Require both. Use the modeled ranges in Exhibit 1 as a floor until your own program produces real ones. A board that approves $3 million should expect to spend $8 million to $14 million, and should be told so.

**Pay the fourth bill first.** The data layer is the one complementary asset the refresh leaves alone. Build provenance, reconciliation, and continuous row-level delivery as a program in its own right, before or alongside the first model deployment, not pipe by pipe as each workflow trips over it. This is the single highest-return allocation in enterprise AI, and it is the one most boards have never been asked to approve, because it does not have a model in it.

**Choose workflows whose honest payback beats the refresh.** Compute the ratio. Favor the narrow, high-volume, well-bounded workflow with a sub-twelve-month honest payback over the transformation use case with a thirty-six-month narrative. The narrow ones clear the horizon. The narrative ones pay the work before the work indefinitely. The narrative can come later, built on top of narrow workflows that have already cleared.

**Buy what refreshes. Build what persists.** Treat the model, the prompting, and the orchestration pattern as consumables — licensed, swapped, with the thinnest possible custom scaffolding. Treat the data layer, the evaluation discipline, and the integration contracts with core systems as owned assets — built once, designed so that a model swap does not touch them. The share of your program spend that a refresh invalidates should be under twenty percent. Measure it. If it is above forty, you are building the saw's next set of teeth.

**Put the Work Multiplier on every slide.** Beside every productivity estimate, the modeled ratio of hours created to hours removed, by quarter, with the exception queue and the refresh term shown explicitly. The number will be uncomfortable. It is the honest denominator, and a deployment presented without it is a deployment whose cost is being hidden from the people approving it.

**Budget the Integration Tax as a standing cost, not an investment.** The integration layer does not go away when the workflow ships. It is required for as long as the workflow runs, because the workflow refreshes. Report it as operating cost, beside the headcount it enables you to release, on the same slide. If the net is positive, say so. If it is not yet, say that.

**Separate the honest payback from the business-case payback, and report both.** The business-case payback answers "if nothing else changes." The honest payback answers "with all four bills, the multiplier, and the refreshes you have already absorbed." Boards that see both will make better decisions. Boards that see only the first will approve another round of the work before the work and call it patience.

---

## The Creed

**Count the four bills. Pay the fourth one first. Build what persists; buy what refreshes.**

And beneath it:

The business case says four months. The honest case says thirty. Report the honest one.

The plumbing was built for reports. A model reads rows. Fix the pipes before you pick the model.

You are hiring to shrink. Put both numbers on one slide.

For every hour removed, count the hours created. The ratio is the cost.

If the refresh is shorter than the payback, patience is not a strategy.

The quarter that profits did not spend more. It spent where the refresh cannot reach.

---

## The Instruments

| Instrument | What it measures | Where to look | Threshold |
|---|---|---|---|
| **The Four Bills** | Realized AI spend across infrastructure, people, integration headcount, and data remediation, against approved budget | Program actuals vs. approval | Realized ÷ approved above 2× means bills 3 and 4 are uncounted |
| **The Lineage Gap** | Distance between dashboard-grade aggregates and model-grade continuous row-level data with provenance | Pipelines built after business-case approval | Any pipeline count above the business case's is the gap's invoice |
| **The Integration Tax** | Headcount added to realize headcount released elsewhere; its per-head cost and persistence | Integration-layer hires ÷ AI-titled hires | Above 2× means the tax is being paid; unmeasured means paid unknowingly |
| **The Work Multiplier** | Hours created ÷ hours removed per workflow per quarter, across build, evaluation, governance, exception, and refresh | Every business case | Absent from a business case means cost is uncounted; above 1 after Q6 means the workflow is not paying |
| **The Horizon Crossing** | Refresh interval ÷ honest payback | Longest-horizon deployment | Below 1 means the technology is rebuilt before it is profitable |
| **Refresh exposure** | Share of program spend a model or pattern refresh invalidates | Allocation across scaffolding, data, evaluation, integration | Above 40% means the program is building the saw's next teeth; under 20% is the quarter that profits |

---

## Sources and Grounding

The worldwide AI spending forecast — about $2.59 trillion in 2026, rising to about $3.49 trillion in 2027, with infrastructure at $1.43 trillion and $1.89 trillion respectively — is from a published industry forecast issued in May 2026. The survey figures — 97 percent with active initiatives, 5 percent reporting data readiness, 24 percent reporting broad or strong returns, and the ranked barriers of data access, quality, integration, and talent — are from a 2026 survey of ten thousand businesses by a commercial-data provider. The data-center financing figures — roughly $150 billion of required financing over a two-year window and about $600 billion borrowed since the prior year — are from a major bank's analysis and a wire service's tally, both cited in the first document of this lineage. The forward-deployed-engineer demand figures are from an executive-search study reported secondhand in July 2026 and are presented as directional. All exhibits marked illustrative or modeled are this outlook's own constructions with assumptions stated in place; they are not survey results and should be replaced with an organization's own figures as soon as those exist. Meridian is a composite.

---

**Lineage**

THE-SECOND-CLOCK · THE-CEREMONIAL-STACK · THE-CLOCK-AND-THE-CEILING · THE-ORACLE-TOLL · THE-WORK-BEFORE-THE-WORK

ERI Labs · Eric Ren · Jersey City, New Jersey · github.com/ericrenone · 2026
