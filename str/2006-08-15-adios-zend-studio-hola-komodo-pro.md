# Adios, Zend Studio. Hola, Komodo Pro!

While my posts have been few and far between over the last several months, anyone who’s been following along knows I’ve been wrestling with the decision over my preferred development environment.

A long time BBEdit user, I bit the bullet and (mostly) [switched to Zend Studio](http://killersoft.com/randomstrings/2005/11/10/switching-pains-bbedit-8-to-zend-studio-5/) back in November 2005. I was frustrated by [Zend Studio’s clunky Subversion handling](http://killersoft.com/randomstrings/2005/11/12/subversion-wrapper-for-zend-studio-5/), but within a few weeks was willing to put up with that for Zend Studio’s great debugging environment and intimate knowledge of PHP that helps speed coding along on a line-by-line basis.

Then, I got a MacBook Pro in February. A 2.0Ghz Intel-based MacBook Pro with 2GB of RAM went a long way to helping me get over how slow Zend Studio is on OS X. But, the switch to an Intel Mac broke Zend Studio’s great debugger. Whoops! There went at least half of why I was using Zend Studio in the first place.

I emailed Zend about this issue several times over the following months, and when it hadn’t been resolved by July, I chose not to renew my Zend Studio license. I toyed with [switching to TextMate](http://killersoft.com/randomstrings/2006/06/20/textmate-and-phpdoc-comment-blocks/) for awhile, but it just didn’t have the oomph I had gotten accustomed to with Zend Studio.

I’m sure there’s a valid reason that Zend hasn’t shipped an update for Zend Studio that would allow Zend Studio Server’s debugger extension work on Intel Macs in the 8 months since they first hit the market … but for the life of me, I just can’t imagine what it is.

Enter [Komodo Pro](http://www.activestate.com/Products/Komodo/). Komodo Pro 3 has supported Intel Macs for months. (Still no word from Zend on this issue.) Its debugging environment is based on the robust [Xdebug extension](http://xdebug.org/).

What’s especially nice is that while Komodo bundles Xdebug, I’m fully able to compile my own, along with my own PHP. In fact, I’m working through building [Mashery](http://www.mashery.com/) on a MacBook Pro, PHP 5.2.0RC1 running as a fast-cgi under [Lighttpd](http://www.lighttpd.net/) with Xdebug 2.0beta6, all through [Komodo Pro 4.0alpha3](http://www.activestate.com/store/beta/register.plex?id=komodo). While I wouldn’t necessarily recommend that *exact* setup to everyone, it’s working out very, very well for me. (The Live Folder/Live Import feature in 4.0 alpha3 is critical for Zend Studio switchers.)

That’s what it boils down to: Komodo Pro lets me work the way I want to, with the tools (and versions of those tools) I want to use. Zend Studio, on the other hand, does not.
