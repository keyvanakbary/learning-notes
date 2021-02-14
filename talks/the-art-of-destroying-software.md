# [The Art of Destroying Software](https://vimeo.com/108441214)

One of the beautiful things about deleting code is that it allows you to change your mind.

[Waterfall paper](http://www-scf.usc.edu/~csci201/lectures/Lecture11/royce1970.pdf), one of the biggest ironies in our industry; it basically describes agile.

[Big ball of mud paper](https://joeyoder.com/PDFs/mud.pdf). It argues that the big ball of mud is inevitable. The way to tackle it is to create pockets of smaller ball of muds. You have to write code for the purpose of deleting it.

What if you developed software with the purpose of deleting it.

Apply the lessons of Erlang to the rest of the software. Microservices help on this vision, if we have many services, I can delete and rewrite them.

The definition of refactor is to either change my test or my code. Refactor changing the code and the test at the same time is called *refucktor*. The whole point of TDD is to make one of the sides stable so you can modify the other. It's a measurement, I'm predicting what will happen. Many refactoring tools change both sides at the same time. Your tools affect the code you are building.

There is no way of having a 12 months project to refactor the `ls` program. The Unix way of doing things is the same as microservices, the same as the Erlang way. When we have small programs, we are not afraid anymore of deleting and rewriting them from scratch. We should optimise for their delete ability. Imagine how wonderful to know you could delete code without side-effects.

The best way to optimise for deletability is to run away from monoliths, from decoupling. You should run coupling analysis in your software, there are great tools for it like Sonar.

Microservices shouldn't be big or small, shouldn't be bigger than a week worth of rewrite. My personal risk if I had to do a rewrite is a week. If I later I get a better understanding of the model, it's just a week.

Business people won't understand 3 months of tackling "technical debt" without providing value to customers.

When you find that your models are wrong, just delete the code.

Debt is not bad, debt allows you to buy your house! Same is true for technical debt. Sometimes you can ship crap code, would you care that much about crap if you were able to delete it easily? If technical debt start accumulating, delete it.

Working in month-length projects is waste, try to work in 1 week projects. It is also more manageable in your head. Imagine onboarding and understanding the system as a whole.

Get things small, manageable and understandable.

The same for services is the same for objects or actors.

Divide bigger systems into 1 week projects. Refactoring becomes just _deleting_ code.

Alan Kay said that the biggest mistake he made naming the thing Object-Orientation was to call it Object-Orientation instead of Message-Orientation. Bigger programs contain smaller programs that communicate to each other. People nowadays think about the objects and not the messages that go between them. In Erlang, each Object is basically a process. These programs should be 1 week to rewrite.

The secret for consulting is to never build big programs!

The difference between good code and bad code is the size of the programs.

You cannot keep 100.000 lines of code in your head, 3000 unit tests won't help.

Refuse also to deploy more than a thousand lines of code to production. Smaller chunks are easier to deploy, test, rollback and debug.

Teams want to build programs that are inherently too big and too complex.

Developers usually have the habit of solving problems nobody has.

> I could do it in a simple way, but if I did it won't be up to my level of intellect, so I am going to make it more complicated so it is worthy of me.

You won't be able to predict the use case of the future, make your system easier to delete than to change.

Don't plan for future changes, focus on the ability to rewrite from scratch when changes happen. Make decisions in the last responsible moment.

The identifying trait of good code is small isolated programs that can be deleted on the fly.