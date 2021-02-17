# State management

Trivial programs are trivial so develop it as fast as you can.
For non-trivial programs state management is usually the part witch has the biggest **aftereffects**.
For this reason I think state management is usually the most critical and challenging part of a system.

## First step, start with a state ... hold on, what state?

In any journal the first step is a key step.
Start growing your domain knowledge, inquire business people and people that will interact with the system along the whole organization, search for competitors too.
But don't go too deep, don't rush a low level mental model. It speed-up your learning but can backfire later.

When you inquire knowledgeable (both technical and non technical) people in the domain try to keep your hand on the wheel of the conversation.
Don't let the conversation get beached in a solution they already thought since long time ... "it's easy, just code it as I say".
Don't let them indulge in too many details (for now).
Just ask for a high level view of data, flow and involved people.
Ask for hints of corner cases and exceptions. Don't go in details (for now) but mark them on the back of your head to get an idea of the size of the problem space.
Go for an high level view of the whole problem space, near and far.
There's a thing that you absolutely need from this first exploration: clear and sharp ownership and responsibility **boundaries** that mark the problem space.

Take an up-down approach. Thinks that belong (ownership or responsibility) to the same organization must stay together.
Shape your mental model inside those boundaries, not the other way around.
Here is where a premature low level model can backfire greatly.

Then investigate the ways data change. Don't ask directly about the data, collect **all** the actions and focus on the mutations.
Lay down witch data change together.
Data that change together need to stay as close as possible.

For the rest try to make your data model as orthogonal as possible with respect to ownership and mutations.
Try to keep apart data that don't change together. Enforce separation for data with different ownership.

Now don't forget to inquire any model detail and any corner case and make adjustments to the model to include them.

If you want make your model more general than required think twice.
The generalization you have in mind is really cheap now and in the future?
It's worthy (enable business opportunities)?
Why others didn't do it?
Check the tradeoffs and don't make this choice by yourself.

## Now we have a state and a list of actions/mutations, how can we manage it?

### Go for the Holy Grail (aka Single source of truth) ... if you can

First of all: is it feasible to keep all the state in a single place? (feasible not easy)
If the answer is yes go for it!

A **single source of truth** has so many advantages that easily outworths most of the tradeoffs you can possibly have.
More precisely not having it gets you multiple Pandora's boxes that keep opening at the worst possible times.

So you are the lucky guy: single source of truth, all the business logic on the server and just a remote UI (ex.: web).
_Not so fast ..._
Are you sure that your UI call the server at **any** interaction (**every** single click)?
Lets forget for a moment about _difficult_ states as page scroll, control focus and so on.
No forms, no client-side validation, no caches? UI responsiveness and latency are not a problem?
Is so you really are the lucky guy!

If not you have a _not-so-single_ source of truth.
Welcome to cache invalidation and synchronization, updates distribution and eventual consistency.
