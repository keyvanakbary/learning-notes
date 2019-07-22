# [Kanban: Successful Evolutionary Change for Your Technology Business](https://www.goodreads.com/book/show/8086552-Kanban)

- [Solving an agile manager's dilemma](#solving-an-agile-managers-dilemma)
- [Kanban](#kanban)
- [Recipe for success](#recipe-for-success)
- [From the worst to the best in five quarters](#from-the-worst-to-the-best-in-five-quarters)
- [A continuous improvement culture](#a-continuous-improvement-culture)
- [Mapping the value stream](#mapping-the-value-stream)
- [Coordination with Kanban systems](#coordination-with-kanban-systems)
- [Establishing a delivery cadence](#establishing-a-delivery-cadence)
- [Establishing an input cadence](#establishing-an-input-cadence)
- [Setting work-in-progress limits](#setting-work-in-progress-limits)
- [Establishing service level agreements](#establishing-service-level-agreements)
- [Metrics and management](#metrics-and-management)
- [Operations review](#operations-review)
- [Starting a Kanban change initiative](#starting-a-kanban-change-initiative)
- [Bottlenecks and non-instant availability](#bottlenecks-and-non-instant-availability)
- [An economic model for Lean](#an-economic-model-for-lean)
- [Sources of variability](#sources-of-variability)
- [Issue management and escalation policies](#issue-management-and-escalation-policies)

## Solving an agile manager's dilemma

> Our deadlines were set by managers without regard to engineering complexity, risk, or project size.

> Changes suggested out of context would be rejected by the workers who lived and understood the project context.

Drum-Buffer-Rope is an example of a class of solutions known as pull systems. The side effect of pull systems is that they limit work-in-progress (WIP) to some agreed-upon quantity, thus preventing workers from becoming overloaded.

## Kanban

_Kan-ban_ is a Japanese word that literally means "signal card" in english. Cards are used as a signal to tell an upstream step in the process to produce more. Kanban is fundamental to the _kaizen_ (continuous improvement).

Workflow visualisation, work item types, cadence, classes of service, specific management reporting, and operation reviews is what defines the Kanban Method.

### Kanban system

A number of cards equivalent to the agreed capacity of a system are placed in circulation. One card attaches to one piece of work. Each card acts as a signalling mechanism. A new piece of work can be started only when a card is available. The free card is attached to a piece of work and follows it as it flows through the system. When there are no more free cards, no additional work can be started. Any new work must wait in a queue until a card becomes available. When some work is completed, its card is detached and recycled. With a card now free, a new piece of work in the queuing can be started.

This is known as a pull system because new work is pulled into the system when there is capacity to handle it, rather being pushed into the system based on demand. A pull system cannot be overloaded if capacity, as determined by the number of signal cards in circulation, has been set appropriately.

### Kanban in software development

In software development the cards do not actually function as signals to pull more work. They represent work items.

Card walls have become a popular visual control mechanism. These are not inherently Kanban systems, they are merely visual control systems. **If there is no explicit limit to work-in-progress and no signalling to pull new work through the system, it is not a Kanban system.**

### Why use Kanban

We use it in order to limit team's work-in-progress to a set capacity and to balance the demand on the team. By providing visibility onto quality and process problems, it makes obvious the impact of defects, bottlenecks, variability, and economic costs on flow and throughput.

Kanban facilitates emergence of a highly collaborative, high-trust, highly empowered, continuously improving organisation.

### Kanban and Lean

Kanban uses five core properties to create an emergent set of Lean behaviours in organisations:
* Visualise workflow
* Limit work-in-progress
* Measure and manage flow
* Make process policies explicit
* Use models to recognise improvement opportunities (like Theory of Constraints, Systems Thinking, _muda_)

---

Kanban is not a software development lifecycle methodology or an approach to project management. It requires that some process is already in place so that Kanban can be applied to incrementally change the underlying process.

Your situation is unique and you deserve to develop a unique process definition tailored and optimised to your domain.

## Recipe for success

Asking people to change their behaviour creates fear and lowers self-esteem, as it communicates that existing skills are clearly no longer valued.

The recipe for success presents guidelines for a new manager adopting a new existing team.
* **Focus on quality**: Excessive defects are the biggest waste in software development.
  - Both agile and traditional approaches to quality have merit
  - Code inspections improve quality
  - Collaborative analysis and design improve quality
  - The use of design patterns improves quality
  - The use of modern development tools improves quality
  - Reducing the quality of design-in-progress boosts software quality
* Reduce work-in-progress
* Deliver often
* Balance demand against throughput
* Prioritise
* Attack sources of variability to improve predictability

Working down the list, there is gradually less control and more collaboration required with other downstream and upstream groups. The final step it's the one that separates the truly great technical leaders from the merely competent managers.

### WIP, lead time, and defects

Longer lead times (from starting to done) seem to be associated with significantly poorer quality. In fact, an approximately 6.5x increase in average lead time resulted in greater than 30x in initial defects. Longer average lead times result from greater amounts of work-in-progress. Hence, the management leverage point for improving quality is to reduce the quantity of work-in-progress. **Shorter iterations will drive higher quality.**

### Frequent releases build trust

Reducing WIP shortens lead time and frequent releases build trust with external teams (social capital). Trust is event driven and that small, **frequent gestures or events enhance trust more than larger gestures made only occasionally.**

Small gestures often cost nothing but build more trust than large, expensive gestures bestowed occasionally.


### Tacit knowledge

Information discovery in software development is tacit in nature and is created during collaborative working sessions, face-to-face. Our minds have a limited capacity to store all this tacit knowledge. Knowledge depreciates with time, so shorter lead times are essential.

### Balance demand against throughput

By setting the rate at which we accept new requirements, we are effectively fixing our work-in-progress to a given size. As work is delivered, we will pull new work from the people creating demand.

### Create slack

Slack capacity created by the act of limiting work-in-progress enables improvement. **You need slack to enable continuous improvement.** You need to balance demand against throughput and limit the quantity of work-in-progress to enable slack.

In order to have slack, you must have an unbalanced value stream with a bottleneck resource. Optimising for utilisation is not desirable.

### Prioritise

At this point, management attention can turn to optimising the value delivered rather than merely the quantity of code delivered.

**Prioritisation should not be controlled by engineering.** Improving prioritisation requires the product owner, business sponsor, or marketing department. Engineering can seek only to influence how prioritisation is done.

### Building maturity

First, learn to build high-quality code. Then reduce the work-in-progress, shorten lead times, and release often. Next, balance demand against throughput, limit work-in-progress, and create slack to free up bandwidth, which enable improvements. Then, with a smoothly functioning and optimising software development capability, improve prioritisation to optimise value delivery.

### Attack sources of variability to improve predictability

Reducing variability in software development requires knowledge workers to change the way they work, to learn new techniques and change their personal behaviour. All of this is hard. Variability creates a greater need for slack.

## From the worst to the best in five quarters

### Adjusting policies

> So how prioritisation was facilitated? If something was important and valuable, it was selected for the input queue from the backlog; if it wasn't then it wasn't selected. Any item older than six months was purged from the backlog.

> The weekly meeting with product owners also disappeared, when a slot became available in the input queue. It would alert the product owners to pick again.

## A continuous improvement culture

Continually improving quality, productivity, and customer satisfaction is known as "kaizen culture".

Workforce is empowered. Individuals feel free to take action; free to do the right thing without fear. Management is tolerant with failure and individuals are free to self-organise around the work they do and how they do it. Everyone looks out for the performance of the team and the business above themselves.

A kaizen culture has a high level of social capital, a trusting culture where individuals respect each other. High-trust cultures tend to have flatter structures than lower-trust cultures. It is the degree of empowerment that enables a flatter structure to work effectively. Achieving kaizen culture may enable elimination of wasteful layers of management and reduce coordination costs as a result.

**Introducing a radical change is harder than incrementally improving an existing one.**

### Unanticipated effects of introducing Kanban

> The physical board had a huge psychological effect. By attending standup each day, team members were exposed to a sort of time-lapse photography of the flow work across the board.

### Sociological change

Kanban method appear to achieve a kaizen culture faster and more effectively than typical Agile software development teams. Kanban enables every stakeholder to see the effects of his or her actions or inactions.

## Mapping the value stream

Kanban drives change by optimising your existing process. The main change will be quantity of WIP and the interface to add interaction with upstream and downstream parts of your business. So you must work with your team to map the value stream as it exists. Map the process they actually use.

### Defining a start and end point for control

Define interface points with upstream and downstream partners.

### Work item types

Identify the types of work that arrive at that point in any others that exist within the workflow that will need to be limited. A few examples:
* Requirement
* Feature
* User story
* Use case
* Change request
* Production defect
* Maintenance
* Refactoring
* Bug
* Improvement suggestion
* Blocking issue

### Drawing a card wall

Once you have understood your workflow by sketching or modelling it, start to define a card wall by drawing columns on the board that represent the activities performed, in the order hey are performed.

Where to put buffers: do not try to second-guess the location of bottleneck that will require a buffer. Rather, implement a system and wait for the bottleneck to reveal itself, then make changes to introduce a buffer.

### Demand

For each type of work identified, you should make a study of the demand.

Decide to allocate capacity within the Kanban system to cope with that demand.

> The allocation is 60% change requests, 10% code refactorings, and 30% production text changes

### Anatomy of a work item card

The information on the cards must facilitate the pull system and empower individuals to make their own pull decisions.

Cards may include:
* Electronic tracking number as a link to the electronic card
* Title of the item
* Date the ticket entered the system. Facilitates first-in, first-out queuing for standard class of service
* Name of assigned person. Name tags, stickers or magnets are a good idea to represent members.

Basically sufficient information to facilitate project-management decisions without the intervention or direction of a manager.

### Electronic tracking

For teams that are distributed geographically, or those who have policies that allow team members to work from their homes, electronic tracking is essential. They allow you to visualise the work item tracking as if it were on a card wall.

### Coping with concurrency

Two or more activities can happen concurrently. There are two ways for coping with this.
* One is not to model it at all; just leave a single column where both activities can occur together. Using different colours or shapes of ticket to show the different activities.
* The other option is to split the board vertically into two (or more) sections
  ```
  ┌─────────────┬────────────────┬────────────────┬────────────┐
  │ INPUT QUEUE │   ANALYSIS     │ DEV & TEST DEV │ TEST READY │
  ├─────────────┼─────────┬──────┼─────────┬──────┼────────────┤
  │             │ IN PROG │ DONE │ IN PROG │ DONE │            │
  ·             ·         ·      ·         ·      ·            ·
  ```

### Coping with unordered activities

Usually happens in highly innovative and experimental work.

First, simply have a single column as a bucket for the activities and do not explicitly track on the board which of them is complete.
Second, tickets have to move vertically up and down the column they are pulled into each of the specific activities. When the activity is complete, the checkbox can be filled to visually signal that the item is ready to be pulled to another activity in the same column. If all the checkboxes are filled, the item is ready to be pulled to the next column on the board or it can be moved to "done".

    ┌──────────────────────────┐
    │ DEV & TEST DEV           │
    ├───────────────────┬──────┤
    │ IN PROGRESS       │ DONE │
    ├───────────────────┼──────┤
    │ ┌───────────────┐ │      │
    │ │ ☒ UI DESIGN   │ │      │
    │ │ ☒ SECURITY    │ │      │
    │ │ ☐ PERSISTENCE │ │      │
    │ │ ☐ BIZ LOGIC   │ │      │
    · └───────────────┘ ·      ·

## Coordination with Kanban systems

### Visual control and pull

You are likely to want to visually capture the assigned staff member, the start date, the electronic tracking number, the work item type, the class of service, and some status information, such as whether the item is late.

Visually communicate enough information to make the system self-organising and self-expediting ad the team level. It should enable team members to pull work without direction from their manager.

### Electronic tracking

As an alternative or as a supplement

### Daily standup meetings

In Agile a typical standup meeting is for a single team of up of twelve people, usually about six. Involving answering three questions: **What did you achieve yesterday? What will you do today? Are you blocked or do you need assistance?**

In Kanban, the wall contains all the information so the focus will be on the flow of work. The facilitator will "walk the board". Work backward, from right to left (in direction of the pull), through the tickets on the board. Making emphasis on items that are blocked, delayed due to defects or stuck for a few days. There will also a call for any other blocking issues that are not on the board and for anyone who needs help to speak up. Mature teams do not need to walk through every card. They will tend to focus only on the tickets that are blocked or have defects.

### The after meeting

Huddles of small groups of 2 or 3 people. Team members that want to discuss something on their minds. After meetings generate improvement ideas and result in process tailoring and innovation.

### Queue replenishment meetings

These serve the purpose of prioritisation in Kanban. They happen at regular intervals providing cadence for queue replenishment.
Ideally they will involve several product owners or business people from potentially competing groups. The tension becomes a positive influence.
Mature teams evolve towards demand-driven prioritisation where stakeholders can be available on demand.

### Release planning meetings

Basically plan downstream delivery.

### Triage

Triage is used to classify bugs that will be fixed, and their priority, versus bugs that will not be fixed.

The most useful application of triage is the backlog of items waiting to enter the system.

The purpose of triaging the backlog is to reduce its size. A good rule of thumb is to trim the backlog for anything more than 3 months of work.

There is a relationship between the size of the backlog, the volatility of the domain and the delivery velocity.

### Issue log review and escalation

When work items are impeded, an issue work item will be created. The issue will remain open until the impediment is removed and the original work item can progress through the system. Issues that are not progressing should be escalated.

### Sticky buddies

Each person not physically present in the office and able to move the sticky note on the card wall, make a peer-to-peer agreement with someone who would be present in the office to act as their delegate.

### Synchronising across geographic locations

The key coordination across multiple site is to use an electronic system. It isn't enough to have only a card wall. It will be necessary to keep physical card walls synchronised on a daily basis. It is important to assign someone to take responsibility to this at each location.

## Establishing a delivery cadence

Kanban avoids any dysfunction introduced by artificially forcing things into time-boxes. It decouples the time it takes to create a user story from the delivery rate. While some work is complete and ready for delivery, some other work will be in progress. It makes sense to question how often prioritisation (and perhaps planning estimation) should happen.

### Coordination costs of delivery

Activities involved in successfully delivering software need to be accounted for, planned, scheduled, resourced and then actually performed.

#### Efficiency of delivery

To be more efficient, focus on reducing waste by reducing coordination and transaction costs in order to make the batch size efficient.

#### Agreeing a delivery cadence

You, the team, and the organisation are aware of the costs of making a delivery and are capable of making some form of ration assessment about the acceptable frequency of delivery.

#### Improve efficiency to increase delivery cadence

Choose conservatively initially. Let the organisation prove that it can achieve this level of consistency. After, improve configuration management.

Reducing coordination and transaction costs is at the hart of Lean. Deliver more value to your customers more often.

#### Making on-demand deliveries

Regular delivery helps to build trust. Lack of predictability destroys trust. Choose a regular cadence except in circumstances in which trust already exists, where near-continuous deployment is desirable.

Under special circumstances, it makes sense to plan a special, off-cycle release. It should be treated as exceptional.

## Establishing an input cadence

### Agreeing on a prioritisation cadence

Weekly is a good schedule for prioritisation cadence. It provides frequent interaction with business owners, builds trust through the interaction involved and enables the players to move the pieces once a week.

It's a collaborative experience, there is transparency to the work and to the work flow; progress can be reported every week; everyone gets to feel that they are contributing to something valuable.

### Efficiency of prioritisation

Some teams sit together, so there is no need for a meeting, a quick discussion across the desk will be enough. Other teams may have people in multiple zones, so weekly meetings may not be so easily scheduled.
As general advice, more frequent prioritisation is desirable. It allows the input queue to be smaller, and, as a result, there is less waste in the system. WIP is lower and therefore a lead time is shorter.

### Transaction costs of prioritisation

Activities such as estimation, business plan preparation, and candidate selection from the backlog, are preparatory work for prioritisation. These are the transaction costs of prioritisation. It is desirable to keep these costs low.

### Improve efficiency to increase prioritisation cadence

Because of the coordination-cost effect, Agile planning methods are efficient only for small teams focused on single systems and product lines.

By choosing to eliminate estimation, transaction costs and coordination costs of prioritisation are reduced. This reduction facilitates frequent prioritisation or on-demand prioritisation.

### On-demand prioritisation

Each week product managers would refill the empty slots in the input queue.

Choose on-demand prioritisation when you have a relatively high level of organisation maturity, low transaction costs, and low coordination costs. Otherwise, use a regularly scheduled prioritisation meeting.

## Setting work-in-progress limits

WIP limits should be agreed upon by consensus with up- and downstream stakeholders and senior management.

### Limits for work tasks

One task at a time should be ideal. As items could be blocked and task switching should be allowed, some research suggest that two items in progress per knowledge worker is optimal.

You may encounter resistance to the notion that one item per person, pair or small team is the correct choice.

#### Limits for queues

When work is completed and waiting to be pulled by the next stage it is said to be "queuing".

#### Buffer bottlenecks

The bottleneck in your workflow may require a buffer in front of it. Buffers and queues smooth flow and improve predictability of lead time.

Buffers also ensure that people are kept working and provide for a greater utilisation. **Do not sacrifice predictability in order to achieve agility of quality.**

#### Input queue size

It can be directly determined from the prioritisation cadence and the throughput, or production rate in the system.

Queue and buffer sizes should be adjusted empirically as required.

#### Unlimited sections of workflow

With Drum-Buffer-Rope, all work stations downstream from the bottleneck have unlimited WIP.

             BOTTLENECK
             ↓
    ☺··☺··☺··☹·☺·☺
    └────────┘           DRUM-BUFFER-ROPE

    ☺·☺····☺·☹·☺···☺
    └──────────────┘     CONWIP

    ☺··☺··☺··☹·☺···☺     
    └────────┴─────┘     DBR + CONWIP

    ☺··☺··☺··☹··☺··☺
    └──┴──┴──┴──┴──┘     KANBAN


With a Kanban system, most or all the stations in the workflow have WIP limits. The local WIP limit with the Kanban system will stop the line quickly keeping the system from becoming overloaded.

#### Don't stress your organisation

In more mature organisation that suffer few unexpected issues you can be more aggressive with your WIP-limit policies. For more chaotic organisations, you will want to introduce looser limits initially with greater WIP and an intention to reduce it later.

#### It's a mistake not to set a WIP limit

The tension created by imposing a WIP limit is positive tension. It forces discussion about the organisation's issues and dysfunctions. Without WIP limits, progress and process improvement is slow.

#### Capacity allocation

                ┌───────┬────────────────┬────────────────┬─·
    ALLOCATION  │ INPUT │   ANALYSIS     │ DEV & TEST DEV │
    TOTAL = 20  │ QUEUE ├─────────┬──────┼─────────┬──────┼─·
                │       │ IN PROG │ DONE │ IN PROG │ DONE │
                ├───────┼─────────┼──────┼─────────┼──────┼─·
    CHANGE REQ  │       │         │      │         │      │
    12          │       │         │      │         │      │
                ├───────┼─────────┼──────┼─────────┼──────┼·
    MAINTENANCE │       │         │      │         │      │
    2           │       │         │      │         │      │
                ├───────┼─────────┼──────┼─────────┼──────┼·
    PROD DEFECT │       │         │      │         │      │
    6           │       │         │      │         │      │
                ·       ·         ·      ·         ·      ·

Capacity allocation allows us to guarantee service for each type of work received by the Kanban system. It is important to complete some demand analysis to facilitate reasonable allocation of WIP limits on swim lanes for each type of work.

## Establishing service level agreements

Some requests are needed more quickly than others, while some are more valuable than others. **By quickly identifying the class of service for an item, we are spared the need to make a detailed estimate or analysis.** Policies associated with a class of service affect how items are pulled through the system. Class of service determines priority.

### Typical class-of-service definitions

Based on business impact, each class of service comes with its own set of policies. You might want to offer up to a maximum of six such classes. Common ones are:
* **Expedite** (white): Offers a vendor the ability to say "Yes!" in difficult circumstances to meet a customer need. The business makes a choice to realise value on a specific sale at a cost of both delaying other orders and incurring additional carrying costs of higher inventory levels.
* **Fixed delivery date** (purple): Requests of this nature carry a significant cost delay whether direct or indirect. There would be a date when a penalty will happen.
* **Standard class** (yellow): One common Kanban system design scheme separates work types by size, such a small, medium, and large. A different service level agreement for standard class items of each size can be offered. Peg: small items to be processed in 4 days, medium size items 1 month, and large items 3 months.
* **Intangible class** (green): There is no cost of delay within the timeframe that it might take to deliver the item, such as platform replacement. Platform replacement, although it has a low immediate cost of delay, gets displaced by other work with greater and more immediate cost of delay.

### Policies for class of service

Different colours of tickets or different swim lanes on the card wall are the most common. Any staff member can use simple prioritisation policies without management intervention.

Policies:
* **Expedite policies**
  - Only one expedite request is permitted at any given time.
  - Other work will be put on hold.
  - WIP limit may be exceeded in order to accommodate the expedite.
* **Fixed delivery date policies**
  - Receive some analysis an estimate of size, it may be broken up into smaller items.
  - They are pulled in preference over other, less risky items.
  - Must adhere to the WIP limit.
  - If a fixed delivery date item gets behind, it might be promoted to an expedite request.
* **Standard class policies**
  - Prioritised based on an agreed-upon mechanism, such as democratic voting, and typically selected based on their cost of delay or business value.
  - First in, first out (FIFO) queuing as they are pulled through the system.
  - No estimation is performed.
  - May be analysed for order of magnitude in size.
  - Large items my be broken down into smaller items. Each item may be queued and flowed separately.
* **Intangible class**
  - Prioritised based on an agreed-upon mechanism, such as democratic voting, and typically selected based on their cost of delay or business value.
  - Members may choose to pull an intangible class item regardless of its entry date.
  - No estimation is performed.
  - May be analysed for size.

### Determining a service delivery target

Service-level agreements that offer target lead time with due-date performance metric allows us to avoid costly activities such as estimation.

To determine the target lead time (from first selection to delivery), it helps to have some historical data. If you don't have any make reasonable guess.

> 30% of all requests were late compared to the target lead time. Due date performance = 70%

### Assigning a class of service

The class should be assigned when the item is selected into the input queue.

                    5   +        4       +   3   +        4       +   2   +   2  = 20 TOTAL
                ├───────┼────────────────┼───────┼────────────────┼───────┼──────┼─────────┼·
    EXPEDITE    │ INPUT │   ANALYSIS     │  DEV  │   DEVELOPMENT  │ BUILD │ TEST │ RELEASE │
    █ +1 = 5%   │ QUEUE ├─────────┬──────┤ READY ├─────────┬──────┤ READY │      │  READY  │
                │       │ IN PROG │ DONE │       │ IN PROG │ DONE │       │      │         │
    FIXED       ├───────┼─────────┼──────┼───────┼─────────┼──────┼───────┼──────┼─────────┼·
    ▒  4 = 20%  │   ░   │    ░    │      │   ▓   │    ░    │      │   ░   │  ▓*  │    ░    │
                │       │         │   ░  │       │         │      │       │      │         │
    STANDARD    │   □   │    ░    │      │   ▒*  │    ░    │      │   ▓   │  ▒   │    ▒    │
    ░ 10 = 50%  │       │         │      │       │         │      │       │      │         │
                │   □   │    ░    │      │   ▓   │    █    │      │       │      │    ░    │
    INTANGIBLE  │       │         │      │       │         │   ▒  │       │      │         │
    ▓  6 = 30%  │   □   │         │      │   ░   │         │      │       │      │         │
                │       │         │      │       │         │      │       │      │         │
    □ SLOT      │   □   │         │      │       │         │      │       │      │         │
    * BLOCKED   ·       ·         ·      ·       ·         ·      ·       ·      ·         ·

Now that we have allocated capacity to different classes of service, the input queue replenishment activity is complicated.

If the costs associated are high, we may choose to leave the slot empty. It may make sense to effectively reserve capacity for a fixed delivery date item. If risks are low, we may choose to fill the slot with a standard class item.

## Metrics and management

We are less interested in reporting on whether a project is "on-time" or a specific plan is being followed. **What's important is to show that the system is predictable and is operating as designed.**

We want to show how well we perform against the class-of-service promises. What's the due-date performance? We want to track the trend over time.

### Tracking WIP

The bands on the chart should be smooth and their height should be stable.

### Lead time

How predictably our organisation delivers against the promises in the class-of-service definitions. How quickly did we get it from the order into production?

### Due-date performance

The item was delivered on time.

### Throughput

Number of items that were delivered in a given time period, such as one month. It should be reported as a trend over time. The goal is to continually increase it. You may be able to report the relative size.

You may be able to report the value of the work delivered as a dollar amount.

Throughput is used as an indicator of how well the system is performing an to demonstrate continuous improvement.

### Issues and blocked work items

A cumulative-flow diagram of reported impediments overlaid with a graph of the number of WIP items that have become blocked. This chart can be used on a day-to-day basis alert of impediments and their impact.

### Flow efficiency

Track assigned time (to an individual) against time spent blocked and queuing. Show how much potential there is for improvement.

### Initial quality

It makes sense to report the number of escaped defects as a percentage against the total WIP and throughput.

### Failure load

Items we process because of earlier poor quality.

## Operations review

### Main agenda

* Each manager gets 8 minutes for a presentation on their department's performance.
* Project specific updates from program-management office.
* Team managers get 5 minutes to quickly present their metrics plus a few minutes for questions, comments and suggestions on the metrics presented.
  - Defect rates
  - Lead times
  - Throughput
  - Value-added efficiency
  - Maybe some extra metrics to review some aspect of the process


### Keystone of lean transition

Ops Review is the keystone of Lean transition and Kanban method implementation. It provides the feedback loop that enables growth of organisation maturity and organisation-level continuous improvement.

### Appropriate cadence

Operations review have to be monthly. Quarterly is too seldom to really drive an improvement program, review tends to be superficial.

The loss of a feedback loop reduces the opportunities for reflection and adaptation that could lead to improvements.

### Demonstrating the value of managers

Operations review trains the workforce to think like managers, to understand when to make interventions and when to stand back and leave the team to self-organise.

### Organisational focus fosters kaizen

Organisation-wide ops review fosters institutionalisation of changes, improvements and processes. Teams want to demonstrate how they can help the organisation with better predictability, more thought, shorter lead times, lower costs, and higher quality.

## Starting a Kanban change initiative

**The main reason for adopting Kanban is change management. Everything else is secondary.**

### Cultural change rather than a managed-change initiative

It is a significant shift away from how a typical Agile transition is planned and managed. There is no planned initiative, no assessments. Ideally, there is no end. Leadership drives a continuous process, encouraging incremental changes. There is a gradual transformation toward a kaizen culture.

### Goals for our Kanban system

**Change with minimal resistance must be our first goal.**

* **Goal 1: Optimise existing processes**. Existing processes will be optimised through introduction of visualisation and limiting work-in-progress to catalyse changes.
* **Goal 2: Deliver with high quality**. Limiting WIP and allowing us to define policies around what is acceptable before a work item can be pulled to the next step in the process.
* **Goal 3: Improve lead time predictability**. The amount of WIP is directly related to lead time, so keep WIP small.
* **Goal 4: Improve employee satisfaction**. There is a huge impact on performance that comes with a well motivated and experienced workforce.
* **Goal 5: Provide slack to enable improvement**. Without slack (space between work items), team members cannot take time to reflect upon how they do their work and how they might do it better.
* **Goal 6: Simplify prioritisation**. Maximise business value and minimise risk and cost. In order to respond to change in the market and evolving events, it is necessary to reprioritise. What is needed is a prioritisation scheme that delays commitments as long as possible and that asks a simple question that is easy to answer. Kanban provides this by asking the business owners to refill empty slots in the queue while providing them with a reliable lead-time and due-date performance metric.
* **Goal 7: Provide transparency on the system design and operation**. Transparency into the performance of the team, provide customers with confidence. Transparency into the process, let everyone involved see the effects of their actions or inactions. People will be more reasonable.
* **Goal 8: Design a process to enable emergence of "high-maturity" organisation**. Seek predictability above all else, coupled with business agility and good governance. Success at the senior-executive level depends a lot on trust, and trust requires reliability.

### Steps to get started

1. Map the value stream
2. Define some point where you want to control input. Define what is the upstream of that point and the upstream stakeholders.
2. Define some exit point beyond which you do not intend to control. Define what is downstream of that and who the downstream stakeholders are.
3. Define a set of work item types based on the types of work requests that come from the upstream stakeholders.
4. Analyse the demand for each work item type. Observe the arrival rate and variation.
5. Meet with the upstream and downstream stakeholders.
6. Discuss policies around capacity and get agreement on WIP limit.
7. Discuss and agree on an input-coordination mechanism, such as a regular prioritisation meeting, with the upstream partners.
8. Discuss and agree on a release/delivery-coordination mechanism, such as a regular software release, with downstream partners.
9. You might need to introduce the concept of different classes of service.
10. Agree on a lead-time target for each class of service of work items (SLA).
11. Create a board/card wall to track the value stream.
12. Optionally, create an electronic system to track and report the same.
12. Agree with the team to have a standup meeting every day in front of the board; invite up- and downstream stakeholders but don't mandate their involvement.
13. Agree to have a regular operations review meeting for retrospective analysis of the process; invite up- and downstream stakeholders but don't mandate their involvement.
14. Educate the team on the new board, WIP limits, and the pull system.

### Kanban strikes a different type of bargain

Kanban does not seek to make a promise and commit based on something that is uncertain. The typical implementation involves agreement that there will be regular delivery of high-quality working software, with complete transparency, daily visibility of progress and offering frequent opportunities to select the most important new items for development.

A commitment around scope, schedule, and budget is indicative of a one-off transaction. It implies that there is no ongoing relationship; it implies a low level of trust.

Kanban is based on the notion that the team will stay together and engage in a supplier relationship over a long period of time.

### WIP limits

Getting our partners to agree on a WIP limits is a vital element. There will be a day when our partners ask us to take some additional work and we will be able to respond that we have an agreed-upon WIP limit. We would be able to ask "which one of the current items in progress would you prefer that we drop in order to start your new item?"

### Prioritisation

An agreement to have a regular replenishment meeting and mechanism for how new work will be selected.

### Lead time and classes of service

It helps to have some historical data on past performance.

The lead-time target you are agreeing to for each class of service should be presented as a target rather than a commitment. If you do need to agree that lead time in the SLA represent a commitment, you should add a margin for safety. A lower level of trust results in a direct economic cost.

## Bottlenecks and non-instant availability

A bottleneck in a process flow is anywhere that a backlog of work builds up waiting to be processed.

### Capacity-constrained resources

#### Elevation actions

A natural reaction is to hire another person to help, adding capacity so that bottleneck is removed. However, **elevating a capacity-constrained resource ought to be the last resort**. Hiring more people slows a project down.

#### Exploitation/protection actions

Rather than jump immediately to elevation, is better to first find ways to fully exploit the capacity of the bottleneck resource. On a highway analogy, speed does not really affect throughput. It's the gap between vehicles that is most important. Variability in the system has a huge impact on throughput.

Fortunately, in our office, our capacity-constrained resources are affected by variability that we _can_ do something about. We can seek to keep the individual busy working on value-added work by minimising the non-value-added (wasteful) activities required of that person.

If you find yourself saying "invest", you are generally talking about an elevation action. Adding resources is not the only way to elevate capacity. **Automation is a good an natural strategy for elevation.** It does also reduce the variability: repeatable tasks and activities are repeated with digital accuracy.

A strong organisational capability at issue identification, escalation, and resolution is essential for effective exploitation of capacity-constrained bottlenecks.

If there are several issues blocking current work, they should get the highest priority. Kanban will help to raise awareness.

One more technique is to ensure that the resource is never idle. **The most common way to avoid such idle time is to protect the bottleneck resource with a buffer** of work intended to absorb the variability in the arrival rate of new work queuing. You will get more work done despite the slightly longer lead time and the slightly greater total WIP.

#### Subordination actions

Something else will need to change in order to improve the exploitation of the bottleneck. **Changes required to improve performance in a bottleneck are usually not made at the bottleneck.**

### Non-instant availability resources

These look and feel like bottlenecks but they are not bottlenecks. They tend to become a problem with shared resources or people who are asked to perform a lot of multi-tasking.

When encountering non-instant availability problems, the ultimate is to turn them into an instantly available resources.

#### Subordination actions

Making policy changes across the value stream to maximise the exploitation of the bottleneck. Automation is usually the route to elevation. Hiring another engineer is not a good choice.

## An economic model for Lean

### Redefining "waste"

It is probably better to refer to "wasteful" activities as costs.

    COST
    ↑
    │
    │░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
    │░░░░░░░░░░░░░░░░COORDINATION COSTS░░░░░░░░░░░░░░░░
    │░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
    │▒▒▒▒▒▒▒▒▒▒▒▒▒                        ▒▒▒▒▒▒▒▒▒▒▒▒▒
    │▒▒▒▒▒▒▒▒▒▒▒▒▒    VALUE-ADDED         ▒▒▒▒▒▒▒▒▒▒▒▒▒
    │▒▒▒▒▒▒▒▒▒▒▒▒▒    WORK                ▒▒▒▒▒▒▒▒▒▒▒▒▒
    │▒▒▒▒▒▒▒▒▒▒▒▒▒                        ▒▒▒▒▒▒▒▒▒▒▒▒▒
    │▒TRANSACTION▒                    ████▒TRANSACTION▒
    │▒▒▒▒COSTS▒▒▒▒                ████████▒▒▒▒COSTS▒▒▒▒
    │▒▒▒▒▒▒▒▒▒▒▒▒▒            ████████████▒▒▒▒▒▒▒▒▒▒▒▒▒
    │▒▒▒▒▒▒▒▒▒▒▒▒▒        █████FAILURE████▒▒▒▒▒▒▒▒▒▒▒▒▒
    │▒▒▒▒▒▒▒▒▒▒▒▒▒    ████████████LOAD████▒▒▒▒▒▒▒▒▒▒▒▒▒
    │▒▒▒▒▒▒▒▒▒▒▒▒▒████████████████████████▒▒▒▒▒▒▒▒▒▒▒▒▒
    └────────────────────────────────────────────────────→ TIME

### Transaction costs

In economic terms, setup and cleanups activities are referred to as transaction costs. Every value-added activity has associated costs. Customer may not see, most likely does not value them. The customer may be forced to pay the costs of these activities but would prefer not to. Most project will have cleanup costs such us delivery to the customer.

Iterations, too, have transaction costs.

### Coordination costs

Coordination is necessary as soon as two or more people try to achieve a common goal together. These are any activities that involve communicating and scheduling.

Any form of meeting is a coordination activity.

If team members meet in order to create value-adding information, such as design, a test, a piece of analysis, a section of code, then that meeting is not a coordination cost, it is a value-added activity.

If team members meet in order to discuss status, or task assignment, or scheduling that helps coordination, that meeting is a coordination cost and should be regarded as wasteful. You should seek to reduce or eliminate coordination meetings.

Kanban provides coordination information that enables self-organisation and reduces coordination costs on a project. The more information can be made transparent to the knowledge workers on the team, the more self-organisation will be possible and the fewer coordination activities will be required.

### How do you know if an activity is a cost?

You can ask yourself, "if this activity is truly value-adding, would we do more of it?"

Planning is clearly not value-added. The customer would not pay for more planning if he could avoid doing so. Consider about minimising the time and energy spent or make the activity more effective.

What is important is that you have identified an activity as non-value adding, and that you want to reduce or eliminate that activity as part of a program of continuous improvement.

### Failure load

Demand generated by the customer that might have been avoided through higher quality delivered earlier. It adds value that should have been there already. Reducing failure load reduces opportunity cost of delay.

## Sources of variability

### Internal sources of variability

Kanban is a change-management technique that requires making alterations to an existing process.

### Work item size

One dimension of variability on itemising work for development is the size of work items. The average user story is 1.2 days of effort.

### Work item type mix

By breaking our work by specific type, it is possible to treat different types differently and to provide greater predicability. Extreme Programming created different definitions for different sizes of stories: Epic, Story and Grain of Sand.

By using techniques to identify different work item types, we can change the mean and spread of variability and improve the predictability in the system for any one type of work.

An additional strategy to improve predictability is to allocate total WIP capacity by specific types.

**Value predictability more than throughput. Predictability builds and holds trust**.

### Class-of-service mix

Allocate a WIP limit to each class of service. This will enable the mean and spread of variability for each class to settle down and the system will be predictable.

### Irregular flow

Every single item pulled through Kanban system will be different. Kanban copes with this as long as the WIP limits are enforced. It requires sustainable buffering to absorb the ebbs and surges in flow through the system. Additional buffers may be required, and WIP limits will beed to be larger, when there is more variability in the system. Increasing WIP limit to smooth flow will increase the mean lead time and reduce the range of lead-time variability.

Managers, owners, and usually customers value predictability over the random chance of a shorter lead time or greater throughput.

### Rework

Doing rework affects variability. The best strategy for reduction of variability due to defects is to relentlessly pursue high quality with very low defect counts.

### External sources of variability

They usually come from places that are not directly controlled by the software development process, like elements of the physical world that can't be easily anticipated, predicted, or controller, as suppliers or customers.

### Requirements ambiguity

Work items become blocked due to inability to make a decision. This can be addressed by directly influencing the analysis processes used to develop requirements, and by improving the capability and skill level of those defining them.

### Expedite requests

Expediting is known to be bad. It affects predictability of other requests. It increases mean lead time and the spread of variability and it reduces throughput. Expediting is undesirable even if it is being done to generate value.

One solution is to limit the number of expedite requests. By denying the business the ability to expedite anything they feel like, you force upstream people to explore opportunities early and asses them effectively.

### Irregular flow

There are two approaches to dealing with the blocked work items issue:
* You can have a larger overall WIP limit. It will ease the flow but at the expense of lead time and possibly quality. The biggest drawback is that there is less tension to provoke discussion and implementation of improvements.
* Leave work to be block, raising awareness of the blocking issue. Encouraging those idle team members to think about the root causes and possible process changes that will reduce or eliminate the possibility of recurrence.

### Environment availability

The idle time incurred by enforcing a WIP limit has been seen to encourage collaboration on resolving problems.

### Difficulty scheduling coordination activity

There is a challenge of coordinating external teams, stakeholders and resources. A frequent reaction is to schedule meetings with a regular cadence.

By marking items as blocked and raising visibility on to the source of the blockage, you'll lead some behavioural changes to improve the situation.

## Issue management and escalation policies

When an item becomes blocked, the convention is to attach a pink sticky note to the card, indicating the reason for the blockage or a red border in electronic systems.

Blocked work items require an organisation to develop a capability for issue management.

### Managing issues

Knowing something is blocked does not lead to developing a strong capability for getting it unblocked. It is essential to track the reason.

The daily standup meeting should focus on discussing blockages and progress toward the resolution of the issues. Issues should be tracked.

### Escalating issues

By taking the time to define escalation paths and write policy around it, the team knows where to send issues for resolution. This saves time.

### Tracking and reporting issues

A start date, and end date, an assigned team member, a description of the issue, and links to the blocked customer-valued items are the minimum requirements for an issue tracking system. A history of efforts made at resolution, a history of assigned individuals, an indication of escalation path, an estimated time to resolution, an impact assessment, and suggested root-cause fixes for future prevention may also be useful fields to track.
