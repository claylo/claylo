# Ohloh Reports May Paint an Inaccurate Picture

Through no fault of the [Ohloh](http://ohloh.net/) tool itself — it can only report on what it’s told, after all — the reports that Ohloh generates should not be considered The Gospel.

After cruising the site for a few minutes today, and oooohing and aaahing at like many others have been, I popped open a project I’d never heard of: [PHPSurveyor](http://ohloh.net/projects/270).

Ohloh speculates that PHPSurveyor has 731,822 lines of code, and would cost approximately $11 million dollars to reproduce.

Wow.

Upon closer inspection of the history of the project on Ohloh, it appears that the Ohloh crawler is looking at [the root of the PHPSurveyor SVN repository](https://svn.sourceforge.net/svnroot/phpsurveyor/), which happens to contain all their releases **AND** their current working trunk.

I’m sure that Ohloh is using a somewhat different algorithm, but just to get a ballpark comparison, I ran [recursive wc -l](http://www.cs.uleth.ca/~holzmann/C/shells/shell_book_blinn/Wc), on an ’svn export’ of the full repository, excluding image files (.gif/.jpg/.png/.svg) and .txt files:

|  |  |
| --- | --- |
| Lines | Path |
| 1,098,024 | / (full repository) |
| 288,618 | /source |
| 273,544 | /source, minus a directory called “rewrite” |
| **195,198** | /source/phpsurveyor, minus 3rd party ADODB, phpMailer and PEAR libs |

That’s quite a difference. I can’t be sure, but in Ohloh-speak I think I just saved someone over $9 million dollars. 😊

---

# [No Responses to “Ohloh Reports May Paint an Inaccurate Picture”](#comments)

[Feed for this Entry](http://killersoft.com/randomstrings/2006/10/25/ohloh-reports-may-paint-an-inaccurate-picture/feed/)
[Trackback Address](http://killersoft.com/randomstrings/2006/10/25/ohloh-reports-may-paint-an-inaccurate-picture/trackback/ "Copy this URI to trackback this entry.")- No Comments

Posting Your Comment  
Please Wait

Post a ReplyThere was an error with your comment, please try again.

Your Name:

Email:

Website:

Comments:

 

﻿

# What is Killersoft?

Killersoft is a small web development firm located in Fremont, California, founded by web developer and author Clay Loveless.

﻿

# Greatest Hits

* [Walk the Walk Before Talking the Talk](http://www.killersoft.com/randomstrings/2006/02/16/walk-the-walk-before-talking-the-talk/)
* [Web Developer Toolbar for IE6](http://www.killersoft.com/randomstrings/2006/03/24/web-developer-toolbar-for-internet-exploder-6/)
* [On Guest Blogging](http://www.killersoft.com/randomstrings/2006/04/17/on-guest-blogging/)

[![ZCE](/web/20061112193858im_/http://killersoft.com/images/layout/zce1000-small.gif)](http://www.zend.com/store/education/certification/authenticate.php?ClientCandidateID=ZEND001429&RegistrationID=212039840)

© 2006 Killersoft, All Rights Reserved - [Designed by Matt Brett](http://mattbrett.com/ "Visit Matt Brett's site")

![](/web/20061112193858im_/http://killersoft.com/images/layout/spacer.gif)
