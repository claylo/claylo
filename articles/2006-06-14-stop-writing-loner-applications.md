# Stop Writing Loner Applications

It’s not all about you and your killer app. I’m talking to you, Mr. Super-Duper Web Application Developer Guy.

After nearly a decade in web application development, I continue to be dumbfounded by how many applications are built and released by the open-source community that apparently believe that they’ll be the only complex, user-database application I’ll will want to run.

These are the loner applications.

Forum applications. Blog platforms. CMS systems. Ecommerce engines. Wikis. Which website that hopes to draw any kind of crowd needs only ONE of these? Even “Web 0.5″ sites needed two or three of these kinds of tools. These days, many sites need them all, plus custom layers on top of them that provide some uniqueness to justify the existence of the site in the first place.

So why are loner applications still being built, as if they’re the only horse in the stable? Alleged “Best of Breed” apps, such as [WordPress](http://www.wordpress.org/), [Movable Type](http://www.sixapart.com/movabletype/), [ZenCart](http://www.zencart.com/), [FUDforum](http://fudforum.org/), [Vanilla](http://getvanilla.com/), [Trac](http://trac.edgewall.com/), [MediaWiki](http://www.mediawiki.org/wiki/MediaWiki) … the list goes on and on. Insert your favorite application that relies on user registration here \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.

In nearly every case, these loners have been built with no apparent concern for the fact that the person or company involved may already have a database of users, or that one of the other applications may be installed alongside it. Hard to believe, but true.

The result is that the guys in the trenches trying to put together a cohesive whole have to spend a great deal of their cycles writing and maintaining “bridge code” to allow site visitors to register and authenticate against all of the chosen applications at once. Mr. Super-Duper Web Application Developer Guy knows little of this dilemma, because he’s spending his time coding the kitchen sink into his Super-Duper Web Application instead of worrying about interoperability.

Here’s a wake-up call, guys: your awesome \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ application probably isn’t the only thing I’m going to install. The killer feature that will make me choose your app over the other guy’s is not “[widget support](http://wordpress.org/development/2006/03/widgets-plugin/),” but some built-in comprehension that things like authentication, registration, and even user profiles/preferences may be housed in another application.

It’s not that I don’t love you and your masterpiece. It’s just that I may already be using something else that I’m stuck with or committed to, and would rather authenticate against that instead.

Some of the applications I’ve mentioned are starting to think this way … Trac, for example, has [pluggable modules](http://projects.edgewall.com/trac/wiki/TracPluggableModules) on the way that may allow alternative authentication. It’s a start.

This is especially important to consider in today’s Web Services/Remote Application world. The “other application” that houses the user data for authentication and preferences may not be hosted on the same server, or on the same platform, or written in the same language.

So please: drop the loner schtick and start tuning your applications to be part of a collection of tools.
