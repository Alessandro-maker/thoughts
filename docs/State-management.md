# State management

Trivial programs are trivial so develop it as fast as you can.
For non-trivial programs state management is usually the part witch has the biggest **aftereffects**.
Then I think state management is usually the most critical and challenging part of a software.

## First step, start with a state ... hold on, what state?

In any journal the first step is a key step.
Start growing your domain knowledge, inquire business people and people that will interact with the software along the whole organizzatione, search for competitors too.
But don't go too deep, don't rush a low level mental model. It speedup your learning but can backfire later.

When you inquire knowledgeable (non technical) people in the domain try to keep your hand on the wheel of the conversation.
Don't let the conversation get beached in the solution they already thought since long time ... "it's easy, just code it as I say".
Don't let them indulge in too many details (for now).
Just ask for a high level view of data, flow and involved people.
Ask for hints of corner cases and exceptions. Don't go in details (for now) but mark them on the back of your head to get an idea of the size of the problem space.
As a said high level view of the whole problem space, near and far.
There's a thing that you need from this first exploration: clear and sharp ownership and responsibilty **boundaries** that masks the problem space.

Take an up-down approch. Thinks that belong (ownership or responsibilty) to the same organization must stay together.
Shape your mental model inside those boundaries, not the other way around.
Here is where a premature low level model can backfire greatly.

Then investigate the ways data change. Don't ask directly about the data, collect **all** the actions and focus on the mutation.
Lay down witch data change together.
Data that change together need to stay as close as possible.

For the rest try to make your data model as orthogonal as possible with respect to ownership and mutations.
Try to keep apart data that don't change together. Enforce separation for data with different ownership.

Now don't forget to inquire any model detail and any corner case and make adjustmets to the model to include them.

If you want make your model more general than required think twice.
The generalization you have in mind is really cheap now and in the future?
It's worthy (enable business opportunities)?
Why others didn't do it?
Check the tradeoffs and don't make the choice all alone.

## Now we have a state and a list of actions/mutations, how can we manage it?

First of all: is possible to keep all the state in a single place? (possible not easy)
If the answer is yes go for it!

A **single source of truth** has so many advantages that easily outworths most of the tradeoffs you can possibly have.
More precisely not having it gets you multiple Pandora's boxes that keep opening at the worst possible times.
