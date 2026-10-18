---
title: "PeopleLens — From AI Prototyping to Product Adoption"
collection: portfolio
category: "Product & Design"
permalink: /portfolio/peoplelens-product-case-study/
excerpt: "A product case study on workflow discovery, AI experimentation, stakeholder feedback, and turning a working prototype into a tool the team continued using."
---

# PeopleLens
## From AI Prototyping to Product Adoption

*Why a technically functional AI tool wasn't adopted—and how understanding the real user problem led to a different solution.*

**Role:** Technical GTM Automation Intern  
**Organization:** PeopleLens  
**Timeline:** April–July 2026  
**Focus:** Product Discovery · Workflow Analysis · MVP Scoping · User Feedback · AI Evaluation · Adoption & Enablement

---

## 01. Project Overview

PeopleLens is an early-stage B2B AI company building coaching tools for sales organizations.

During my internship, I was tasked with helping a small GTM team scale personalized outreach. The business goal was ambitious: increase outreach capacity from roughly 35 messages per week toward 100, without sacrificing the quality of individual conversations.

I approached the challenge through workflow analysis, AI prototyping, stakeholder feedback, and internal tooling.

The project did not follow a straight line from idea to successful implementation.

My initial AI outreach generator worked technically, but it was not adopted into the team's daily workflow. Investigating why revealed a more fundamental problem: the team lacked a consistent way to identify strong personalization context before generating messages.

That discovery led me to build the **SMYKM Outreach Coach**, a Custom GPT that evaluated outreach quality, explained weaknesses, and coached users toward stronger personalization.

Unlike the initial generator, the coach became part of the interns' ongoing workflow and continues to be used.

This case study focuses on the product decisions, feedback, and iteration behind that shift.

---

## 02. Understanding the Business Problem

The team's outreach process was relationship-driven but difficult to scale.

Writing a personalized message required several steps:

1. Identify the prospect and review their CRM record.
2. Examine previous interactions across email and LinkedIn.
3. Research a relevant personalization angle.
4. Decide what kind of message to send.
5. Write the message in the appropriate voice.
6. Record the interaction and determine the next follow-up.

The internal workflow plan estimated that researching and drafting a message took approximately **7–8 minutes per contact**.

At 100 messages per week, manual research and writing alone could require more than 13 hours.

CRM administration added another source of effort. Follow-up tasks, engagement signals, and relationship history were fragmented across tools, making it harder to prioritize outreach.

### The initial product question

**How might we help the GTM team produce more personalized outreach in less time, without losing the human judgment that makes messages effective?**

The obvious answer seemed to be AI-generated drafts.

But before building, I needed to understand which parts of the workflow were genuinely repetitive and which parts depended on human context.

---


## 03. Workflow Discovery: Finding Automation Opportunities

Before building a solution, I mapped the team's existing outreach workflow to understand how people, data, and decisions moved across different tools.

The process involved prospect sourcing, CRM review, personalization research, message drafting, approval, sending, and follow-up management.

My goal was to identify **where automation could reduce repetitive work without disrupting the human judgment essential to personalized outreach.**

### Mapping the Existing Workflow

I created an end-to-end workflow diagram documenting how the team used HubSpot, LinkedIn, Google Sheets, and other GTM tools.

I then annotated the process to distinguish existing operations from opportunities for future automation.

<iframe
  src="/images/peoplelens/peoplelens_annotated_workflow.html"
  title="PeopleLens GTM Workflow Analysis"
  width="100%"
  height="750"
  style="border: 1px solid #ddd; border-radius: 8px;"
  loading="lazy">
</iframe>

[View Full Workflow Diagram](images/peoplelens_annotated_workflow.html)

*Workflow analysis showing the team's existing outreach process, manual decision points, and proposed automation opportunities. Not all proposed capabilities were implemented.*

### Identifying Opportunities

The workflow analysis helped me distinguish between repetitive operational tasks and activities that required human judgment.

| Activity | Product consideration |
|---|---|
| Contact records and engagement history | Integrate existing data rather than duplicate it |
| Contact classification | Use transparent, deterministic rules |
| Personalization research | Preserve human contextual judgment |
| Message composition | Explore AI-assisted drafting |
| Final outreach approval | Keep human ownership |
| Follow-up management | Consider additional automation in a later phase |

### The Key Product Decision

One important discovery was that the team already had established workflows around Google Sheets and HubSpot.

Introducing a completely new interface would add another system to learn and potentially create adoption friction.

Instead, I prioritized an MVP that worked with familiar tools and preserved the existing review process.

**Product takeaway:** Rather than automating the entire workflow at once, I focused on reducing the most immediate drafting bottleneck while minimizing disruption to how the team already worked.



### A first principle

**The goal was not to replace every manual step. It was to remove repetitive work without disrupting the parts of the process that already created value.**

*The annotated workflow map distinguishes existing activities from proposed automation opportunities. It represents process analysis and planning, not a claim that every annotated automation was delivered.*

---

## 04. MVP Decision: Augmented Authoring, Not Autonomous Outreach

My first solution focused on the time spent composing messages.

Instead of replacing the entire outreach process, I developed an AI-assisted drafting prototype.

The product concept was straightforward:

**Human selects the meaningful context → AI drafts the message → Human reviews and approves.**

### Key product decisions

**Use the existing Google Sheet**

The team was already comfortable working with a shared prospect sheet. Keeping it as the interface reduced the need for new training and avoided building a separate application.

**Separate relationship states**

Cold prospects, people who had replied, and previously engaged contacts required different types of messages.

The drafting workflow therefore needed to respect relationship context rather than generate the same type of outreach for everyone.

**Preserve the human quality gate**

The AI would prepare drafts, not send them automatically.

Final review remained with the person responsible for the prospect relationship.

**Separate voice configuration from code**

A reusable style document captured writing preferences so messaging guidance could be updated without requiring changes to the underlying Python implementation.

### What was delivered

I built a working Python and Claude API workflow that used real prospect data and integrated with the team's existing CRM and spreadsheet tools.

The prototype successfully generated drafts that were reviewed by the CEO.

However, it primarily required manual execution and did not become part of the team's regular daily process.

The technology worked. Product adoption did not.

---

## 05. Stakeholder Feedback: The Output Wasn't Good Enough

The initial drafts were considered underwhelming.

A natural response would have been to rebuild the architecture, switch models, or keep adjusting the prompts.

Instead, I reviewed the generated outputs alongside the inputs supplied to the system.

A pattern emerged.

Many personalization fields contained only weak contextual signals, such as a job title or recent career transition.

Those details were often factually accurate, but they did not explain why a particular recipient should find the message relevant.

The system had been designed to transform a human-selected hook into a polished message. It could improve the wording, but it could not manufacture meaningful relationship context that had never been provided.

### The underlying problem

**We had automated message composition before standardizing how users selected good personalization inputs.**

That distinction mattered.

The initial hypothesis was that the team needed help writing faster.

The feedback suggested that the team also needed help deciding **what was worth writing about**.

I documented the diagnosis and proposed prioritizing stronger evidence of personalization, such as a prospect's own posts, relevant interests, company context, or previous conversations, ahead of generic career information.

This changed how I thought about the solution.

Instead of asking only how to generate more messages, I began asking:

**How might we help team members consistently recognize and create high-quality personalized outreach?**

---

## 06. Product Iteration: Building the SMYKM Outreach Coach

The revised solution focused on coaching and evaluation rather than simply increasing draft volume.

I built a Custom GPT called **SMYKM Outreach Coach**, based on the principle *Show Me You Know Me*.

Its purpose was to help GTM team members write messages that demonstrated genuine knowledge of the recipient.

### Three core capabilities

**1. Evaluate an existing draft**

The coach scores a message on a five-point rubric and explains the reasoning behind its assessment.

**2. Identify what is missing**

If the context is insufficient, the assistant asks targeted questions rather than inventing details.

**3. Improve or generate outreach**

Once the intent and relevant information are established, the assistant can revise the draft or produce new email and LinkedIn versions.

### Designing an explainable evaluation framework

The scoring system translates qualitative outreach judgment into consistent criteria.

| Score | Evaluation |
|---|---|
| 1 — Generic | Could be sent to almost anyone |
| 2 — Light | Basic personalization with little depth |
| 3 — Relevant | Specific, accurate, and appropriate to the intent |
| 4 — Strong | Clearly tailored in tone, context, and CTA |
| 5 — Exceptional | Specific, natural, and genuinely compelling |

The coach also evaluates individual dimensions, including specificity, relevance, business connection, tone, conciseness, call to action, and accuracy.

### Designing around user context

I structured the experience around three questions:

**What is the intent?**

Keep warm, share soft value, or book a meeting.

**What is the relationship history?**

Has the prospect been contacted before, and what was discussed?

**Where does the personalization come from?**

Is the message grounded in something specific the prospect shared, or only in generic profile information?

These questions helped move quality assessment earlier in the process.

Instead of waiting until a generic email had been generated, users were encouraged to gather stronger context before rewriting.

### Why this was a different product

The first prototype helped compose messages.

The SMYKM Coach helped users make better decisions about the messages they wanted to send.

It was also designed as a teaching tool: users received explanations, not just scores and rewritten text.

This made it more useful for interns who were still developing their judgment about personalized outreach.

---

## 07. Supporting Adoption Through Clear Processes

I also created a practical outreach playbook for interns.

The goal was to reduce ambiguity around contact classification, outreach sequence, message structure, and follow-up.

### A simple decision framework

The playbook asked two questions:

- Has the prospect replied on LinkedIn?
- Have we previously emailed the prospect?

Those answers defined four operational cases.

| Case | Relationship context | Recommended approach |
|---|---|---|
| 1 | No LinkedIn reply; prior email history | Continue the existing email thread |
| 2 | No LinkedIn reply; no email history | Begin with personalized email outreach |
| 3 | LinkedIn reply and prior email history | Continue the established conversation |
| 4 | LinkedIn reply; no email history | Prioritize the warm LinkedIn relationship |

Each case included suggested outreach sequencing and timing.

### Reducing unnecessary complexity

The playbook standardized a three-part message structure:

**Personal hook → PeopleLens connection → Simple ask**

This separated the part requiring genuine research from the parts that could be more consistent.

I also documented a pre-send checklist so team members could verify personalization, relationship context, CTA appropriateness, and follow-up tracking.

Together, the coach and playbook made outreach expectations easier to communicate and apply.

The SMYKM Outreach Coach was made available to the team, and interns have continued using it in their outreach work.

---

## 08. Prioritizing the Roadmap

The initial workflow analysis also identified opportunities for deeper automation.

These included:

- Consolidating engagement signals from different platforms
- Prioritizing prospects based on engagement activity
- Scheduling AI-assisted draft preparation
- Automating CRM task completion and follow-up reminders
- Using edits and new engagement data to inform subsequent outreach

I documented a proposed roadmap for these capabilities, including staged implementation and resource considerations.

However, the complete automated engine was not delivered during my internship.

In retrospect, the experience reinforced an important prioritization lesson.

Automating additional stages would have increased system complexity without necessarily addressing the quality and adoption problem we had already observed.

**Improving the human input process was a more relevant next step than simply adding more automation.**

The broader automation roadmap remained a potential future direction, while the SMYKM Coach addressed a more immediate and observable user need.

---

## 09. Outcomes: What Worked and What Didn't

This project produced mixed but instructive results.

### The initial prototype

The AI-assisted drafting workflow successfully ran on real data and demonstrated the technical feasibility of integrating CRM context with language generation.

However, it did not become part of the team's regular daily workflow.

The experience exposed a mismatch between a technically functional solution and what users actually needed to achieve consistently useful results.

### The revised solution

I built and delivered the SMYKM Outreach Coach, complete with an evaluation rubric and user guidance.

**The coach continues to be used by interns**, providing an observable indication of adoption beyond the initial delivery.

I also delivered an outreach playbook and workflow documentation to support more consistent team execution.

### Business context

During the broader GTM improvement period, monthly booked meetings increased from approximately **3 in June to 6 in July**.

This was a team-level observation, not a controlled experiment. The increase cannot be attributed specifically to my prototype, the SMYKM Coach, or any single change to the outreach process.

I also do not have verified quantitative measures of the coach's effect on message quality, response rates, or time saved.

The strongest evidence of the product iteration's usefulness is the continued use of the coach by its intended users.

### What was delivered versus proposed

| Delivered | Not fully implemented |
|---|---|
| Working AI-assisted drafting prototype | Fully scheduled autonomous outreach engine |
| Stakeholder feedback and input-quality diagnosis | Comprehensive automated signal prioritization |
| SMYKM Custom GPT with evaluation rubric | End-to-end automated CRM task management |
| Outreach playbook and team handoff materials | Continuous automated refinement from logged user edits |
| Workflow mapping and future roadmap | Full deployment of every proposed automation stage |

This distinction is important: the result was not a fully automated GTM system, but a set of working tools, validated lessons, and a more useful approach to supporting the team's outreach process.

---

## 10. What I Learned About Product Management

This internship challenged my assumption that building a technically capable solution was enough to solve a business problem.

**A working prototype is not the same as an adopted product.**

The initial system did what it was designed to do, but its output quality and workflow fit were not strong enough to drive daily use.

**User feedback can reveal that the original problem definition was incomplete.**

The weak drafts were not simply a model-performance issue. They exposed an unmet need for stronger personalization research and shared quality standards.

**The best iteration may solve a different part of the workflow.**

The SMYKM Coach did not attempt to replace the entire outreach process. It helped users improve their judgment within it.

**Adoption depends on fitting real behavior.**

A focused tool with clear guidance can be more useful than an ambitious automation architecture that users are not ready to incorporate into their daily routine.

This experience strengthened my interest in product work that connects business needs, user behavior, technical feasibility, and iterative delivery.

My biggest takeaway was that the goal of applied AI is not to automate the maximum number of steps.

**It is to identify the right problem, build a practical solution, and create something people actually use.**

---

### Related Technical Case Study

This case study focuses on workflow discovery, product decisions, stakeholder feedback, and adoption.

For the Python implementation, LLM prompting, CRM integration, and engineering tradeoffs, see my [PeopleLens Outreach Automation technical case study](https://github.com/Dqy719/dqy719.github.io/blob/master/_portfolio/peoplelens-outreach-automation.md).

---

*Project materials are presented in summarized form to protect internal company information. Technical capabilities, product adoption, planning targets, and business outcomes are distinguished throughout.*
