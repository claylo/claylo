# Monitor PHP Extension Releases with Y! Pipes

Like many of my fellow geeks, I've found a few moments to play around
with Yahoo Pipes over the last couple of days.

The first pipe I've created and published is the [PHP Extension
Monitor](https://web.archive.org/web/20080229031955/http://pipes.yahoo.com/pipes/HL5Rzu232xG9k5oJuJqdmw/).
It's an aggregated feed that pulls in release information on several
cool extensions that aren't announced in the PECL feed, such as
[Suhosin](https://web.archive.org/web/20080229031955/http://www.hardened-php.net/),
[XCache](https://web.archive.org/web/20080229031955/http://trac.lighttpd.net/xcache/)
and
[DBXML](https://web.archive.org/web/20080229031955/http://www.oracle.com/technology/products/berkeley-db/xml/index.html).

Since I use all of these extensions at Mashery, I thought it would be
nice to have an aggregated feed to keep track of those releases along
with the PECL releases feed.

So, please [check it
out](https://web.archive.org/web/20080229031955/http://pipes.yahoo.com/pipes/HL5Rzu232xG9k5oJuJqdmw/).
Hope it's helpful to someone else out there. Please make a note in the
comments if you'd like to see additional cool extensions added to the
feed.

My thoughts on the creation process: Pipes is a cool tool, and a very
impressive bit of UI scripting. As [Aaron
noted](https://web.archive.org/web/20080229031955/http://www.wormus.com/aaron/stories/2007/02/08/on-y-pipes.html),
the actual generation of the feed is quite slow. I hope they have some
kind of caching in place. :smile:

If the PHP Extension Monitor feed is a popular idea, but Pipes proves to
be too slow to handle it, let me know and I'll create a more traditional
back-end aggregator for it.

### Original Post Comments

On Friday, February 9th, 2007 at 11:29 pm, Aaron Wormus said:

> Nice job  it’s a pity that the only thing that has been done with pipes is fairly basic rss aggregation.
>
> Anything I’ve done in pipes I could have done in half the time using PHP - especially counting the times I spent restarting my browser.
