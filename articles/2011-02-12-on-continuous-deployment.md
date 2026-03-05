# On Continuous Deployment

My friend Kris Bondi asked this morning:

![](images/on-continuous-deployment-01.png)

I'm no continuous deployment expert, but it's gotten some attention after yesterday's [highlight at an Etsy board meeting](http://www.avc.com/a_vc/2011/02/continuous-deployment.html).

Companies making the most of continuous deployment were designed to do so from the very early stages. Designing software for continuous deployment means a combination of the following:

- **Unit tests.** To really achieve the quantity of unit tests needed to call your code "tested," Test Driven Development or Behavior Driven Development techniques are the easiest paths to get there. (Which isn't to say adopting TDD or BDD is easy; just saying not following those principles make it much harder to get adequate code coverage.)
- **Controlled feature cycle.** An engineering team has to get their mind right about pushing code all the time. This is often referred to as "Agile," but these days the term Agile is abused nearly as often as Cloud, so I avoid the term. The meat is that if a team thinks in terms of big pushes every couple of weeks/months, continuous deployment will never happen.
- **Black box tests**. Testing the system from the outside is critical. With a testing tool that can perform critical application flows (including JavaScript runtime), a team can make sure that they haven't broken anything after a code push.
- **Instrumentation**. Above all, whatever combination of the other points are used, clearly readable team-visible displays of the status of the code base at any one time is the most important. This way it's easy to gut-check whether the codebase is in a pushable state or not. It's also easy to see when things break.


It takes a lot of discipline to implement all of the above. It takes even more to make sure that these kinds of processes get put in place early in a company's life.

There's been a lot of talk lately about technical debt, and I'm behind some of that. However, getting the above processes in place is not a place to skimp. Technical debt in instrumentation, for example, is foolish because it results in untrustworthy instruments. (See: [A Boy Who Cried Wolf](http://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf))

Why would a company *not* do continuous deployment? It's usually not a conscious choice to avoid it, but rather a lack of knowledge of or commitment to the practice of continuous deployment at the point where it's most critical. Once a set of customers/executives/board members get used to a certain pace of development, it's hard to put the brakes on to clean up the development and release process. As a result, some companies just never do it. Their releases get less frequent as their feature builds take longer, usually due to a lack of confidence that what they're doing isn't going to break something else.

Companies *can* retrofit their processes to support continuous deployment, but it's rare. It takes convincing people who are happy with how things are that there's a better way. In an "if it ain't broke, don't fix it" world where everyone is conditioned to tread lightly, no one will eagerly step up to dramatically change the way the world turns.

As Etsy or hundreds of other swiftly-moving, customer-pleasing companies will attest, it's a change worth making.
