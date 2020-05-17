# [Managing The Development of Large Software Systems](http://www-scf.usc.edu/~csci201/lectures/Lecture11/royce1970.pdf)

The context for this paper was related with the development of software packages for spacecraft mission planning, commanding and post-flight analysis.

There are two essential steps of computer programs regardless of the size or complexity: Analysis and coding. However, manufacturing large software projects taking into account only these steps ia doomed to failure.

A more grandiose approach precedes two levels of requirement analysis, separated by a design step and followed by a testing step. These steps are separated because they are planned and staffed differently in terms of resources.

    System Requirements
        ↘
        Software Requirements
            ↘
            Analysis
                ↘
                Program Design
                    ↘
                    Coding
                        ↘
                        Testing
                            ↘
                            Operations

The iterative relationship between phases can be reflected in the following scheme. Each step progresses and the design is further detailed.

Hopefully the interaction is confined in successive steps:

    System Requirements
        ↖  ↘
        Software Requirements
            ↖  ↘
            Analysis
                ↖  ↘
                Program Design
                    ↖  ↘
                    Coding
                        ↖  ↘
                        Testing
                            ↖  ↘
                            Operations

The problem is that design iterations are never confined to successive steps:

    System Requirements
        ↘
     ┌► Software Requirements
     │      ↘
     │      Analysis
     │          ↘
     └───────── Program Design ──┐
                    ↘            │
                    Coding       │
                        ↘        │
                        Testing ◄┘
                            ↘
                            Operations

## Step 1: Program design come first

A first step towards fixing the previous problem is to introduce a preliminary program design step between the software requirements and analysis phase. Critics can argue about the program designer being forced to design in a vacuum of software requirements without any analysis, and that the preliminary design may result in substantial error; and that would be correct, but it would miss the point. This is intended to assure the software won't fail because of storage, timing or data flux reasons. As analysis proceeds, collaboration must happen between the program designer and the analyst, so proper allocation of execution time and storage resources happens.

    ┌─────┐        ┌─► Document System Overview
    └─────┘        ├─► Design Database and Processors
        ↘          ├─► Allocate Subrutine Storage
        ┌─────┐    ├─► Allocate Subrutine Execution Times
        └─────┘    ├─► Describe Operating Procedures
            ↘      │
            Preliminary Program Design
                ↘
                ┌─────┐
                └─────┘
                    ↘
                    ┌─────┐
                    └─────┘

The procedure is made from these steps:
1. Begin the design with program designers, not analysts or programmers.
2. Design, define and allocate the data processing modes even at risk of being wrong.
3. Write an overview document that is understandable, informative and current.

## Step 2: Document the design

The first rule of managing software development is ruthless enforcement of documentation requirements. Management of software is simply impossible without a very high degree of documentation.

    System Requirements
        ↘
        Software Requirements ─► Doc 1: Software Requirements
            ↘
            Preliminary Software Design ─► Doc 2: Preliminary Design (Spec)
                ↘
                Analysis            ┌─► Doc 3: Interface Design (Spec)
                    ↘               ├─► Doc 4: Final Design (Spec)
                    Program Design ─┴─► Doc 5: Test Plan (Spec)
                        ↘
                        Coding ─► Doc 4: Final Design (As Built)
                            ↘
                            Testing ─► Doc 5: Test Plan (Spec), Test Results
                                ↘
                                Operations ─► Doc 6: Operating Instructions

Why so much documentation?
1. Each designer must communicate with interfacing designers, so prevents the designer from hiding behind the "I'm 90 percent finished"
2. During the early phase of software development the documentation **is** the specification and **is** the design.
3. The real monetary value of good documentation begins downstream
    1. **During the testing phase**, the manager can concentrate on personnel on the mistakes in the program.
    2. **During the operational phase**, the manager can use operational-oriented personnel to operate the program and to do a better job, cheaper. Without good documentation the software must be operated by those who built it. These people are relatively disinterested in operations and do not do as effective job as operations-oriented personnel.
    3. **Following initial operations**, good documentation permits effective redesign, updating, and retrofitting in the field.

## Step 3: Do it twice

After documentation, the second most important criterion for success revolves around whether the product is totally original. The final version delivered to the customer for operational deployment should be actually the second version. The point for this is that questions fo timing, storage, etc. which are otherwise matters of judgement, can now be studied with precision. Without this simulation, the project manager is at the mercy of human judgement.

                  ┌─► Preliminary Design ┐
    ┌─────┐       ├─► Analysis           │
    └─────┘       ├─► Program Design     │
        ↘         ├─► Coding             ├────┐
        ┌─────┐   ├─► Testing            │    │
        └─────┘   ├─► Usage              ┘    │
            ↘     │                           │
            Preliminary Program Design        │
                ↘                             │
                Analysis ◄────────────────────┤
                    ↘                         │
                    Program Design ◄──────────┤
                        ↘                     │
                        Coding ◄──────────────┤
                            ↘                 │
                            Testing ◄─────────┤
                                ↘             │
                                Operations ◄──┘

## Step 4: Plan, control and monitor testing

The biggest user of project resources is the test phase. It is also the phase of greatest risk in terms of dollars and schedule.

The previous recommendations, to design before analysis and coding, to document and to build a pilot are about uncovering and solving problems before entering the testing phase.

Recommendations in order to plan for testing:
1. Many parts of tests process are best handled by test specialists. With good documentation it is feasible to use specialists, which do a better job of testing than the designer.
2. Most errors can be easily spotted by visual inspection, in the nature of proofreading the analysis and code. Do not use the computer to detect this kind of thing, it is too expensive.
3. Test every logic path at least once with some kind of numerical check.
4. Turn over the software to the test area for checkout purposes.

## Step 5: Involve the customer

It is important to involve the customer at earlier points before the final delivery. Leaving the contractor free between requirement definition and operation means trouble. Following requirements definition where the insight, judgement, and commitment of the customer can bolster the development effort.

    System Requirements (Update) ◄─ System Requirements Generation
        ↘
        Software Requirements 
            ↘
            Preliminary Software Design ─► PSR: Preliminary Software Review ──┐
                                                                              │
                Analysis ◄────────────────────────────────────────────────────┘
                    ↘               ┌─► CSR 1: Critical Software Review 1 ┐
                    Program Design ─┼─► CSR 2: Critical Software Review 2 ├───┐
                                    └─► CSR N: Critical Software Review N ┘   │
                        Coding ◄──────────────────────────────────────────────┘
                            ↘
                            Testing ─► FSAR: Final Software Acceptance Review ┐
                                                                              │
                                Operations ◄──────────────────────────────────┘

---

Worth noting that each item cost some additional sum of money.
