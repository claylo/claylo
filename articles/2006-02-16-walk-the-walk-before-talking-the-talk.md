# Walk the Walk Before Talking the Talk

If developers think back (in some cases, WAY back), we can all remember a time when we knew very little about programming. Some will declare that there was never such a time for them, but they’ve just killed enough brain cells that they can’t rememeber.

A question that eventually comes up for programmers who stick with it long enough is: Am I an expert yet? Do I have the chops to throw down with The Big Kids?

In some professions, such as the acting biz (where I came from before I started programming), you can fake it. You don’t have to be an expert if you can just act like an expert long enough for a few people to believe you. Halfway decent actors will often become decent actors just by acting like decent actors. After all, they’re practicing the craft in pretending to know the craft.

It doesn’t work that way in professional development; You’ve either got the chops to call yourself a pro, or you don’t. And more importantly, you either behave like a pro, or you don’t. You can’t *just* claim to be a professional software developer, and in the act of making that claim, become one.

I was reminded of my thoughts along these lines today after reading [Ian Kallan](http://www.arachna.com/roller/page/spidaman/20060206#php_best_practices_frameworks_and) and [J. Scott Johnson](http://fuzzyblog.com/archives/2006/02/15/responding-to-ian-on-php/)’s discussion regarding PHP Best Practices.

What professionalism boils down to in software development (and acting, for that matter) is one thing: **discipline**.

That’s it, and that’s all.

Thing is, the “that’s it” of discipline covers a hell of a lot of ground. To name a few things:

* **You must be disciplined enough to write good code.** PHP, Perl and others are flexible enough to permit developers to write bad (or in some cases, *really* bad) code that still functions … but a pro knows that there’s rarely, if ever, a benefit to banging out crap just because it’s permitted by the language. Quit blaming the tools. PHP isn’t responsible for bad PHP code — people using PHP are responsible for bad PHP code.
* **You must be disciplined enough to write well-documented code.** Yes, functionality counts, but if you’re hit by a bus (or trampled by your fan club at an ego-rally) tomorrow, someone else has to take over your stuff and make sense out of it. For a pro, documentation isn’t grunt work left to the community, or the peons. The pro just does it because it’s what pros do.
* **You must be disciplined enough to use source control.** You don’t talk about using it, or bitch about having to use it, you just do it. If you’re spending a lot of time constantly fighting Subversion or CVS, and you think you’re a pro, you probably need to think again. Source control is as natural to a pro developer as typing with all ten fingers. Get it figured out and adjust to the version-controlled world view if you want to be considered a pro.
* **You must be disciplined enough to write unit tests.** Pros realize that they’re not perfect, and that their code should be tested properly before being rolled out. Bugs should have unit tests written for them to reproduce the bug so that you know when they’re fixed, and as your collection of unit tests grows, you’ll know that they *stay* fixed. Most pros don’t refer to those who “get it” in regard to unit testing as freaks.
* **You must be disciplined enough to write code with error reporting** (by whatever name your language of choice calls it) **cranked to the max.** “use strict”, “error\_reporting(E\_STRICT)” on PHP5 or “error\_reporting(E\_ALL)” on PHP4, whatever: these modes of development weren’t created to annoy you, they were created to save your ass and hopefully help you evolve into a better developer. Writing new code under something as sloppy as “error\_reporting(E\_ALL ^ E\_NOTICE)” should be an absolute last resort.
* **You must be disciplined enough to be disciplined even if you’re the only one working on a project.** After all, we all hope that our next brainchild will either gain a cult following in the open source community, or drum up a truckload of cash via investment or acquisition. At the very least, prepare for the possibility that another developer will join you on a project and may expect some process to be in place. Don’t fall into the trap of having an investor pass on your project because you chose not to be disciplined in your development. It ain’t 1999 anymore: investors these days actually have real studs at their disposal to conduct due diligence, and word will get back to VCs and the like if your codebase and development habits are unprofessional.

Of course, there are a lot of other things that define a pro, but they all come back to discipline.

The other key ingredient of a professional developer? **Humility**.

That’s right — know when to say “I don’t know.” It’s okay to say it more often than you may think. No one’s expected to know everything.

Recognize that your peers and co-workers may have something valuable to contribute — don’t be afraid of them. Remember that it’s all a learning process, and admitting mistakes and learning from them is more well regarded than pointing fingers at others and never fessing up to writing code that is bad, buggy, terminally broken, or incapable of handling even minor degrees of scale without a room full of hardware to run it.

The most professional developers I know — the guys who really know what they’re doing — happen to be the ones who do the least amount of strutting around shooting off to the masses about how professional they are. Funny how that is.

To tie this all back into [the discussion](http://www.arachna.com/roller/page/spidaman/20060206#php_best_practices_frameworks_and) [at hand](http://fuzzyblog.com/archives/2006/02/15/responding-to-ian-on-php/), I’ll say:

Ian, you sound like an excellent developer. Haven’t had the chance to meet you yet, but I look forward to the day we eventually do meet. Take a look at [SimpleTest](http://www.pearified.com/index.php?package=SimpleTest) as well as [PHPUnit2](http://www.phpunit.de/wiki/Main_Page) and plain ‘ol .phpt — I’ve found [SimpleTest](http://www.pearified.com/index.php?package=SimpleTest) to be invaluable in the Feedster frontend re-write. Also, in your framework exploration, be sure to check out [SOLAR](http://solarphp.com/); it’s very well done, and E\_STRICT compliant.

Also, I don’t think it’s necessary for any of us PHP developers to define Best Practices — after all, the basics of Best Practices should apply to any language. Shelves full of books have been written on the subject; we shouldn’t have to re-define it. Those who want to practice Best Practices will take the time to read that stuff and apply it to PHP development.

Since some will consider this post to be an arrogant one, I’ll be the first to tell you that I *am* faking it. I’m a New York University-trained actor who’s a “crossover guy” — I started programming freelance when I didn’t want to wait tables in Los Angeles.

I have never had formal development training, and I lieu of such training, I have devoured books like [Code Complete](http://www.amazon.com/gp/product/0735619670/qid=1140118886/102-8321279-7114549), [Rapid Development](http://www.amazon.com/gp/product/1556159005/102-8321279-7114549) and [Software Requirements](http://www.amazon.com/gp/product/0735618798/102-8321279-7114549). Only within the past two years have I added version control to my daily routine, and I finally got around to adding unit testing to the mix regularly about six months ago.

Becoming a true pro is an evolutionary process, and even though I’ve been developing since 1995 and using PHP(/FI) since 1997’s 2.0b6, I’ve still got a long way to go and a lot more to learn.

Until I get there, I’m doing what actors do: “living the role” of a professional developer and focusing on walking the walk as closely as possible. I hope that what comes out of each day of refining my “performance” as a pro results in incrementally better code. Take stock at the end of each day, and try to improve the walk the next day.

[![Technorati](http://killersoft.com/randomstrings/wp-content/plugins/UltimateTagWarrior/technoratiicon.jpg)](http://www.technorati.com/tag/) [development](http://www.technorati.com/tag/development), [feedster](http://www.technorati.com/tag/feedster), [ookles](http://www.technorati.com/tag/ookles), [php4](http://www.technorati.com/tag/php4), [php5](http://www.technorati.com/tag/php5), [technorati](http://www.technorati.com/tag/technorati), [work](http://www.technorati.com/tag/work)
