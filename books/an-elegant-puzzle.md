# [An Elegant Puzzle: Systems of Engineering Management](https://www.goodreads.com/book/show/45303387-an-elegant-puzzle)

- [Introduction](#introduction)
- [Organisations](#organisations)
  - [Sizing teams](#sizing-teams)
  - [Staying on the path to high-performing teams](#staying-on-the-path-to-high-performing-teams)
  - [A case against top-down global optimisation](#a-case-against-top-down-global-optimisation)
  - [Productivity in the age of hypergrowth](#productivity-in-the-age-of-hypergrowth)
  - [Where to stash your organisation risk?](#where-to-stash-your-organisation-risk)
  - [Succession planning](#succession-planning)
- [Tools](#tools)
  - [Introduction to systems thinking](#introduction-to-systems-thinking)
  - [Product management: exploration, selection, validation](#product-management-exploration-selection-validation)
  - [Vision and strategies](#vision-and-strategies)
  - [Metrics and baselines](#metrics-and-baselines)
  - [Guiding broad organisational change with metrics](#guiding-broad-organisational-change-with-metrics)
  - [Migrations: the sole scalable fix to tech debt](#migrations-the-sole-scalable-fix-to-tech-debt)
  - [Running an engineering reorg](#running-an-engineering-reorg)
  - [Identify your controls](#identify-your-controls)
  - [Career narratives](#career-narratives)
  - [Model, document and share](#model-document-and-share)
  - [Scaling consistency: designing centralised decision-making groups](#scaling-consistency-designing-centralised-decision-making-groups)
  - [Presenting to senior leadership](#presenting-to-senior-leadership)
  - [Time management](#time-management)
  - [Communities of learning](#communities-of-learning)
- [Approaches](#approaches)
  - [Work the policy not the exceptions](#work-the-policy-not-the-exceptions)
  - [Saying no](#saying-no)
  - [Your philosophy of management](#your-philosophy-of-management)
  - [Managing in the growth plates](#managing-in-the-growth-plates)
  - [Ways engineering managers get stuck](#ways-engineering-managers-get-stuck)
  - [Partnering with your manager](#partnering-with-your-manager)
  - [Finding managerial scope](#finding-managerial-scope)
  - [Setting organisation direction](#setting-organisation-direction)
  - [Close out, solve, or delegate](#close-out-solve-or-delegate)
- [Culture](#culture)
  - [Opportunity and membership](#opportunity-and-membership)
  - [Select project leads](#select-project-leads)
  - [Make your peers your first team](#make-your-peers-your-first-team)
  - [Consider the team you have for senior positions](#consider-the-team-you-have-for-senior-positions)
  - [Company culture and managing freedoms](#company-culture-and-managing-freedoms)
  - [Kill your heroes, stop doing it harder](#kill-your-heroes-stop-doing-it-harder)
- [Careers](#careers)
  - [Roles over rocket ships, and why hypergrowth is weak predictor of personal growth](#roles-over-rocket-ships-and-why-hypergrowth-is-weak-predictor-of-personal-growth)
  - [Running a humane interview process](#running-a-humane-interview-process)
  - [Cold sourcing: hire someone you don't know](#cold-sourcing-hire-someone-you-dont-know)
  - [Hiring funnel](#hiring-funnel)
  - [Performance management systems](#performance-management-systems)
  - [Career levels, designation momentum, level splits, etc.](#career-levels-designation-momentum-level-splits-etc)
  - [Creating specialised roles, like SRE or TPMs](#creating-specialised-roles-like-sre-or-tpms)
  - [Designing an interview loop](#designing-an-interview-loop)
- [Appendix](#appendix)
  - [Tools for operating a growing organisation](#tools-for-operating-a-growing-organisation)
  - [Useful books](#useful-books)
  - [Useful papers](#useful-papers)

## Introduction

Organisational design gets the right people in the right places, empowers them to make decisions, and then holds them accountable for their results.

## Organisations

An organisation is a collection of people working toward a shared goal.

Organisational design is the attempt ot understand why some create such energy and others create mostly heat: friction, frustration, and politics.

### Sizing teams

The fundamental challenge of organisational design is sizing teams.

**Managers should support six to eight engineers.** This gives them enough time for active coaching, coordinating, and furthering their team's mission by writing strategies, leading change and so on.
  * Fewer than four engineers tend to function as **Tech Lead Managers**, taking on a share of design and implementation work.
  * Managers supporting more than eight or nine engineers act as **coaches** and safety nets for problems.

**Managers-of-managers should support four to six managers.** This gives them enough time to coach, align with stakeholders, and to do a reasonable amount of investment in their organisation.
  * Managers supporting fewer than four other managers should be in a period of active learning.
  * Supporting a large team of managers leaves you functioning purely as a problem-solving coach.

**On-call rotations want eight engineers.** It is sometimes necessary to pool multiple teams together to reach the eight engineers necessary for a 24/7 on-call rotation.

**Small teams (< 4 members) are not teams.** Fewer than four individuals are sufficiently leaky abstraction that they function indistinguishably from individuals.  A few tips:
* Teams should be six to eight during steady state.
* To create a new team, grow an existing team to eight to ten, and then bud into two teams of four or five.
* Never create empty teams.
* Never leave managers supporting more than eight individuals.

### Staying on the path to high-performing teams

Four stages of a team

* **A team is falling behind** if each week their backlog is longer than it was the week before. To fix this, hire new people and increase capacity.
* **A team is treading water** if they're able to get their critical work done, but are not able to paying down technical debt or begin major new projects. To fix this, consolidate team efforts to finish more things, and reduce concurrent work until able to begin repaying debt.
* **A team is repaying debt** when they're able to start paying down tech debt, and are beginning to benefit from the debt repayment snowball. To fix this, add time to pay debt.
* **A team is innovating** when their technical debt is sustainably low, morale is high, and the majority of work is satisfying new user needs. To fix this maintain enough slack in your team's schedule so that the team can build quality into their work.

For each constraint, prioritise one team at a time, this is particularly important for hiring.

Adding new individuals to a team disrupt the team. It is much easier to have rapid growth periods for any given team, followed by consolidation/gelling periods.

### A case against top-down global optimisation

#### Team first

Sustained productivity comes from high-performing teams, be hesitant to disassemble them.

A proposed model is to rapidly hiring into teams loaded down by technical debt, not into innovating teams, which avoids incurring re-gelling costs on high-performing teams.


#### Fixed costs

Moving one person can shift an innovating team back into falling behind.

#### Slack

Don't add more resources to a team with visible slack, inverse does not apply.

In defence of having slack, teams put spare capacity to great use by improving areas within their aegis, in bot incremental and novel ways.

#### Shift scope; rotate

It's more fruitful to move scope between teams. If a team has significant slack, then incrementally move responsibility to them.

Another approach is to rotate individuals for a fixed period into an area that needs help.

### Productivity in the age of hypergrowth

#### More engineers, more problems

Integrating large numbers of engineers is hard. The challenge depends on how quickly you can ramp engineers up ot self-sufficient productivity. You can quickly find a scenario in which untrained engineers increasingly outnumber the trained ones.

It is not just training and hiring tho:
1. For every additional order of magnitude of engineers, you need to design and maintain a new layer of management.
2. For every ~10 engineers, you need an additional team and more coordination.
3. You'll need to improve your development tools
4. More deployments drive more outages.
5. Relative time invested in on-call goes up.

At high enough rates, the marginal added value of hiring gets very slow, especially if your training process is weak.

#### Systems survive one magnitude of growth

If your company is designing systems to last one order of magnitude and doubling every six months, then you'll have to re-implement every system twice every three years.

The real productivity killer is not the system rewrites, but the migrations that follow up those rewrites.

#### Ways to manage entropy

You only get value from projects when they finish. When your company has decided that is going to grow you cannot stop it from growing. However, you absolutely can concentrate that growth, such that your teams alternate between periods of rapid hiring and periods of consolidation and gelling.

Companies do major investments in both new-hire bootcamps and recurring educational classes.

If you could get training down to four weeks, imagine how quickly you could hire without overwhelming the existing team!

Create a rotation for people who are available to answer questions, and train your team not to answer other forms of interruptions. It may be useful to define an _ownership registry_ and document who owns what.

The best solution to frequent interruptions is a culture of documentation, optimised for reading and searching.

The most important opportunity is designing your software to be flexible. If you are going to rewrite your systems every few years due to increased scale, let's avoid any unnecessary rewrites.

An anti-pattern is the gatekeeper pattern. Having people who perform gatekeeping activities create very odd social dynamics, build systems with sufficient isolation so when they occasionally fail, make sure that they fail with a limited blast radius.

---

As a closing though, the way you handle urgent project requests when you're already underwater is by learning to say no.

### Where to stash your organisation risk?

The idea of _organisational debt_ is sibling of _technical debt_, for example a toxic culture, struggling leader, etc.

These problems bubble up from your peers, skip-level one-on-ones, and organisational health surveys.

Identify a few areas to improve, ensure you're making progress on those, and give yourself permission to do the rest poorly.

It's best to only delegate solvable risk. If something isn't likely to end well, hold the bag yourself, you're almost certainly the best positioned to take responsibility.

### Succession planning

Succession planning is thinking through how the organisation would function without you.

First, figure out what you do:
* Look at your calendar and write down **your role in meetings**.
* Take a pass on you calendar for non-meeting stuff.
* Look out for **recurring processes**, like roadmap, planning, performance calibrations, etc. and document your role in each of those processes.
* For each of the **individuals you support**, in which areas are your skills and actions most complementary to theirs?
* Audit inbound chats and emails for requests and questions coming your way.
* Look at the categories of the work you've completed over the past six months.
* Think on the **external relationships** that have been important for your current role.

For each item try to identify individuals who could readily take on that work. If you cannot find someone, identify a handful of individuals who could potentially take over.

Filter the gaps down to two lists:
1. _Easiest gaps to close_, It may require a written document or quick introduction.
2. _Riskiest gaps_, areas where you're uniquely valuable to the company.

Write up a plan to close all of the easy gaps and _onw or two_ the riskiest gaps. This is a great exercise to run once a year to identify things you could be delegating.

## Tools

The key tools for leading efficient change are systems thinking, metrics and vision/

### Introduction to systems thinking

You should read about [_Thinking in Systems: a Primer_](https://www.goodreads.com/book/show/3828902-thinking-in-systems) by Donella H. Meadows.

Systems thinking makes the observation that links between events are often more subtle than they appear.

#### Developer velocity

Recommended reading [_Accelerate: The Science of Lean Software and DevOps_](https://www.goodreads.com/book/show/39211555-accelerate) by Nicole Forsgren, Gene Kim, and Jez Humble.

To measure developer velocity:
* **Delivery lead time**, time from the creation of code to its use in production
* **Deployment frequency**
* **Change fail rate**, how frequent changes fail
* **Time to restore service**, time spent recovering from defects

Any difficult problem is worth trying to represent as a system. There are a few tools that can help you out: Stella and Insight Maker.

### Product management: exploration, selection, validation

Many engineering organisations separate engineering and product leadership into distinct roles. This is ideal because they thrive in different perspectives and priorities.

As an engineering leader, you may have to cover both roles temporarily.

Product management is an iterative elimination tournament.
1. **Problem discovery.** Exploring the different problems that you could pick to solve. You populate the problem space based on:
    * **Users' pain**, problems that your users experience
    * **Users' purpose**, what motivates your users to engage with your systems
    * **Benchmark**, how your company compares to competitors. Areas in which you are weak, _consider_ investing in
    * **Cohorts**, what is hiding behind your clean distributions
    * **Competitive advantages**, areas where you're exceptionally strong
    * **Competitive moats**, extreme version of a competitive advantage. Allows you to pursue offerings that others simply cannot
    * **Compounding leverage**, blocks you could start building today that would compound into major product or technical leverage over time.
2. **Problem selection**, narrow down to a specific problem portfolio
    * **Surviving round**, what do you need to survive current round
    * **Surviving the next round**, where do you need to be when the next round in order to avoid getting eliminated?
    * **Winning rounds**
    * **Consider different time frames.** Assumptions about the correct time frame to optimise for
    * **Industry trends**, where do you think the industry is moving
    * **Return on investment**, try ordering problems by expected return on investment
    * **Experiments to learn**
3. **Solution validation**, it's easy to jump directly into execution, but it's well worth to have an explicit solution validation phase.
    * **Write a customer letter**, useful to test against actual users
    * **Identify prior art**, it's better to rely on people you have some connection to instead of on conference talks, there is lot of misinformation out there.
    * **Find reference users**
    * **Prefer experimentation over analysis**, get good at cheap validation
    * **Find the path more quickly travelled**, try to find the cheapest way to validate
    * **Justify switching costs**, the cost of switching for users to move to your solution

### Vision and strategies

When jumping from supporting managers and supporting their managers alignment may be difficult to handle. Agreeing on strategy and vision is the most effective approach for alignment at scale.

_Strategies_ are grounded documents which explain trade-offs and actions that will be taken to address as specific challenge.

_Visions_ are aspirational documents that enable individuals who don't work closely together to make decisions that fit together cleanly.

#### Strategy

Specific actions that address a given challenge's constraints. Recommended reading [_Good strategy / Bad Strategy: The difference and why it matters_](https://www.goodreads.com/book/show/11721966-good-strategy-bad-strategy) by Richard Rumelt.

The _diagnosis_ is a theory describing the challenge at hand. Before you've even finished reading a great diagnosis, you'll often have identified several good candidate approaches.

The second step is to identify _policies_ that you will apply to address the challenge. Describe the general approach that you'll take, and are often trade-offs between two competing goals.

When you apply your guiding policies to your diagnosis, you get your _actions_. This is the easiest part to write, however publishing it and following through with it can be significant test of your commitment.

Because strategies are specific to a given problem, it's okay to write a few of them. The act of writing a strategy leads folks through a systematic analysis.

#### Vision

If strategies describe the harsh trade-offs necessary to overcome a particular challenge, then _visions_ describe a future in which those trade-offs are no longer mutually exclusive. **An effective vision helps folks think beyond the constraints of their local maxima**, and lightly aligns progress without requiring tight centralised coordination.

Visions should be detailed, but the details are used to illustrate the dream vividly, not prescriptively constraint with its possibilities. Good visions are composed of:
* **Vision statement**, a one or two sentence aspirational statement to summarise the rest of the document.
* **Value proposition**, how will you be valuable to your users and your company?
* **Capabilities**, what capabilities will the product, platform, or team need in order to deliver on your value proposition?
* **Solved constraints**, constraints that you're limited by today, but that in future you'll no longer be constrained by?
* **Future constraints**, constraints that you expect to encounter in this wonderful future?
* **Reference materials**, link to all resources for those who want to understand more of the thinking that went into the vision.
* **Narrative**, synthesise all those details into a short, maybe one page, narrative that serves as an easy-to-digest summary.

**A vision is succeeding when people reference the document to make their own decisions.**

Some additional tips:
* **Test the document** sit down with a few different folks to get their perspectives and iterate.
* **Refresh periodically**
* **Write simply** You'll likely want _one vision for every complete distinct area, but no more_.

### Metrics and baselines

Goals decouple the "what" from the "how"

Goals are a composition of
1. A **target** states where you want to reach
2. A **baseline** identifies where you are today
3. A **trend** describes the current velocity
4. A **time frame** sets bounds for the change

Two interesting kinds of goals: investments and baselines. Investments describe a future state that you want to reach, and baselines describe aspects of the present that you want to preserve.

The best way to avoid unintended outcomes is to pair your investments goals with baseline metrics (countervailing metrics). 

The most common way to use goals is during s planning process. You'll probably want to identify more baseline goals than investment goals.

OKRs are useful, lightweight structure to start from.

### Guiding broad organisational change with metrics

Metrics are an extremely effective way to lead change with little or no organisational authority.

1. **Explore**: The first step is to get data in an explorable format in your data warehouse.
2. **Dive**: Go deep on understanding the levers.
3. **Attribute**: Diving will uncover one team who are nominally accountable for the metric's performance.
4. **Contextualise**: Start to build context around each team's performance by doing benchmarking against a small handful of cohorts like backend, frontend or infrastructure.
5. **Nudge**: Nudge them for action! Send push notifications, typically email, to teams whose metric has changed recently, both in terms of absolute change and in terms of their benchmarked performance against their cohort. Recommended read [Nudge](https://www.goodreads.com/book/show/2527900.Nudge).
6. **Baseline** some cases contextualised nudges are not enough, you may need to agree on the baseline metrics for performance.
7. **Review** hopefully you won't need to reach, is running a monthly or quarterly review that looks each team's performance.

### Migrations: the sole scalable fix to tech debt

Migrations matter because they are usually the only available avenue to make meaningful progress on technical debt.

Each migration aims to create technical leverage. Moving from VMs to containers, rolling out circuit-breaking, moving to the new build tool… If you don't get effective at software and system migrations, you'll end up languishing in technical debt.

#### De-risk

Write a **design document** and shop it with the teams that you believe will have the hardest time migrating. Test it against the next six to twelve months of the roadmap and iterate.

**Embed into the most challenging one or two teams**, and work side by side with them to build, evolve, and migrate to the new system.

**Each team who endorses a migration is making a bet on you**.

#### Enable

It's better to slow down and build tooling to programmatically migrate the easy 90 percent, it reduces the cost radically.

Figure out the **self-service tooling and documentation** that youc an provide to allow teams to make the necessary changes without getting stuck. The best migration tools are incremental and reversible.

Documentation and self-service tooling are products, and they thrive under the same regime.

#### Finish

The last phase of a migration is deprecating the legacy system that you've replaced. It requires 100 percent adoption.

Start by **stopping the bleeding**, which is ensuring that all newly written code uses the new approach.

Start **generating tracking tickets**, and set in place a mechanism which **pushes migration status** to teams.

**Finish it yourself**.

It is important to celebrate migrations, **recognition should be reserved for their successful completion**.

### Running an engineering reorg

There are two managerial skills that have a disproportionate impact in your organisation success: making technical migrations cheap, and running clean reorganisations.

Checklist to ensure a reorganisation is appropriate:
1. Is there a structural problem? With a reorg you can increase communication, reduce decision friction, and focus attention
2. Are you reorganising around a broken relationship? You'll be better of addressing the underlying issue.
3. Does the problem already exist? It's better to wait until a problem actively exists before solving it.
4. Are the conditions temporary? It may be easier to patch through and rethink on the other side.

#### Project head count a year out

You can design an organisation determining it approximate total size:
1. An optimistic number based on what's barely possible
2. A number based on the "natural size", if every team and role was fully staffed
3. A realistic number based on historical hiring rates.

Merge those into a single number.

#### Manager-to-engineer ratio

Now you need to identify how many individuals you want each manager to support. **If engineering managers are expected to do hands-on technical work, it should be 3 to 5 engineers.**

**Otherwise, 5 to 8 depending on the experience level.**

#### Defining teams and groups

Example: 35 engineers, 7 engineers per manager = you need 5 managers, and 1.8 managers of managers. This is 5 to 6 teams, and maybe one to three groups.

You should generally round up the number of managers.

Few extra considerations:
1. Can you write a crisp mission statement for each team?
2. Would you personally be excited to be a member of each of the teams, as well as the manager of each of those teams?
3. Put teams that work together, as close together as possible.
4. Can you define clear interfaces for each team?
5. Can you list the areas of ownership for each team?
6. Avoid implicitly creating holes of ownership, define understaffed teams.
7. Are you over-optimising on individuals versus establishing a sensible structure?

#### Staffing the teams and groups

Four sources of candidates to staff them:
1. Team members who are ready to fill the roles now
2. Team members who can grow into the roles in the time frame
3. Internal transfers from within your company
4. External hires who already have the skills

#### Commit to moving forward

1. Are the changes meaningful net positive?
2. Will the new structure last at least six months?
3. What problems did you discover during design?
4. What will trigger the reorg _after_ this one?
5. Who is going to be impacted most?

**Organisational change is resistant to rollback, you have to be collectively committed to moving forward with it, even if runs into challenges along the way.**

#### Roll out the change

Key elements to a good rollout:
1. Explanation of reasoning driving the reorganisation
2. Documentation of how each person and team will be impacted
3. Availability and empathy to help bleed off frustration from impacted individuals

Tactics for doing this:
1. Discuss with impacted individuals first
2. Ensure that managers are prepared to explain the reasoning behind the changes
3. Send an email out documenting the changes
4. Be available for discussion
5. If necessary, hold an all-hands by try not to (people don't process well in large groups)
6. Double down on doing skip-level one-on-ones

### Identify your controls

When you partner with managers it may be difficult to remain effective without understanding their day-to-day tasks.

Controls are the mechanisms that you use to align with other leaders you work with.

**Metrics** align on outcomes while leaving flexibility around how the outcomes are achieved.

**Visions** ensure that you agree on long-term direction.

**Strategies** confirm you have a shared understanding of the current constraints.

**Organisation design** allows you to coordinate the evolution of a wider organisation.

**Head count and transfers** are the ultimate form of prioritisation.

**Roadmaps** align on problem selection and solution validation.

**Performance reviews** coordinate culture and recognition.

Start with this list but don't stick to it!

You will need to agree on the _degree of alignment_ for each one.

**I'll do it**. Stuff that you'll personally be responsible for doing.

**Preview**. You'd like to be involved early and often.

**Review**. You'd like to weigh in before it gets published.

**Notes**. Projects you'd like to follow but don't have much to add to.

**No surprises**. The work that we're currently aligned on but requires updates to keep your mental model in tact.

**Let me know**. If something comes up that you can help with, but otherwise you are totally confident it'll go well.

### Career narratives

You as a manager, can simply give folks a career path.

#### Artificial competition

Climbing the career ladder has the side effect of funneling most folks toward a constrained pool of opportunity.

An important part of setting your goals is developing areas you're less experienced in to maximise your global success, but it's equally important to succeed locally within your current environment by prioritising doing what you do well.

#### Translating goals

Once you've identified goals to pursue, the next step is to translate those goals into actions, your manager can be a leveraged partner finding the intersection of your interests and the business priorities.

Bringing your list of goals to this discussion helps ensure that it's successful.

#### The briefest of media trainings

Three rules for speaking with the media:
1. **Answer the question you want to be asked**. Reframe it into one that you're comfortable answering. [Don't Think of an Elephant!](https://www.goodreads.com/book/show/13455.Don_t_Think_of_an_Elephant_Know_Your_Values_and_Frame_the_Debate) is an excellent book on framing issues.
2. **Stay positive**, find a positiver framing and stick to it.
3. **Speak in threes**. Narrow your message in three concise points.

### Model, document and share

**Model**. Start measuring your team's health (maybe using short, monthly surveys) and your team's throughput (do some lightweight form of task sizing), baseline before your change.

Then just start running Kanban. Don't publicise it, don't make a big deal about it, just start doing it. Frame it as a short experiment.

**Document**. Document the problem you set out to solve, the learning process, and the details of how another team would adopt the practice.

**Share**. The final step is to share your documented approach, don't lobby for change, just present the approach and your experience following it. This has often lead to more adoption than top-down mandates have.

##### Where it works

Compare it with the top-down mandate. Mandates assume:
* **It's better to adopt a good-enough approach quickly**
  * Teams have the bandwidth to adopt a new approach
  * The organisation has available resources to coordinate a rollout
  * You want to centralise decision-making
  * Consistency is important
  * It's important to make this change quickly
* **Model, document, share assumes**
  * Some teams don't have the bandwidth to adopt a new approach
  * The organisation may not have resources to coordinate a rollout
  * You want to decentralise decision-making
  * Teams have agency to adopt practices for themselves
  * It's okay to approach change gradually

  You'll still need some natural authority and the respect of your peers.

  Do not try to use this as a strategy to circumvent organisational authority, it does not end well.

### Scaling consistency: designing centralised decision-making groups

As organisations grow, there is a subtle slide into inconsistency. When the problem becomes acute, people tend to reach for a centralised, accountable group.

The two most common flavours are "product reviews" to standardise product decisions and "architecture group" to encourage consistent technical design.

Some of these groups take on an authoritative bent, becoming rigid gatekeepers, and others become more advisory, with a focus on educating folks toward consistency.

#### Positive and negative freedoms

Folks will feel a significant loss of freedom when you create these groups. Many others will find the creation of centralised groups extremely empowering, some people are comfortable with self-authorisation and some others have a higher threshold for self-authorisation.

A _positive freedom_ is the freedom to do something, for example the freedom to pick a programming language you prefer. A _negative freedom_ is the freedom from things happening to you, like freedom not to be obligated to support additional programming languages.

**Particularly in cases where ownership is extremely diffuse, cautiously authoritative groups do increase net positive freedom for individuals without greatly reducing negative freedom.**

#### Group design

**Influence.** How do you expect this group to influence results? In an authoritative way? Natural authority of its members? Advocacy?
**Interface.** How will other teams interact with this team? Tickets, emails, weekly review session?
**Size.** How large the group be? If it's six or fewer it's possible for them to gel into a true team. More than ten will find hard to have a good discussion, it'll need to be structured into sub-groups.
**Time commitment.** How much time will members spend working in this group?
**Identity.** Should members view their role in the group as their primary identity?
**Selection process.** How will you select members? Structured selection in which you identify requirements and folks apply?
**Length of term.** How long will members serve? Best default is fixed terms, while allowing current individuals to remain eligible, and without enacting term limits.

#### Failure modes

There are a few ways these groups consistently fail:
* **Domineering** groups significantly reduce individuals negative and positive freedoms, those making decisions are abstracted from the consequences of the decisions.
* **Bottlenecked** groups tend to be very helpful, but are trying to do more than they're actually able to do.
* **Status-oriented** groups place more emphasis on being a member of the group than on the group's nominal purpose.
* **Inert** groups don't do much of anything.

### Presenting to senior leadership

Some tips to prepare your presentation:
* Communication is company-specific.
* Start with the conclusion. Starting with what's important, instead of building toward it gradually.
* Frame why the topic matters. Start by explaining why your work matters to the company.
* Everyone loves a narrative.
* Prepare for detours. Be ready for the discussion to derail toward a thread of unexpected questions.
* Answer directly. Instead of hiding problems, use them as an opportunity to explain your plans to address them.
* Deep in the data. Spend time exploring the data.
* Derive actions from principles. Provide a mental model of how you view the topic, and make folks familiar on how you make decisions.
* Discuss the details.
* Prepare a lot; practice a little. Leadership presentation tend to quickly detour, so practice isn't quite as useful. Prepare instead getting deeper into the data, details and principles.
* Make a clear ask. Start the meeting by explicitly framing your goal.

Approach to presenting to senior leaders is:
1. Tie topic to business value.
2. Establish historical narrative.
3. Explicit ask.
4. Data-driven diagnosis.
5. Decision-making principles.
6. What's next and when it'll be done.
7. Return to explicit ask.

### Time management

Time management is the enduring meta-problem of leadership. The most impactful change you can do to manage time are:
* **Quarterly time retrospective.** Categorising your calendar from the past three months to figure out how you've invested your time.
* **Prioritise long-term success over short-term quality.** You have to prioritise long-term success, eve if it's personally unrewarding to do so in the short term.
* **Finish small, leveraged things.** Each thing you finish should create more bandwidth to do more future work.
* **Stop doing things.** Alert your team and management chain that you won't be doing it.
* **Size backward, not forward.** Specify the number of hours you're able to dedicate to the activity (like skip-level meetings), perhaps two per week, and perform as many as possible within that amount of time.
* **Delegate working "in the system".** Design a path that will enable someone else to take on that work.
* **Trust the system you build.**
* **Decouple participation from productivity.** Don't fall into the trap of assuming that attendance is valuable.
* **Hire until you are slightly ahead of growth.** Hire before you get overwhelmed.
* **Calendar blocking.** Add three or four two-hour blocks scattered across your week to support more focused work.
* **Getting administrative support.** Once you've exhausted all the above tools and approaches, having someone else handling the dozens of little interruptions is a remarkable improvement.

You can get less busy by prioritising finishing things with the goal of reducing load. **Don't fall into the trap of believing that being busy is being productive.**

### Communities of learning

Recommended approach:
1. **Be a facilitator, not a lecturer.** Folks want to learn from each other more than they want to learn for a single presenter.
2. **Brief presentations, long discussions.** Present a few minutes of content, maybe five, and then move into discussion.
3. **Small breakout groups.** Allow folks to learn in small and safe places. It also gives everyone an opportunity to be part of the discussion.
4. **Brining learning to the full group** Give each group an opportunity to bring their discussions back to the larger group.
5. **Chose topics that people already know about.** Successful topics are ones that people have already thought about.
6. **Encourage tenured folks to attend.** You'll find that the most senior or most tenured folks opt out to focus on other work.
7. **Optional pre-reads.** Providing a list of optional pre-reads can help them prepare for the discussion.
8. **Checking in.** Have each person give a 20 or 30-second self-introduction. Your name, team and one sentence about what's on your mind.

## Approaches

### Work the policy not the exceptions

Exceptions undermine one of the most powerful mechanisms for alignment: consistency.

Insisting on its established routines is a company pacing a path whose grooves leads to failure. How do you reconcile consistency and change?

#### Good policy is opinionated

Every policy you write is a small strategy, identifying your goals and the constraints that bring actions into alignment with those goals.

**Don't recommend writing policies that do little to constraint behaviour.** In such cases, recommend writing norms, which provide non-binding recommendations.

#### Exception debt

Once you've supported your goals through constraints, all you have to do is consistently uphold your constraints.

Applying policy consistently is challenging:
1. Accepting reduced opportunity space. Good constraints make trade-offs that deliberately narrow your opportunity space.
2. Locally suboptimal. Global constraints inevitably leads to local inefficiency.

We need the courage to accept these local inefficiencies.

Granting exceptions undermines people's sense of fairness, and sets a precedent that undermines future policy.

#### Work the policy

You have to avoid undermining your work, and yourself, with exceptions.

Once you've collected enough escalations, revisit the constraints. Move you from working the exceptions to working the policy.

### Saying no

No is explaining your team's constraints to folks outside the team.

#### Constraints

Two topics are frequent venues of disagreement: Velocity and Prioritisation.

#### Velocity

Your goal is to provide a compelling explanation of how your team finishes work. _Finishes_ as opposed to _does_.

**The most effective approach for explaining your team's delivery process is to build a Kanban board.**

You want to focus your team on the single inefficient component that's slowing down your throughput of finished work. Next step is explaining what's preventing you from solving it (technical debt).

You'll have to translate the problem into something resembling data, if you estimate this can be easy as explaining how you decide the number of story points. If you don't, check what your team is working on at a few random moments across the day, and use that as an approximation.

You can shift time from other behaviours toward your constraints. The next stage is to add capacity. You can add more capacity by  moving existing resources to the team, or to create new resources (via hiring).

#### Priorities

Document all your incoming asks, develop guiding principles for how work is selected, and then share subsets of tasks you;ve selected based on those guiding principles.

#### Relationships

If your perspective still isn't resonating after explaining both your velocity and priorities, you have a relationship problem to address.

### Your philosophy of management

When you start managing, your philosophy could be quite simple:
1. The Golden Rule, treating others as you want to be treated, makes a lot of sense.
2. Give everyone an explicitly area of _ownership_ that they are responsible for.
3. Reward and status should derive from _finishing_ high-quality work.
4. _Lead from the front_, and never ask anyone to do something you wouldn't.

Remember that that you leave a broad wake and that your actions have a profound impact on those around you.

**Almost every internal problem can be traced back to a missing or poor relationship.**

"With the right people, any process works, and with the wrong people, no process works."

Instead of avoiding the hardest parts, double down on them.

Aas a leader, you can't run from problems; engage them head-on.

**Do the right thing for the company, the right thing for the team, and the right thing for yourself, in that order.**

Be honest about which of your practices are truly best practices and which you're following on autopilot. You can't fix everything at one, you'll often be doing something mediocre, remember to come back and improve it when you can.

### Managing in the growth plates

**You can't expect to succeed by iterating on the status quo.** Execution is the primary currency in the growth plates.

#### In the growth plates

What folks in the growth plates need is help reducing and executing backlog of ideas, not adding more. Giving more ideas feels helpful, but isn't. In the growth plates, you are focused on surviving to the next round.

#### Outside the growth plates

You are mostly working on problems with known solutions. Often, we make solid executors responsible for slower-growth areas, we need the innovators int he highest-growth ones, but the opposite tends to work better.

#### Aligning values

If you are working in the growth plates, or outside them, for the first time, treat it like a brand-new role.

### Ways engineering managers get stuck

Newer managers get stuck when:
1. **Only manage down.** Building something your team wants to build, but which the company and your customers aren't interested in.
2. **Only manage up.** Focus so much on following their management's wishes.
3. **Never manage up.** Excellent work go unnoticed because it was never shared upward.
4. **Optimise locally.** Picking technologies that the company can't support, or building a product that puts you in competition with another team.
5. **Assume that hiring never solves any problems.** Spend all time firefighting and neglect hiring.
6. **Don't spend time building relationships.** Your team impact depends largely on doing something other teams or customers want, and getting it shipped out the door. This is extraordinarily hard without a supportive social network within the company.
7. **Define their role to narrowly.** Effective managers tend to become the glue in their team, filling any gaps. That means sometimes doing things you don't really want to do in order to set a good example.
8. **Forget that their manager is a human being.** You have to give them room to make mistakes.

More experienced managers get stuck when:
1. **Do what worked at their previous company.** Pause to listen and foster awareness before you start "fixing" everything.
2. **Spend too much time building relationships.** Particularly common in managers coming from larger companies. Smaller companies expect more execution focus than relationship management focus.
3. **Assume that more hiring can solve every problem.** Adding too many people can dilute your culture.
4. **Abscond rather than delegate.** Delegation it's easy to goo too far and ignore critical responsibilities to discover a disaster later on.
5. **Become disconnected from ground truth.** Make decisions fundamentally disconnected from reality.

All managers tend to get stuck when:
1. **Mistake team size for impact.** A larger team is not better job, it's a _different_ job. It won't make you important or make you happier.
2. **Mistake title for impact.** Titles are arbitrary social constructs. Don't let them become your goal.
3. **Confuse authority with truth.** Authority it's a pretty expensive way to work with people, they'll eventually turn off their minds and simply follow orders.
4. **Don't trust the team enough to delegate.**
5. **Let other people manage their time.** Prioritise your time on important things.
6. **Only see the problems.** Forget to celebrate the good stuff.

### Partnering with your manager

To partner successfully with your manager:
1. You need to know a few things about you.
2. You need to know a few things about them.
3. You should occasionally update the things you know about each other.

Things your manager should know about you:
* What problems you're trying to solve. How you're trying to solve each of them.
* That you're making progress (you're not stuck).
* What you prefer to work on (staff you properly).
* How busy you are (if you can take an opportunity if comes up).
* What your professional goals and growth areas are. Where you are between bored and challenged.
* How you believe you're being measured (KPIs, etc.).

To keep your manager informed:
1. Maintain a document with this information, which you keep updated.
2. Sprinkle this information into your one-on-ones, focusing on information gaps.
3. At some regular point, maybe quarterly, write up a self-reflection that covers each of those aspects.

Another key aspect of managing up, is to know some things about your manager and their needs.
* What are their current priorities? Particularly, what are their problems and key initiatives.
* How stressed are they?
* Is there anything you can do to help?
* What is their management's priority for them?
* What are they trying to improve on themselves, and what are their goals? This is particularly valuable to know if they appear stuck, because you may be able to help unstuck them.

### Finding managerial scope

There are three types of engineering management jobs:
1. Manager: you manage a team directly.
2. Director: you manage a team of managers.
3. VP: you manage an organisation.

We should really be pursuing scope: not enumerating people but taking responsibility for the success of increasingly important and complex facts of the organisation and company.

You can always find an opportunity to increase your scope and learning, even in a company that doesn't have room for more directors or vice presidents. **You can grow scope through broad, complex projects.**

If you've been focused on growing the size of your team as the gateway to career growth, call bullshit on all that, and look for a gap in your organisation that you can try to fill.

### Setting organisation direction

#### Scarce feedback, vague direction

On your early career, you'll have folks who are routinely giving feedback on your work. As your span responsibility grows, increasingly no one will feel responsible or able to provide that feedback.

You'll be expected to set your own direction with little direction from others.

If you don't supply direction, you'll start to feel the pull of irrelevance.

This is a symptom of success, you'll ave to learn how to set your organisation's direction and your own.

#### Mining for direction

The first phase is discovery without judgement. Take ideas from everywhere and generate a pile of ideas that folks are pursuing, even if you think they're terrible.

Once your pile of ideas has gotten large enough, craft it into a strategy, and then start testing that strategy. Identify the key pivots in your strategy.

Make a clear decision on each of those pivots, write a document explaining those decisions.

Return to your rounds of engaging with experienced leaders at other companies.

The final step is to distil the document into something comprehensible without hours of close reading.

### Close out, solve, or delegate

Your ability to put your head down and solve gritty, important problems was probably a big part of how you were promoted. Now it's the wrong answer to most of your problems. It's too inefficient to accomplish the breadth and quantity of things you need to get done. 

If your instincts are driving you into a pile of work you can't make a dent in, you must pick one of three options:
* **Close out.** In a way that this specific ask is entirely resolved. Making a decision and communicating it to all involved participants.
* **Solve.** Design a solution that you won't need to spend time on this particular kind of ask again in the next six months.
* **Delegate.** Redirect the ask to someone who is responsible for that kind of work.

## Culture

### Opportunity and membership

An inclusive organisation is one in which individuals have access to opportunity and membership.

#### Opportunity

Ensuring that folks can go home most days feeling fulfilled by challenge and growth.

**The most effective way to provide opportunity is through the structured application of good process.** Structure allows folks to learn how these process work, build trust by watching the consistent, repeated application of those process.

Ways to create and distribute opportunity:
1. **Rubrics everywhere.** Every important people decision should have a rubric around how folks are evaluated.
2. **Selecting project leaders.**
3. **Explicit budgets.** Instead of reasonable number of conferences per year, specify a fixed number. Instead of general ongoing education budget, make it explicit.
4. **Nudge involvement.** It's very effective to reach out to those folks directly and recommend they apply.
5. **Educational programs.** Ongoing training and learning programs available for everyone, or, for all managers.

We can measure opportunity, some useful metrics:
1. **Retention.** This is the most important measure. Slow to show change.
2. **Usage rate** is how often folks get picked in project selection.
3. **Level distribution** is useful, in particular comparing cohorts of folks with different backgrounds, like underrepresented minorities and women.
4. **Time at level** is how long team members wait between promotions.

Some of this data will require partnering with your human resources team.

#### Membership

Membership is the precondition to belonging. Impactful programs could be:
1. **Recurring weekly events** held during work hours, like a paper-reading group.
2. **Employee resource groups (ERGs)** create opportunities for folks with similar backgrounds to build community.
3. **Team offsites** once a quarter. Spending a day together learning and discussing is surprisingly effective.
4. **Coffee chats**, maybe randomly assigned, get folks from different teams interacting.
5. **Team lunches** give folks time to relax a bit and interact socially.

Measuring remains extremely important:
1. **Retention**
2. **Referral rate**
3. **Attendance rate**
4. **The quantity and completion rate of coffee chats**

### Select project leads

Having a wide cohort of coworkers who lead critical projects is one of the most important signifiers of good organisational health. Critical projects are scarce while other projects are abundant.

To increase the number of folks leading these projects:
1. **Define** the project's scope and goals in a short document.
  * Time commitment
  * Requirements to apply
  * Selection criteria
2. **Announce** the project
  * Allow folks to _apply in private_
  * Make sure that applicants _don't see who else has applied_. Less experienced people may get discouraged to apply if they see seniors apply.
  * Give _at least three working days for people to apply_.
3. **Nudge** folks to apply who you think would be good candidates but may not self-select.
4. **Select** a project leader based on the selection criteria. Write up a paragraph or two about each of them. Once you've selected the leader, privately reach out to them to confirm that they're able to commit.
5. **Sponsor** the project leader by finding someone accountable for coaching the leader to successful completion.
6. **Notify** other individuals who applied that they were not selected. It's extremely helpful if you provide them feedback, create room for another person to learn.
7. **Kick off** the project, notifying who the project leader is, who the sponsor is, and what their plan is.
8. **Record** the project, who was selected, and who the sponsor is into a public spreadsheet. Link to a project brief.

### Make your peers your first team

Folks that consistently look for each other are willing to disappoint the teams they manage in order to help their peers succeed. These people have shifted their _first team_ from the folks they support to their peers.

Ingredients:
* **Awareness of each other's work**. This requires a significant investment of time. This could be achieved sharing weekly progress.
* **Evolution from character to person**. It is much easier to understand people you know personally.
* **Refereeing defection**. _Dominant strategy_ is one that is expected to return maximum value regardless of the actions of other players. Team collaboration is not a dominant strategy, it depends on everyone participating in good faith. Then defection happens, coordination is only possible via a manager or a highly respected team member.
* **Avoiding zero-sum culture**. Positive cultures center on recognising impact, support, and development.
* **Making it explicit**. You still have to explicitly discuss the idea of shifting folks' identities away from the team they support and toward the team of their peers.

Treating your peers as your first team _allows you to practice your manager's job_.

One of the most important things a first team does is provide a _community of learning_. Your peers can only provide excellent feedback if they're aware of your work. To speed up your learning, join a rapidly expanding company, and make your peers your first team.

### Consider the team you have for senior positions

Letting individuals apply is the easy part. You must announce each position and ask for internal candidates. The trickier part is evaluation.

Ensure you are testing the following categories:
1. **Partnership**. Have they been effective partners to their peers, and to the team they've managed?
2. **Execution**. Can they support the team in operational excellence?
3. **Vision**. Can they present a compelling, energising vision of the future state of their team and its scope?
4. **Strategy**. Can they identify the necessary steps to transform the present into their vision?
5. **Spoken and written communication**. Can they convey complicated topics in both written and verbal communication?
6. **Stakeholder management**. Can they make others, especially executives feel heard?

For testing these categories, use these tools:
* **Peer and team feedback**. Collect written feedback. Listen to would-be dissenters and hear their concerns.
* **A 90-day plan**. The applicant writes a 90-day plan on how they'd transition into the role, and what they would focus on.
* **Vision/strategy document**. The applicant writes a combined vision/strategy document. Where the new team will be in two to three years.
* **Vision/strategy presentation**. Have the applicant present their vision/strategy document to a group of three to four peers.
* **Executive presentation**. Have the applicant present their strategy document one-on-one, with an executive.

Keep in mind that internal processes are awkward, don't decide to avoid this awkwardness, you can't.

### Company culture and managing freedoms

"Freedom's just another word for nothing left to lose".

We should make a distinction between positive and negative freedoms.

A positive freedom is your freedom to _do_. Like to blow smoke into neighbours porch.

Negative freedom is your freedom _from_ things. Like having your neighbours blow smoke onto your porch.

Each positive freedom we enforce strips away a negative freedom, and each negative freedom we guarantee eliminates a corresponding positive freedom ([Paradox of Positive Liberty](https://plato.stanford.edu/entries/liberty-positive-negative/#ParPosLib)).

**The balancing of positive and negative freedoms is a fundamental task of managers and management.**

Freedom is a loaded term, so it's easy to deteriorate into a moral discussion.

[Tom DeMarco's _Slack_](https://www.goodreads.com/book/show/123715.Slack) has an excellent suggestion for a good starting state between positive and negative freedoms for engineering teams: **follow the standard operating procedure, but always change one thing for each new project.**

### Kill your heroes, stop doing it harder

Unless your problem is that people aren't trying hard, the "work harder" mantra only breeds hero programmers whose heroic ways make it difficult for nonheroes to contribute meaningfully.

Your options are limited: either kill the environment that breeds hero programmers, or kill the hero programmer by burnout.

Their presence limits the effectiveness of those around them in exchange for short-term burst of productivity fuelled by long hours and minimised communication costs.

These long hours burn your heroes out, and they will either quit or you shove them into a corner.

If hard work and breeding heroes doesn't work, what does?

If you set the original direction and hve the leverage to change directions, then resetting is as simple as standing up and taking the bullet for the fiasco you're embroiled in.

Without policy, your tool is stepping back and allowing the brokenness to collapse under its own weight. You conserve your energy and avoid creating rifts by pushing others away in hero mode, and you will be ready to be part of new, hopefully functional, system after the reset.

## Careers

### Roles over rocket ships, and why hypergrowth is weak predictor of personal growth

Stay everywhere at least two years, and look for a place where you could spend four years to serve as the counterweight for those two year stints.

Thriving requires both finding a way to succeed in each new era and successfully navigating the transitional periods.

#### Your new career narrative

Each time there was a change that meaningfully changed how you work, mark that down as a transition.

How did the values and expectations change? What skills did you depend on the most, and which of your existing skills fell out of use?

#### Opportunities for growth

Both the stable and the transitions are great opportunities for growing yourself. Transitions are opportunities for new skills, and stable periods for developing mastery in the skills in the new era values.

What matters most is the particular team you join.

> If you're offered a seat on a rocket ship, don't ask what seat! Just get on.

**Growth only comes from change, and that is something you can influence.**

### Running a humane interview process

There is still a lot of whiteboard programming out there, mainly due inertia and coarse-grained analytics.

Interviewing well is far from easy, but is fairly _simple_:
1. Be kind
2. Ensure that all interviewers agree on the role's requirements
3. Understand the signal your interviewer is checking for
4. Come prepared
5. Express interest in candidates
6. Create feedback loops for interviewers
7. Instrument and optimise as you would any conversion funnel

#### Be kind

Allow the candidate a few minutes to ask questions. You can't be kind if your interviewers are tightly time-constrained.

**Unkind interviewers usually suffer interview burnout, give them an interview sabbatical for a month or two.**

#### Finding signal

Break your interview into a series of interview slots that together cover all the signals. Each skill is covered by two different interviewers for redundancy in signal detection.

Effective interview formats:
1. Prepared presentations, talk about a given topic for 30 minutes.
2. Debugging or extending an existing codebase on a laptop (ideally on _their_ laptop).
3. Giving demos of an existing product or feature (ideally they one they've be working on).
4. Roleplays

The key point i to keep trying new approaches that improve your chance of finding signal.

#### Be prepared

Being unprepared shows a disinterest in the candidate's time, your team's time, _and_ your own time.

#### Deliberately express interest

Make your candidate know that you're excited about them.

Have every interviewer send a note to them saying that they enjoyed the interview.

#### Feedback loops

Pair interviews, practice interviews, and weekly sync-ups between everyone strategically involved in recruiting, work actively to improve your process.

Ask every candidate to fill an anonymous Glassdoor review.

#### Optimise the funnel

Instrumenting the process at each phase (sourcing, phone screens, take-home tests, onsites, offers, and so on).

Don't obsess about it, optimising the funnel should be the last priority. You should measure first, and optimise second.

### Cold sourcing: hire someone you don't know

Sources of candidates are _referrals_ from your existing team, _inbound_ applications who apply on your jobs page, and _sourced_ candidates whom you proactively bring into your funnel.

**Referrals come with two major drawbacks: personal network will always be quite small and folks tend to have relatively uniform networks.**

#### Moving beyond your personal networks

Hiring managers freeze up when their referral network starts to dry up. Could sourcing is reaching out directly to people you don't know.

A concise, thoughtful invitation to discuss a job opportunity is an opportunity, not an infringement, especially for those who are on sites like Linkedin.

#### Your first cold sourcing recipe

1. Join Linkedin (or other networks like GitHub)
2. Seed your network with some people you know because it'll increase the reach of your second-degree network.
3. Be patient, you'll get throttled pretty frequently.
4. Use the search function to identify second-degree connections to connect to.
5. When someone accepts your connection request, grab their email and send them a short, polite note inviting them to coffee or a phone call. Customisation matters less, people mostly choose to respond based on their circumstances, not on the quality of your note.

  Hi $THEIR_NAME
  I'm an engineering manager at $COMPANY, and I think you would be a great  fit for $ROLE (link to your job description).
  Would you be willing to grab a coffee or do a phone call to discuss sometime in the next week?
  Best.
  $YOUR_NAME

  Run an A/B test with something more personalised or sophisticated.
6. Schedule an enjoy your coffees and chats. Figure out if there is a good mutual fit between the candidate and the role, if there is a good fit, try to get them to move forward with your process. Tell them why are you excited about the company and role discussed.
7. Keep spending an hour each week adding more connections and following up with folks who have connected. It is a practice that rewards consistency.

#### Is this high-leverage work?

Candidates are more excited to chat with someone who/d be managing them than they are to chat with a recruiter. It gives a signal showing that managers care about hiring enough to invest their personal energy and attention into it.

Be concerned if an engineering manager spends more than an hour a week on sourcing (not including follow up chats).

A clear indicator of strong recruiting organization is a close and respectful partnership between recruiting and engineering.

### Hiring funnel

#### Funnel fundamentals

* **Identify** where candidates tend to come from.
  * _Inbound_ are candidates who apply to you directly, via the jobs website, job postings on LinkedIn and other job sites. These tend to be high on volume and low on quality.
  * _Sourced_ are candidates you proactively find an engage with by using LinkedIn, colleagues and networking at conferences and meetups.
  * _Referrals_ are candidates someone at your company already knows. This is usually the most efficient source of candidates.
* **Motivate** people to come interview
  * _Spend time_ with them, get them excited about learning from each other.
  * _Clearly define the role_, what they'd be doing. Be honest and a bit optimistic.
* **Evaluate** if they'll be a successful addition to your team.
  * Be as confident as possible that the candidate will be a success in your company.
  * You want their motivation to increase as they're evaluated.
  * Minimise the amount of time invested by both your team and the candidate.
* **Close**, from compensation packages to benefits, to making them feel needed.

#### Instrument and optimise

The first step is looking at the conversion rates across each phase and investing in improving those rate. Find what the upper bounds for each section should be, benchmarking against your peer companies is the only way.

#### Extending the funnel

Instead of ending your funnel at closing candidates, add a few more phases:
* **Onboard**. How long does it take new hires to get up to speed? Pick a productivity metric, like commits per week. How long does it take to reach P40 productivity?
* **Impact**. How impactful are the people you're hiring? You can look out at performance rating distributions on time since hiring.
* **Promote**. How long does it take to get promoted after they're hired?
* **Retain**. Are the people you hire staying?

### Performance management systems

#### Career ladders

These are the foundation of an effective performance management system. They describe the expected behaviours and responsibilities for a role.

Try to make a ladder for each unique role that have at least 10 individuals.

One method for reducing the fixed cost of maintaining ladders is to establish a _template_ and _shared themes_ across every ladder. This also focuses on a set of common values across the company.

Each ladder is composed of levels, which describes how the role evolves in responsibility and complexity as the practitioner becomes more senior. Crisp level boundaries reduce ambiguity while promoting people. These boundaries are also important because they provide to those on the ladder where they are on the journey. Level definitions are quite effective at defining the behaviours.

A good ladder allows individuals to accurately self-access. A bad ladder is ambiguous and requires deep knowledge of precedent to apply correctly.

#### Performance designations

The next step is to apply the ladder. People can use the ladder as a guide for self-reflection, but you'll also want to create formal feedback in the form of a performance designation, which is how an individual is performing against the expectations of their career ladder at their current level.

More important than the scale used for rating, is how the ratings are calculated
1. **Self-review** written by the individual receiving the designation. Explicitly compare and contrast against their appropriate ladder and level. A ["Brag Document"](https://jvns.ca/blog/2017/12/31/2017--year-in-review/) may be a good idea.
2. **Peer reviews** written by peers, which are useful for recognising mentorship and leadership contributions. They are also useful for identifying problems. Peers are generally not comfortable providing negative feedback.
3. **Upward reviews**. Similar to a _peer review_, these are used to ensure manager's performance includes the perspective of the individuals they manage.
4. **Manager reviews**, written by the individuals' manager, typically a synthesis of the self-peer, and upwards reviews.

With these, you can establish a _provisional designation_, which you can use as input to a calibration system. **Calibrations are rounds of reviewing performance designations and reviews, with the aim of ensuring that ratings are consistent and fair across teams.**

Promotions are typically also considered during calibration process. They are pretty hard to do well. Some useful rules for calibrations:
1. **Adopt a shared quest for consistency** as a community of co-workers working together toward the correct designations.
2. **Read, don't present**, managers are effective, concise presenters. Don't allow managers to pitch their candidates, have everyone read the manager review.
3. **Compare against the ladder, not against others**
4. **Study distribution, don't enforce it**. It may be useful to review the distributions across different organisations and discuss why they appear to be deviating.

Feedback for weak performance should be delivered immediately.

#### Performance cycles

Most companies do either annual or biannual performance cycles.

### Career levels, designation momentum, level splits, etc.

If designation momentum is not taking you a direction you're happy with, set clear goals to your manager, and iterate together toward an explicit agreement on the expectations to hit the designation you are aiming for.

**The goals need to be ambitious enough that your manager can successfully pitch the difficulty to their peers during calibration.**

**Tit-for-that.** Calibration systems without strong process and fair referees can degrade into tit-for-that favour trading.

**Level expansion**. As your company ages, it will inevitably add levels to support career progression.

**Level drift.** Levels added at the top create downward pressure on existing levels. Expectations at a given level decrease over time.

**Opening of the gates.** The combination of _level expansion_ and _level drift_ leads to periodic burst in which a cohort of individuals cross level boundaries together.

**Career level.** The level where most individuals are not expected to progress beyond.

**Time-at-level limits.** Employees who haven't yet reached _career level_ are expected to progress toward the career level at a consistent pace.

**Crisis designations.** Companies sometimes find themselves in difficult situations where key individuals or even key teams that they consider to be at-risk. One of the tools for addressing this situation is to recognise these individuals' importance through elevated performance designations. These sacrifice long-term usefulness to manage short-term difficulty. Generally try to avoid this if possible.

### Creating specialised roles, like SRE or TPMs

#### Challenges

The major challenges while rolling out new roles are:
* **Class systems**. Folks often look at new roles as less important. Sometimes are intended to reduce work for another role as opposed to having an empowering mission of their own.
* **Brittle organisation**. As you move away from generalised roles and toward specialists, your organisation has far more single points of failure.
* **Pattern matching**. Folks pattern match on how they've seen the role done elsewhere. People will avoid taking any steps to learn how the role is intended to function.
* **Task offloading**. Individuals will view it as an opportunity to offload tasks that they find challenging, difficult or uninteresting.
* **Roles too "trivial" to value**. Many roles start by taking on work that is viewed uninteresting. Individuals tend to view that work as trivial and unimportant.
* **Roles too "trivial" to promote**. The work done by new roles is often valued very highly, but not viewed sufficiently "strategic" to merit promotion.
* **Head count obstacles**.
* **Recruiting rare humans**. People want the first hire for a new role to be a strong role model, which usually makes impossible for any candidate to pass the bar.
* **Inability to evaluate**. The existing organisation has so little experience with the new function that don't know how to properly evaluate. This leads to evaluations focused on qualities that are independent to what the candidate would be doing.

#### Facilitating success

The ingredients to bootstrap a new role successfully:
* **Executive sponsor**. Find an authorised, senior leader who is committed to the success of the new function. If you can't find a sponsor, it may mean that leadership doesn't believe on the new role.
* **Recruiting partner**. Make sure that your recruiting team is able to support a new role.
* **Self-sustaining mission**. You might describe TPMs as offloading project management responsibilities for engineering managers. This frames the role as auxiliary, which makes it difficult to recognise impact. You must be able to frame the role's work without referencing other existing roles in order for it to succeed long-term.
* **Career ladder**. New roles should have a career ladder from the beginning, this is the foundation of a successful performance management.
* **Role model**. You want to have a person you can point to.
* **Dedicated calibrations**. Sometimes managers try to perform calibration with mixed roles in a single session, which leads to smaller roles being treated as afterthoughts. Consider dedicated calibration sessions for the one role, or consider all smaller roles together.

#### Advantages

Creating a new role has some advantages:
* **Efficiency**. Specialised roles are able to spend more time doing a smaller set of tasks, which leads to great expertise that can be translated in significantly more overall throughput without increasing head count.
* **Efficiency solve constraints**. You can add exactly the kind of capacity you are missing. If your organisation is low on project management bandwidth, you could add five new managers who can each other take on a bit of it, or you might be able to add a single project manager who individually adds as much relevant bandwidth as the five managers combined.
* **Recognition**. It provides additional structural mechanisms to support recognition.
* **Evaluating for strengths**. It's often challenging to interview specialists because you'll typically evaluate them based on your generalist position. Creating a new role makes it possible to target the interview process on the ares that are most important.
* **Increased hiring pool**.
* **Specialised compensation**.

#### What to do

**Create a new role if it immediately be covered with at least 20 individuals, be reluctant to create a new role if it would take 2 years to hire 20 individuals.**

### Designing an interview loop

* **Metrics first**. Do not start designing a new interview loop without instrumenting your hiring funnel.
* **Understand the current loop's performance**. What you think does and doesn't work well in your current process.
  * Funnel performance
  * Employee trajectory
  * Candidate debriefs
* **Learn from peers**. Chat with folks who have interviewed at other companies for the kind of role you're hoping to evaluate.
* **Find role models**.
* **Identify skills** that are essential to candidate's success and rank them from most to least important.
* **Test for each skill**. For each skill, design a test to evaluate the candidates' strengths.
* **For each test, a rubric**. Write a rubric to assess performance on each test. These should include explicit scores and criteria for reaching each score.
* **Group tests into interviews**. Group them into sets that can be performed together in a single 45-minute interview.
* **Run the loop**. Early on, you should be asking candidates what did or didn't work well.
* **Review the hiring funnel**. Review the funnel metrics to see how it's working out.
* **Schedule an annual refresh**. Schedule a review for a year out.

A few more general pieces of guidance:
* **Try to avoid design by committee**. Prefer a working group of one or two people.
* **Don't hire for potential**. It is a major vector for bias.
* **Use your career ladder**.
* **Iterate on the interview a little**. Spend time iterating on the interview format.
* **Iterate on the rubric a lot**. Pay attention and incorporate edge cases and ambiguities.
* **A/B testing loops**.
* **Hiring committees** as an alternative to A/B testing. A centralised hiring committee that identifies trends across new loops.

Avoid reusing stuff that you know doesn't work and approach the matter with creativity and iteration.

## Appendix

### Tools for operating a growing organisation

One tension in management is staying far enough out of the details to let folks innovate, yet staying near enough to keep the work well-aligned with your company's value structures.

#### Line management

Around the time your team reaches three engineers, you'll want to be running a **spring process**.

You can evaluate if a team's sprint works well:
1. _Team_ knows what they should be working on.
2. _Team_ knows why their work is valuable.
3. _Team_ can determine if their work is complete.
4. _Team_ knows how to figure out what to work on next.
5. _Stakeholders_ can learn what the team is working on.
6. _Stakeholders_ can learn what the team plans to work on next.
7. _Stakeholders_ know how to influence the team's plans.

The **backlog** is a context-rich interface that you'll use to negotiate changes in direction and priority with your stakeholders.

You also want to develop a **roadmap** describing your high-level plans over the three to twelve months.

Your backlog will be a bit more detailed while your roadmap will look further into the future.

#### Middle management

As you move into middle management, you'll become responsible for two to five line managers. **You'll need to shift away from day-to-day execution to give your line managers room to make an impact**.

You'll spend more time on your _roadmaps_:
* From receiving asks from stakeholders to deeply understanding what is motivating those asks.
* Continuously validate that your teams' efforts are valuable.
* You'll want to start a **weekly staff meeting** with your managers. You can do brief updates from each attendee, at most a couple of minutes per person, and then move into group discussions on shared topics, like running effective sprints planning, career development or whatever else proves useful.
* Once you start observing misalignment, it's time for each team to write a **vision document**.
* **Start skip-level on-on-ones** to ensure that there are direct, open channels for feedback about your managers and your teams.

#### Managing an organisation

Once your organisation gets larger, you may end up managing middle managers.

You have to ensure that every team has a clear set of **directional metrics** in an easily discoverable dashboard. It should cover longer-term goals of the team (user adoption, revenue, return users, etc.), and the operational baselines necessary to know if the team is functioning well (on-call load, incidents, availability, cost, etc.). The dashboard should make things clear: the current value, the goal value, and the trend between them.

Your staff meetings can start with a quick metrics review to give a sense of whether there is somewhere you need to drill in. You can focus your attention on projects that are exceeding or struggling.

Another interesting mechanism is **team snippets**. Every two to four weeks give snapshots of each team's sprints: what are they doing, and what they're planning to do next.

### Useful books

* [Thinking in Systems: A Primer](https://www.goodreads.com/book/show/3828902-thinking-in-systems)
* [Don't Think of an Elephant! Know Your values and Frame the Debate](https://www.goodreads.com/book/show/13455.Don_t_Think_of_an_Elephant_Know_Your_Values_and_Frame_the_Debate)
* [Peopleware: Productive Projects and Teams](https://www.goodreads.com/book/show/67825.Peopleware)
* [Slack: Getting Past Burnout, Busywork, and the Myth of Total Efficiency](https://www.goodreads.com/book/show/123715.Slack)
* [The Mythical Man-Month](https://www.goodreads.com/book/show/13629.The_Mythical_Man_Month)
* [Good Strategy/Bad Strategy. The Difference and Why it Matters](https://www.goodreads.com/book/show/11721966-good-strategy-bad-strategy)
* [The Goal: A Process of Ongoing Improvement](https://www.goodreads.com/book/show/113934.The_Goal)
* [The Five Dysfunctions of a Team](https://www.goodreads.com/book/show/21343.The_Five_Dysfunctions_of_a_Team)
* [The Three Signs of a Miserable Job](https://www.goodreads.com/book/show/749937.The_Three_Signs_of_a_Miserable_Job)
* [Finite and Infinite Games](https://www.goodreads.com/book/show/189989.Finite_and_Infinite_Games)
* [Inspired: How to Create Tech Products Customers Love](https://www.goodreads.com/book/show/35249663-inspired)
* [The Innovator's Dilemma: When New Technologies Cause Great Firms to Fail](https://www.goodreads.com/book/show/18750852-the-innovator-s-dilemma)
* [The E-Myth Revisited: Why Most Small Businesses Don't Work and What to do About it](https://www.goodreads.com/book/show/81948.The_E_Myth_Revisited)
* [Fierce Conversations: Achieving Success at Work and in Life, One Conversation at a Time](https://www.goodreads.com/book/show/15017.Fierce_Conversations)
* [Becoming a Technical Leader: An Organic Problem-Solving Approach](https://www.goodreads.com/book/show/714344.Becoming_a_Technical_Leader)
* [Designing with the Mind in Mind](https://www.goodreads.com/book/show/8564020-designing-with-the-mind-in-mind)
* [The Leadership Pipeline: How to Build the Leadership Powered Company](https://www.goodreads.com/book/show/1254.The_Leadership_Pipeline)
* [The Manager's Path: A Guide for Tech Leaders Navigating Growth and Change](https://www.goodreads.com/book/show/33369254-the-manager-s-path)
* [High Output Management](https://www.goodreads.com/book/show/324750.High_Output_Management)
* [The First 90 Days: Proven Strategies for Getting Up to Speed Faster and Smarter](https://www.goodreads.com/book/show/18491275-the-first-90-days-updated-and-expanded)
* [The Effective Executive: The Definitive Guide to Getting the Right Things Done](https://www.goodreads.com/book/show/48019.The_Effective_Executive)
* [Don't Make Me Think: A Common Sense Approach to Web Usability](https://www.goodreads.com/book/show/18197267-don-t-make-me-think-revisited)
* [The Deadline: A Novel About Project Management](https://www.goodreads.com/book/show/123716.The_Deadline)
* [The Psychology of Computer Programming](https://www.goodreads.com/book/show/1660754.The_Psychology_of_Computer_Programming)
* [Adrenaline Junkies and Template Zombies: Understanding Patterns of Project Behaviour](https://www.goodreads.com/book/show/2342271.Adrenaline_Junkies_and_Template_Zombies)
* [The Secrets of Consulting: A Guide to Giving and Getting Advice Successfully](https://www.goodreads.com/book/show/566213.The_Secrets_of_Consulting)
* [Death by Meeting](https://www.goodreads.com/book/show/49040.Death_by_Meeting)
* [The Advantage: Why Organizational Health Trumps Everything Else in Business](https://www.goodreads.com/book/show/12975375-the-advantage)
* [Rise: 3 Practical Steps for Advancing Your Career, Standing Out as a Leader, and Liking Your Life](https://www.goodreads.com/book/show/12838919-rise)
* [The Innovator's Solution: Creating and Sustaining Successful Growth](https://www.goodreads.com/book/show/2618.The_Innovator_s_Solution)
* [The Phoenix Project: A Novel About IT, DevOps, and Helping Your Business Win](https://www.goodreads.com/book/show/17255186-the-phoenix-project)
* [Accelerate: The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organisations](https://www.goodreads.com/book/show/39080433-accelerate)

### Useful papers

* [Dynamo: Amazon's Highly Available Key-Value Store](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf)
* [Hints for Computer System Design](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/acrobat-17.pdf)
* [Big Ball of Mud](https://joeyoder.com/PDFs/mud.pdf)
* [The Google File System](https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf)
* [On Designing and Deploying Internet-Scale Services](https://mvdirona.com/jrh/TalksAndPapers/JamesRH_Lisa.pdf)
* [CAP Twelve Years Later: How the "Rules" Have Changed](https://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed/)
* [Harvest, Yield, and Scalable Tolerant Systems](https://radlab.cs.berkeley.edu/people/fox/static/pubs/pdf/c18.pdf)
* [MapReduce: Simplified Data Processing on Large Clusters](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf)
* [Dapper, a Large-Scale Distributed Systems Tracing Infrastructure](https://research.google/pubs/pub36356/)
* [Kafka: a Distributed Messaging System for Log Processing](https://notes.stephenholiday.com/Kafka.pdf)
* [Wormhole: Reliable Pub-Sub to Support Geo-Replicated Internet Services](https://www.usenix.org/system/files/conference/nsdi15/nsdi15-paper-sharma.pdf)
* [Borg, Omega, and Kubernetes](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/44843.pdf)
* [Large-Scale Cluster Management at Google with Borg](https://research.google/pubs/pub43438/)
* [Omega: Flexible, Scalable Schedulers for Large Compute Clusters](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/41684.pdf)
* [Mesos: A Platform for Fine-Grained Resource Sharing in the Data Center](https://people.eecs.berkeley.edu/~alig/papers/mesos.pdf)
* [Design Patterns for Container-Based Distributed Systems](https://www.usenix.org/system/files/conference/hotcloud16/hotcloud16_burns.pdf)
* [Raft: In Search of an Understandable Consensus Algorithm](https://raft.github.io/raft.pdf)
* [Paxos Made Simple](https://www.microsoft.com/en-us/research/publication/paxos-made-simple/)
* [SWIM: Scalable Weakly-Consistent Infection-Style Process Group Membership Protocol](https://www.cs.cornell.edu/projects/Quicksilver/public_pdfs/SWIM.pdf)
* [The Byzantine Generals Problem](https://www.microsoft.com/en-us/research/publication/byzantine-generals-problem/)
* [Out of the Tar Pit](https://www.microsoft.com/en-us/research/publication/byzantine-generals-problem/)
* [The Chubby Lock Service for Loosely-Coupled Distributed Systems](https://static.googleusercontent.com/media/research.google.com/en//archive/chubby-osdi06.pdf)
* [Bigtable: A Distributed Storage System for Structured Data](https://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf)
* [Spanner: Google's Globally-Distributed Database](https://static.googleusercontent.com/media/research.google.com/en//archive/spanner-osdi2012.pdf)
* [Security Keys: Practical Cryptographic Second Factors for the Modern Web](https://fc16.ifca.ai/preproceedings/25_Lang.pdf)
* [BeyondCorp: Design to Deployment at Google](https://research.google/pubs/pub44860/)
* [Availability in Globally Distributed Storage Systems](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36737.pdf)
* [Still All on One Server: Perforce at Scale](https://info.perforce.com/rs/perforce/images/GoogleWhitePaper-StillAllonOneServer-PerforceatScale.pdf)
* [Large-Scale Automated Refactoring Using ClangMR](https://research.google/pubs/pub41342/)
* [Source Code Rejuvenation is not Refactoring](https://s3.amazonaws.com/systemsandpapers/papers/sofsem10.pdf)
* [Searching for Build Debt: Experiences Managing Techncial Debt at Google](https://s3.amazonaws.com/systemsandpapers/papers/sofsem10.pdf)
* [No Silver Bullet, Essence and Accident in Software Engineering](https://s3.amazonaws.com/systemsandpapers/papers/sofsem10.pdf)
* [The UNIX Time-Sharing System](https://people.eecs.berkeley.edu/~brewer/cs262/unix.pdf)
