# Build a Cool App

My post yesterday struck a chord that many others were also hearing, as
[Andrei's
post](https://web.archive.org/web/20080229205522/http://www.gravitonic.com/blog/archives/000359.html)
and the comments that followed it indicate.

Potential developers of new frameworks, take note: Your announcement
**will** be followed by wholesale eyeball-rolling.

Stephan and the Stubbles folks
[feel](https://web.archive.org/web/20080229205522/http://stubbles.org/archives/4-Pavlov.html)
that my reaction and Andrei's are somehow knee-jerk, and that if we
really looked at their framework, we'd feel differently. Perhaps this is
true, perhaps it's not. I can say that if I spent time browsing code for
every new framework that came out, I'd never have time for anything else
(what with three n00bs in the last couple of days).

What I always wonder when these things come out is: why are people
pouring their talents and energies into frameworks that will probably
never have a critical mass **instead of** building something cool with
existing frameworks?

Yes, it's hard to build applications. There's all that unpleasant user
interface work and design considerations to think about, and you
actually need a relatively complete package before you can
announce/release something. But, given the landscape of PHP frameworks,
there is no less work to building the next "everybody uses it because
it's so damn handy" application than there is to building the framework
that everyone will eventually use.

Seriously.

Build a cool app. Forget about your own personal stamp on the framework
world; you missed the boat on that one. But, if you want to make a mark,
the world is wide open for new and cool applications. Pick an existing
framework, start building your app, and contribute fixes back to that
framework's community as you find shortcomings in your needs for your
app.

OR, if you're not an application guy, and only feel comfortable with the
plumbing, then pick a framework that has a shortcoming and fix that
shortcoming. If you're afraid that your work will not be accepted, or
that there will be too many
[contribution](https://web.archive.org/web/20080229205522/http://framework.zend.com/wiki/display/ZFPROP/Contributor+License+Agreement)
[political
hurdles](https://web.archive.org/web/20080229205522/http://framework.zend.com/wiki/display/ZFPROP/Home#Home-ContributionProcess),
then pick another framework (there are plenty to choose from, after
all).

We need better tools, and better applications. We **DO NOT** need more
clean slate starts.

### Original Post Comments

On Saturday, February 17th, 2007 at 10:27 am, Stephan Schmidt said:

> Again, I can only speak for Stubbles:
>
> 1. We do not need the “critical mass” of developers and users of our framework. It’s mainly needed and developed at the company we work at (1&1 Internet Ltd.).
>
> 2. We are not only building a framework, we are building applications as well. Those applications are what we get paid for.
>
> We neither want to use the framework, nor the apps built with it, to earn our reputation in the PHP community, we just do it for the money.
>
> We just released the code because to us it does not matter, if we develop in a public or private Subversion repository. If no one uses it (instead of our own developers), that’s fine to use, too.
>
> BTW: I used existing “frameworks” for years (e.g. PEAR) and even worked on one of the first code repositories for PHP (PAT), but now we felt, that there was no framework out there that fulfilled all of our needs. We still will use non-Stubbles packages for our apps, as long as we think that the solutions fit our needs, but for parts some parts of the applications and the general infrastructure, we could not find any matching framework.

On Saturday, February 17th, 2007 at 11:14 am, Clay said:

> So find the framework that is closest to filling your needs, and bridge the gap.
>
> Contribute to existing communities instead of rolling your own. Stubbles is nothing other than a result of the NIH Syndrome.
>
> Sorry, Stephan — I’m not trying to bust on you personally. Given the selection of frameworks to choose from, there is just no defensible position for not using one of the dozens of other frameworks out there and contributing your changes/patches/fixes/extensions back to that community. That’s the open source principle, is it not?

On Saturday, February 17th, 2007 at 11:50 am, Stephan Schmidt said:

> I’ll not comment on the NIH syndrome anymore, as II have been contributing to the open source community for years and think this discussion will not lead us anywhere.
>
> A slightly off-topic comment: If you would use an existing blog instead of building your own, this wouldn’t happen:
> http://killersoft.com/randomstrings/randomstrings/page/2/
>
> So why are you building a new blog instead of supplying patches to Serendipity or WordPress?

On Saturday, February 17th, 2007 at 12:14 pm, Clay said:

> Stephan, it’s your contributions to the open source community over the years that started this whole discussion. I just don’t understand why you wouldn’t contribute to/extend one of the excellent existing frameworks.
>
> As far as your decision to try to make this a personal attack on my development skills and decision-making, I find that disappointing and out of character for you.
>
> I would advise, however, that you view source on applications before you publicly attack them — if you had, you’d see that I’m running the same poorly architected, buggy WordPress 2.1 as many others.
>
> I do appreciate the bug report, though.
>
> I apparently should also clarify my position on apps versus frameworks: as I said above, there are too many frameworks, and not enough apps.
>
> There are no great open source publishing apps built on top of the new PHP 5 frameworks. I am working on a variety of applications based on Solar that will challenge existing applications with code architecture that don’t adhere to “best practices” for development.
>
> After all, why contribute to a framework if you’re not going to build something useful with it?
>
> But again, thanks for the WordPress bug report. I’ll pass it along.

On Saturday, February 17th, 2007 at 1:25 pm, Stephan Schmidt said:

> My apologies for mistaking the WordPress bug for an incomplete blog application of yours. I did not intend to attach you personally. I just thought, this 404 message was one of yours to remind you to finally finish the blog. I was not referring to your development skills. How should I, without reading any code from you. If you misunderstood my intentions, I apologize for this.
>
> I don’t understand, why my contributions to open source software started this discussion? Could you please elaborate this topic?
>
> Back in 2000, when I started the PAT packages (that ware open sourced 2001), there was nothing to contribute to. Then later I contributed to PEAR and have been very active. But there is stuff I want to experiment or work with, that cannot be easily included in existing frameworks (try adding a new templating engine to PEAR, or drastically change the way objects are created in Solar or any other framework) and thus, we started a new project.
> Maybe our ideas fail, but then we at least tried them. But if we succeed with some ideas, they might influence some existing frameworks and be “backported” to them.
>
> Since we have PEAR as the “official” repository,  you could have asked Paul M. Jones, ezSystems or Zend, why they had to implement their own framework instead of improving PEAR. But they had good reasons not to work with PEAR. You surely must be happy, that Paul started Solar, as you are using it now. Solar provides form handling, but this could have done with patForms or HTML_QuickForm, both have been available for a very long time. Solar even seems to have its own DocBlock parser, although the PhpDoc team is constantly looking for contributors. So, who gets to choose, whether we have enough frameworks or not? If you discourage people from starting new projects, you might discourage the one person, that starts a framework that will revolutionize the way we develop. And that would be very sad, wouldn’t it?
>
> And before anybody else feels bashed by this entry: I’m just referring to Solar as an example, as you mentioned it in your last comment. I’m sure that a lot of other frameworks also provide new implementations for the same problem instead of supporting existing solutions.
>
> Still, I’d be very happy if you could explain, why my contributions started this discussion (as long it’s not Stubbles, you are talking about, as I committed approx. 5% of the code to this project).

On Saturday, February 17th, 2007 at 5:03 pm, Rich Buggy said:

> Why do framework developers all feel the need to provide wrappers around PHP functions or use template engines instead of PHP? I’m still waiting for someone to show me a fast, lean framework. Until then I’ll continue to use my own tiny framework.

On Saturday, February 17th, 2007 at 9:39 pm, Clay said:

> @Stephan: I probably wasn’t clear enough when I said that your contributions to open source software “started this whole discussion.” What I really meant was that this “branch” of the discussion started my comments relating to you.
>
> And even then, I’m not trying to single you out personally; I’d have similar thoughts regarding anyone who’d made a commitment to contributing to open source projects.
>
> I am just surprised that regular open source contributors cannot (or could not) find an existing framework that was “close enough” to work with. I don’t mean to say that people with a history of contributing to open source projects can never do anything _but_ contribute to other projects (instead of starting their own). However, I figure that those with a history of contributing are perhaps more likely to find some shoulders to stand on before starting from scratch. I may be completely wrong in that assumption.
> Deciding whether to contribute to something or start from scratch is a difficult decision. Sometimes you don’t like the people involved in a particular project, other times you may not like the code and feel it will take too long (or be too insulting) to attempt the kind of re-factoring a project would need to suit your goals/needs.
>
> So, it’s not how much you (Stephan-you) contributed to Stubbles, but I’m just surprised that there wasn’t anything out there “close enough” to build upon.
>
> Regarding PEAR/Solar/ezSystems/Zend, I believe that there are several things going on in those examples. A growing number of experienced PHP developers seem to be breaking ranks from PEAR package use due to how mired PEAR is in PHP 4 support. Since Paul M. Jones’ stated goals for Solar were a E_STRICT compliant PHP 5 framework with a common configuration format shared by all classes, it’s easy to see why PEAR packages were not a fit for Solar use. (It’s also worth mentioning that Paul DID try a PEAR-based approach to a framework — see Yawp.)
>
> Zend? My understanding is that they also wanted a PHP 5-only framework, and also felt it important to call it “Zend (something).” It’s too bad they made the latter decision, in my opinion … They could have chosen to support Solar, a project with near-identical goals that pre-dated Zend Framework by a year … but they clearly wanted to control the project completely, as evidenced by their CLA, among other things.
>
> When a major requirement is “I/We Must Have the Final Say,” the obvious choice is you’ve got to roll your own. However, when you look at well designed frameworks like Solar and Zend Framework, you can still have the final say in your use of it, since you can override/extend as needed.
>
> Perhaps there would be less eyeball-rolling in the community if new frameworks stated explicitly what they do differently that simply could not possibly be done with any existing solution. Even if this isn’t published on the project site, offer to explain it to those who are interested.
>
> Of course, even as I suggest that, I realize that there are far too many frameworks out there to evaluate each one carefully before making the “contribute or build from scratch” decision. However, there are five or so leaders of the pack that have been around longer than the rest.
>
> Coming back to the original topic of this comment: what about Stephan and his history of open source contributions? I think it would be very interesting to hear what Stubbles ideas you’re referring to that could not have been implemented in any of the top 5 or so frameworks. if nothing else, it would be informative to those frameworks you considered.
>
> Since all the frameworks you likely considered tout themselves as being highly extensible and flexible, they would no doubt be interested to know why any particular idea/approach simply isn’t possible under their roofs.
>
> @Rich: Plenty of frameworks claim to be fast and lean. Paul M. Jones, author of Solar, spent a considerable amount of time over the holidays benchmarking some of the more popular frameworks. He’s published his results, as well as his benchmarking code.
>
> As for wrappers around PHP functions, and templating engines other than PHP itself, I don’t think you’ll find either of those in Solar or Zend Framework, and while I can’t speak at length about CakePHP, it uses straight PHP for templating as well.

On Sunday, February 18th, 2007 at 3:11 am, Stephan Schmidt said:

> As Frank mentioned in our blog, we will write an entry, to explain, why we develop Stubbles. As this explanation should be well thought, it may take some time.
>
> All I can say now, is that we have an existing Java framework and in some cases we have to implement things the same way in PHP, to make it easier to for (frontend-)developers to switch between languages. If adopted an existing framework, this would definitely be no valid argument to change the way, that things are done and would probably lead to endless discussions.
>
> And still, I’m not working on my own, although I showed that I can work well with others. This time I’m just working well with people that are not part of the PHP community, but employees of the company I’m working at. Some of them are not even PHP developers, but XSL/Javascript or even Java developers. We are building our work on top of existing code and standards, but those are part of 1&1 and not the OS PHP community. So to some extend, we are doing what we think we should be.

On Sunday, February 18th, 2007 at 6:51 am, Stephan Schmidt said:

> The last sentence in my comment should read: “So to some extend, we are doing what you think we should be.”
>
> Stephan

On Friday, July 13th, 2007 at 3:59 pm, Stanis Shramko said:

> What for me, in 2002 there were no good frameworks at all. So, the friends of mine and me decided to develop something at our own. Now there are a lot of good frames but our approach seems more logical for me than some others.
>
> If we’re unable to find something of interest but we need it, who should implement it?
