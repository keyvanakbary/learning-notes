# [What I wish I had known before scaling Uber to 1000 services](https://www.youtube.com/watch?v=kb-m2fasdDY)

## Why micro services
* Move and release independently
* Own your uptime (on-call)
* Use the "best" tool for the job

## What are the costs
* Now you have a distributed system
* Everything is an RPC
* What if it breaks?

## Less obvious costs
* Everything is a trade-offs, you are going to give something up
* You can build around problems
* Might trade complexity for politics
* You get to keep your biases

## Tech stack
* Pre-history: PHP (outsourced)
* Dispatch: Node.JS, moving Go
* Core Services: Python, moving to Go
* Maps: Python and Java
* Data: Python and Java
* Metrics: Go

## Different languages costs
* Hard to share code
* Hard to move between teams
* What I wish I knew: Fragments the culture

## RPC
* HTTP/REST gets complicated
* JSON needs a schema
* RPCs are slower than PCs
* What I wish I knew: Servers are not browsers

## How many repos
* With one repo you can make cross-project changes easier. Not really usable
* Multiple repos
* 7000 repositories

## Operational
* What happens when things break? Downstream dependencies; people issues, people fix your service
* Can other teams release your service?
* Understand a service in the larger context

## Performance
* Depends on language tools. Tools are all different. Flamegraphs
* If dashboards are not generated automatically, teams create their own. This could be solved as if you expose your service automatically, to generate the dashboards automatically and homogeneously across all teams
* Doesn't matter until it does. You can place SLAs
* Probably want at least simple perf requirements
* What I wish I knew: "good" not required, but "known" is

## Fanout
* Go for the slowest thing that you have in your chain
* Overall latency >= latency of slowest.
* Looking at p95, p99, p99.9

## Tracing
* Lots of ways to get this. Zipkin, Open-tracing, etc.
* Best way to understand fanout
* Probably want sampling
* What I wish I knew: cross-lang context propagation

## Logging
* Need consistent, structure logging
* Multiple languages makes this hard
* Logging floods can amplify problems
* What I wish I knew: Accounting

## Load testing
* Need to test against production
* Without breaking metrics
* Preferably all the time
* What I wish I knew: All systems need to handle "test" traffic

## Failure testing
* What I wish I knew: People won't like it

## Migrations
* Old stuff still has to work, you cannot stop the world, people are making changes all the time
* What happened to immutable?
* What I wish I knew: mandates are bad. People will be more willing for change if you provide a better system rather than forcing them to change the current one

## Open source
* Build/buy trade-off is hard
* Commoditisation
* What I wish I knew: This will make people sad

## Politics
Services allow people to play politics. Politics happen when "Company > Team > Self" is out of order.

## Trade-offs
Everything is a trade-off
Try to make them intentionally