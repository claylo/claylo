# PHP Did Not Cause Facebook Code Leakage

[Facebook](https://web.archive.org/web/20080224092722/http://www.facebook.com/)
experienced a technical glitch over the weekend. The nature of the
glitch was that the [source
code](https://web.archive.org/web/20080224092722/http://facebooksecrets.blogspot.com/)
for the Facebook homepage was displayed instead of the result of the
execution of that source code. Widespread news of the glitch first broke
in [this TechCrunch
article](https://web.archive.org/web/20080224092722/http://www.techcrunch.com/2007/08/11/facebook-source-code-leaked/)
by TechCrunch writer and OmniDrive founder [Nik
Cubrilovic](https://web.archive.org/web/20080224092722/http://www.nik.com.au/).

I agree with Cubrilovic that the inadvertent delivery of source code
instead of the result of that source code is certainly a horrific
situation, with potentially serious ramifications for any company that
experiences such a problem on a large scale basis.

That a company like Facebook, currently a [hot
ticket](https://web.archive.org/web/20080224092722/http://google.com/trends?q=facebook)
for searches, articles and blog posts, would experience this kind of
problem is noteworthy.

Unfortunately, the updates appended to the article imply that PHP is
somehow responsible for this leakage. In the first article update,
Cubrilovic states:

> It seems that the cause was apache and mod_php sending back
> un-interpreted source code as opposed to output, due to either a
> server misconfiguration or high load (this is a known issue).

On the first of Cubrilovic's suggested causes, server misconfiguration:
well, duh.

Of course servers will behave strangely if they are misconfigured. The
world of a system administrator is one of details, and when it comes to
managing load balanced web servers for an extremely high-traffic
destination like Facebook, it's a world of a large number of details.
Miss one of them and things will predictably start breaking in
unpredictable ways.

On Cubrilovic's second allegation: It's "a known issue" that PHP barfs
out source code under high load? I've been writing PHP code for some
very, very high traffic websites for over 10 years, and this is the
first I've heard of this.

Surely we in the PHP community would have heard from someone like
[Rasmus](https://web.archive.org/web/20080224092722/http://lerdorf.com/bio.php)
if PHP were prone to puking source at a high load. As an infrastructure
architect at Yahoo!, Rasmus has likely seen how PHP behaves under load
levels most of us only fantasize about. If PHP coders were building
their applications on a platform pre-destined for [Twitter-like
failures](https://web.archive.org/web/20080224092722/http://www.radicalbehavior.com/5-question-interview-with-twitter-developer-alex-payne/),
no doubt we'd have heard about it by now.

Can anyone provide links to articles or posts indicating that PHP will
eject application source under a heavy load?

It's infinitely more likely that Facebook's problems were caused by a
system administrator breaking some web server configuration (possibly
not even PHP-specific configuration), or a new installation of a mod_php
build that hadn't been tested properly in a non-production environment.

Cubrilovic's second amendment to his article links to an article on his
own blog, [Learning from Facebook: Preventing PHP
Leakage](https://web.archive.org/web/20080224092722/http://www.nik.com.au/archives/2007/08/11/learning-from-facebook-preventing-php-leakage/).

Given the likelihood of this issue's cause being server
misconfiguration, it is disturbing that Cubrilovic's first tip for
avoiding this kind of problem is to install and correctly configure the
powerful and complex Apache module
[mod_security](https://web.archive.org/web/20080224092722/http://www.modsecurity.org/).
After all, if the a sysadmin can't get Apache and PHP configured
properly, how likely is it that they'll be able to get *two* modules
configured properly?

The rest of Cubrilovic's tips also relate largely to web server
configuration, such as making certain files inaccessible from direct
requests.

The disappointing part of the
[FUD](https://web.archive.org/web/20080224092722/http://en.wikipedia.org/wiki/Fear%2C_uncertainty_and_doubt)
that Cubriolovic is spreading is that anything *more* than decent
release practices are necessary to address and avoid the problem
Facebook experienced.

I can only imagine why Cubrilovic has invested this weekend in
undermining people's faith in PHP's reliability under heavy load. What I
can tell you, though, is this:

> **PHP doesn't cause website problems and inadvertent code leaks.
> People making mistakes while using PHP and other powerful tools do.**

However, that *fact* isn't worthy of two articles, so perhaps that's why
Cubrilovic went with the PHP-as-boogeyman-that-must-be-defended-against
approach instead.

What's the take-away from all this? Servers are powerful, and can be
complicated. Tread carefully. *Don't roll untested configurations of web
servers and related modules out on production without testing them in an
identical staging environment.*

Know what you're doing, and do it carefully.

### Original Post Comments

On Sunday, August 12th, 2007 at 8:51 am, Antony Dovgal said:

> It’s similar to saying that 2×2 = 5 under high load.
> Nonsense.

On Sunday, August 12th, 2007 at 3:28 pm, McLion said:

> Hmm…maybe a clue…  php was not running on apache or at least not as mod_php… fastcgi is for heavyload sites better as for memory consumation…
>
> When the web server displays the source? Easy…when php dies… you’re running X PHP instances (fastcgi interface), something happens (not stable PHP installation), it dies…bum, you’re serving sources

On Monday, August 13th, 2007 at 8:53 am, Mike Malone said:

> When I read that article I thought the exact same thing. I’ve had single CPU servers running with a load average over 50 (it wasn’t pretty). Responses lagged like hell, but I’ve never seen mod_php barf up source code.
>
> It’s much, much more likely that it was a configuration error. And, while proper configuration is always a must, I have to agree that keeping source code outside the root directory is kind of a “best practice”. I took a look at the facebook source, and it looks like most of their “libraries” are not in their wwwroot dir, but the index page held far too much code. It would be wise for them to move their index to another directory and have a simple index.php that includes it… or something.

On Monday, August 13th, 2007 at 11:39 am, Morgan said:

> Even worse is this post on Scott Gilbertson’s blog at Wired.com.
> Quote: “PHP is notorious for just this sort of thing — serving code as text — but there are ways you prevent it from happening on your own site.”

On Tuesday, August 14th, 2007 at 2:08 am, Mike Seth said:

> The allegation that PHP is responsible for leaking source code in any fashion is, indeed, false. For a short period of time, there was an issue with the PHP interpreter crashing and being unable to recognize the PHP source code when a certain bug was triggered which has caused the source to be leaked. If I remember correctly, something to do with invalid regular expression. However, this does not happen anymore, last time I’ve seen it was maybe three years ago if not more, and this can not be used to blame PHP.
>
> Of course, the histrionic nonsense spewed out by the big folks is rooted in their despise of PHP in general, for its open, chaotic nature of development which yields historical lack of naming conventions (just look at the string API or the array API), and for its disregard to the “enterprise” needs, which are basically pretty frontends and some sort of money-backed guarantee that the stuff works.
>
> PHP has gone a long way from being just a scripting language for rendering HTML. We now have decent support for Unicode and more to come in PHP6, we have PDO which is intended to replace intermediary hacky database APIs, we have a great OO system that suits the purposes of web development, and a rich base of written user-level code which can be reused by application developers. Commercial quality frameworks are being grown as we speak, the documentation is being improved (and PHP is known to have the single best documentation in the FOSS world - which, ironically, no one ever bothers to read), there’s a thriving community that gives a lot of support to newcomers and many many many businesses from small web studios to giants such as Yahoo rely on PHP for mission critical tasks.
>
> So, the whining can be safely ignored.

On Tuesday, August 14th, 2007 at 6:55 am, Chase Saunders said:

> You’re missing the point.  This could not have happened in a compiled language.  All interpreted language, including PHP, JavaScript, Ruby, etc. are less secure from a corporate IT perspective for this reason.

On Tuesday, August 14th, 2007 at 7:12 am, Clay said:

> @Chase - whose point is that, other than yours, in this discussion?
>
> Not even Cubrilovic is arguing for a compiled language in either of his posts.
>
> No, the point, quite clearly, is that PHP is more than adequately secure for web applications when deployed by system administrators who dot their ‘i’s and cross their ‘t’s.
>
> Cubrilovic’s assertion that PHP failed in some way in the Facebook scenario is just complete and utter bullshit. That’s the point.
