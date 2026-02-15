# PHP and JSON: Cut #987

## JSON Decoding in PHP 5.2.1 is Broken

As of PHP 5.2.1, `json_decode()` no longer follows [the published
standards](https://web.archive.org/web/20080317033522/http://www.ietf.org/rfc/rfc4627.txt)
for JSON-encoded texts.

Why not? For no reason other than the convenience of those ignorant of
JSON standards.

Prior to PHP 5.2.1, this:

`var_dump(json_decode('true'));`

resulted in:

`NULL`

As of PHP 5.2.1, it results in:

`bool(true)`

Nice and handy, perhaps ... but a blatant violation of JSON
specifications, since `'true'` **is not** a valid JSON encoded text.

## A little history

Back in August, I spent a lot of time with
[JSON](https://web.archive.org/web/20080317033522/http://www.json.org/).
I was working on adding
[Prototype](https://web.archive.org/web/20080317033522/http://www.prototypejs.com/)/[script.aculo.us](https://web.archive.org/web/20080317033522/http://script.aculo.us/)
support to the [Solar
Framework](https://web.archive.org/web/20080317033522/http://solarphp.com/),
and wanted a handy utility for passing options around in JavaScript with
JSON.

Rather than roll some new JSON interpreter, I chose to leverage the
[Services_JSON](https://web.archive.org/web/20080317033522/http://mike.teczno.com/JSON/JSON.phps)
package along with
[ext/json](https://web.archive.org/web/20080317033522/http://pecl.php.net/package/json)
to build a package that was compatible with ext/json, but usable for
those who did not have that extension installed. With compatibility
built in, developers could move application code back and forth between
systems without having to worry about whether or not the extension was
installed --- if it was, the application would benefit from the added
performance of a native extension. If it wasn't, everything should work
exactly the same way.

In the course of my research for the Solar_Json package, I learned a lot
about JSON and how it is supposed to behave.
[JSON.org](https://web.archive.org/web/20080317033522/http://www.json.org/)
is a spartan but complete resource about the format, and includes the
[JSON
Checker](https://web.archive.org/web/20080317033522/http://www.json.org/JSON_checker/)
and a comprehensive JSON test suite. There's also a link to [RFC
4627](https://web.archive.org/web/20080317033522/http://www.ietf.org/rfc/rfc4627.txt),
which details JSON's structure in a proposal for the formal
application/json media type.

While digging through all this JSON goodness, I came to appreciate
ext/json's strict adherence to JSON's format. The version of ext/json
bundled with PHP 5.2.0 (version 1.2.1) was right on the money in its
parsing, and by the time I was done, Solar_Json matched it every step of
the way. To ensure ext/json compatibility, I wrote [a series of unit
tests](https://web.archive.org/web/20080317033522/http://solarphp.com/svn/trunk/tests/Solar/JsonTest.php)
(26 in all) to ensure that Solar_Json's "pure PHP" implementation
matched ext/json's output *exactly*.

It was challenging, but it worked out well. The result was
[Solar_Json](https://web.archive.org/web/20080317033522/http://solarphp.com/svn/trunk/Solar/Json.php).

## JSON Bundled with PHP, Confusion Ensues

To my delight, ext/json was bundled with PHP 5.2.0, and enabled by
default. This was great news for PHP developers everywhere who are
working with rich applications that need to exchange a lot of data with
JavaScript.

All was good, for awhile.

*(Yesterday, [Paul M.
Jones](https://web.archive.org/web/20080317033522/http://www.paul-m-jones.com/)
re-ran the JSON unit tests I'd written for Solar_Json using PHP 5.2.1 in
preparation for a new release of Solar. He mentioned that some of the
tests started failing, which sparked this discussion. Thanks, Paul!)*

Sure, a couple people (myself included) didn't fully understand JSON for
awhile. I even [opened (and quickly
closed)](https://web.archive.org/web/20080317033522/http://bugs.php.net/bug.php?id=38440)
a bug in the way I *thought* certain strings should be decoded by the
`json_decode()` function. [Others had the same
confusion](https://web.archive.org/web/20080317033522/http://bugs.php.net/bug.php?id=38680).

What's so confusing?

Well, the common thing that people want to do is something like this:

    var_dump(json_decode(true));
    // or
    var_dump(json_decode('true'));

The confusing part about these two snippets is that they both return
`NULL` instead of `true`. Based on the two bug reports
([#38440](https://web.archive.org/web/20080317033522/http://bugs.php.net/bug.php?id=38440)
and
[#38680](https://web.archive.org/web/20080317033522/http://bugs.php.net/bug.php?id=38680)),
it's common for people to expect the output to be a boolean `true` in
these examples.

However, if you understand JSON at all, you'll know that `NULL` is a
perfectly reasonable result, because `true` and `'true'` *are not valid
JSON texts*.

## Standard, Shmandard

Note that I said "if you understand JSON at all", you'll realize that
`NULL` is a perfectly reasonable result when attempting to decode an
invalid JSON text.

I should amend that: If you understand JSON at all ***and actually care
about standards and compatibility***, you'll realize that `NULL` is a
perfectly reasonable result of parsing an invalid JSON text.

Just like other formats, there's actually [a
specification](https://web.archive.org/web/20080317033522/http://www.ietf.org/rfc/rfc4627.txt)
that defines what is valid and what is not when it comes to JSON. [No,
really](https://web.archive.org/web/20080317033522/http://www.ietf.org/rfc/rfc4627.txt).

Section 2 of the standard states very plainly:

> A JSON text is a serialized object or array.
>
> `JSON-text = object / array`

Translated, that means that a valid JSON-text is either an object or an
array. It's *not* a string literal, an integer, a boolean. The list of
what a valid JSON-text can be is short. It can be an object. It can be
an array. It can be ... whoops, that's it. An object, an array, or it
just isn't JSON.

I mean, think about it: **J**ava**S**cript **O**bject **N**otation. Not
JavaScript Boolean Notation. Not JavaScript Assorted Stuff Notation.
Objects. Arrays thrown in because in JavaScript, they're basically the
same thing. Period, the end.

*DAMN, that's inconvenient,* you may be thinking. Yep, it is. But, it is
what it is. If you don't like it, submit an RFC to have it changed.
That's the way this crazy thing called the internet works.

Put another way: if you don't like it, you do not just [start making
things
up](https://web.archive.org/web/20080317033522/http://tinyurl.com/2lxsba).
Apparently, enough people unclear on the concept of JSON
[complained](https://web.archive.org/web/20080317033522/http://bugs.php.net/bug.php?id=38680)
about their lack of understanding that PHP now just does whatever it
wants with JSON. [Check this
out](https://web.archive.org/web/20080317033522/http://tinyurl.com/2lxsba)
for the details. (And to reiterate, I'm not knocking the people who
aren't clear about JSON. [I was one of them
too](https://web.archive.org/web/20080317033522/http://bugs.php.net/bug.php?id=38440),
up until I actually researched how JSON is *supposed* to behave.)

Imagine if the core team behind every language did that. Hey, if you
don't like the standards, just ignore them! We can explain it away with
documentation, right?

## Cut #987

The
[cavalier](https://web.archive.org/web/20080317033522/http://word.sc/cavalier "given to haughty disregard of others")
attitude taken by the PHP internals team on this issue is inexcusable.
Yep, *cavalier* --- a colleague who spoke to a member of the PHP
internals team about this change confirmed that the break from the JSON
spec is deliberate and intentional.

To make matters worse, the version number of ext/json did not change
between PHP 5.2.0 and PHP 5.2.1. In both releases, ext/json claims to be
at version 1.2.1, despite this significant change.

While some are lobbying to compile the definitive [business case for
PHP](https://web.archive.org/web/20080317033522/http://blog.stuartherbert.com/php/2007/02/08/what-does-the-business-case-for-php-need-to-cover/)
(and I even [piped in and
agreed](https://web.archive.org/web/20080317033522/http://tinyurl.com/2q7yoc)
that it was necessary), some PHP internals folks are effectively
shooting that effort in the foot by disregarding published standards.

I've spent the better part of the last two years defending my choice of
PHP 5 as my preferred language, first at
[Feedster](https://web.archive.org/web/20080317033522/http://www.feedster.com/),
now at
[Mashery](https://web.archive.org/web/20080317033522/http://www.mashery.com/).
With all the buzz about other languages these days, the case for PHP is
getting harder to make. Incidents like this will not make the case for
PHP any easier.

Is this a big flap over a little thing? That's certainly one way of
looking at it. I see this flagrant disregard for published specs as one
more cut toward [a death by a thousand
cuts](https://web.archive.org/web/20080317033522/http://en.wikipedia.org/wiki/Death_by_a_thousand_cuts).

Talented and notable developers are dropping PHP, or [seriously
considering](https://web.archive.org/web/20080317033522/http://lukewelling.com/2007/02/07/maybe-it-is-time-i-got-out-of-php/)
other languages. If PHP's next 10 years are to be as poignant as its
first, a significant attitude adjustment is required.

### Original Post Comments

On Wednesday, February 28th, 2007 at 9:21 am, IETF guy said:

> May I quote the IETF motto to you:
>
> Be conservative in what you generate, and liberal in what you accept.
>
> It appears the motto applies in this case.

On Wednesday, February 28th, 2007 at 9:25 am, Clay said:

> Fair enough. In that case, when will PHP’s XML extensions start accepting invalid XML? That’ll take a huge burden off some developers who don’t want to be bothered with getting XML formatting right.

On Wednesday, February 28th, 2007 at 9:45 am, Douglas Crockford said:

> JSON allows a decoder to decide what to do with badly formed texts, so long as it handles well formed texts correctly. JSON requires an encoder to only produce well formed JSON text.

On Wednesday, February 28th, 2007 at 9:46 am, Lukas said:

> Just wondering what reply you got when you filed a bug report?

On Wednesday, February 28th, 2007 at 9:48 am, Gaetano Giunta said:

> Well, I was thinking too about a blog post on this topic, but just bit my tongue and kept silent.
>
> In fact I am in favor of the library accepting decode(’true’), but this continuous, undocumented change in behavior is really unacceptable.
>
> Afaict, there is even an “earlier” json extension implementation, which was not based upon the json.c state machine code from json.org, and needless to say, API changed when the first switch was made.
>
> For the record, since I maintain another json lib (in the phpxmlrpc lib extras package), I did also code an api-compatibility layer on top of my code. It allows a coder to develop according to json-ext, and deploy upon phpxmlrpc (if it is eg. on a hosting with an old version of php).
> It now seems a (moderate) waste of time: keeping up with the apis is like follwoing the .doc standard…
>
> …this is really disappointing, especially since Zend has been touting “Enterprise” every day for one year or more.
> In the enterprise I work for, I had the chance to deloy a couple of months ago on php 4.0.4. Yes, you read it right. This is the kind of stability and backward compatibility hassle you have to confront in a real enterprise setting, but it looks like most of the dev team does not grok it…
>
> BTW: If you look at bugs.php.net, the behavior was changed to close a user bug. I know sometimes the developers really seem too harsh when closing the bug you entered as as ‘not an error’, but in this case it is really objectionable…
>
> PS: the xmlrpc extension also got quite a few fixes which really fixed the apis on a few corner cases, and the extension version never was updated. That does not look too complicate to do, does it?

On Wednesday, February 28th, 2007 at 9:51 am, Paul M. Jones said:

> @Lukas —  I “pre-filed” a bug report by email with the developer, who confirmed “it is not a bug” and was the intended behavior.

On Wednesday, February 28th, 2007 at 9:55 am, Clay said:

> @Douglas: Thanks for clarifying, that’s interesting — am I misreading RFC 4627?
>
> @Lukas: I didn’t get a response, because I closed the bug as ‘bogus’ — I’d determined that a NULL decoding was in fact what I should have gotten.
>
> @Gaetano: I think you’ve really hit on it. This issue is one in a long series of similar issues that make PHP’s behavior unreliable from one version to the next. Paul wrote about similar changes in PDO yesterday.

On Wednesday, February 28th, 2007 at 11:12 am, sapphirecat said:

> Try doing ‘var_dump(json_encode(true));’ sometime. Under php5.1.6 using json1.2.1 from PECL, at least, you’ll get ’string(4) “true”‘.
>
> To add to the confusion, the JavaScript code available from JSON.org happily accepts this, because of its use of eval() and the fact that ‘”true”‘ is valid JS syntax.
>
> The same really applies to _all_ types defined on json.org as “value”. So the blame isn’t 100% on PHP, but returning null on invalid JSON is fixing the wrong side of the problem.
>
> (The PECL extension is way out of date, by the way — see http://pecl.php.net/bugs/bug.php?id=9481. Nothing says “we don’t care” like neglecting your bugs for 3 months and counting.)

On Wednesday, February 28th, 2007 at 11:20 am, sapphirecat said:

> I said: “returning null on invalid JSON is fixing the wrong side of the problem.”
>
> Disregard that bit. I was (surprise) confused. The current state of the PHP parser, accepting any valid JSON value as a valid JSON text, meshes with what JSON.org is actually providing. If that’s not what they really intend, they need to make that a bit clearer. Like adding a “JSON Text = object || array” picture.

On Wednesday, February 28th, 2007 at 11:33 am, Clay said:

> Following up on my own comment, Section 4 of RFC 4627 does indeed say:
>
> A JSON parser MAY accept non-JSON forms or extensions.

On Wednesday, February 28th, 2007 at 4:10 pm, Scott MacVicar said:

> Section 5:
>
> A JSON generator produces JSON text.  The resulting text MUST strictly conform to the JSON grammar.

On Thursday, March 1st, 2007 at 6:08 am, Patrick Mueller said:

> RFC 4627 is not a standard.  From the document itself: “This memo provides information for the Internet community.  It does not specify an Internet standard of any kind.”
>
> It’s a bit ridiculous to only support objects and arrays with a decoder.  It would be easy enough to support number, string, boolean and null as well, and then the user of the API make a determination of whether the resultant type is appropriate.  Or add a flag to limit filter the result for you (returning an error condition).  As an earlier commented noted, the way of the web is: “be liberal in what you accept”.
>
> Of particular importance, it appears, given this blog entry,  that json_decode() function returns NULL on errors.  That’s pretty bad.  Since null is a perfectly valid value in JSON.  Even if this API never returns anything but array / object, it’s not immediately obvious, without looking at the doc that this would be the case.  Someone might do a quick test and find json_decode(’null’) returns NULL and think - woot!  it handles nulls!  When of course it doesn’t.  This would have been a good case for using an exception in the API.  Or returning an error object you could sniff for.  Or something.  NULL is just bad.

On Thursday, March 1st, 2007 at 7:07 am, Lukas said:

> @Lukas: I didn’t get a response, because I closed the bug as ‘bogus’ — I’d determined that a NULL decoding was in fact what I should have gotten.
>
> I dont understand that sentence. Didnt you say that it does not return NULL. So why did _you_ bogus your own bug?
>
> /me is confused

On Thursday, March 1st, 2007 at 7:19 am, Clay said:

> @Lukas: Please click on the link for the bug if you really want to know what happened with the initial bug report.
>
> I opened a bug related to PHP 5.2.0RC1 and the decoding issue. I then dug deeper into the way JSON should work (according to the JSON Checker test suite), and declared my bug bogus.
>
> Then PHP 5.2.1 came along, and the behavior changed. As I mentioned in the post, and Paul mentioned above, some pre-bug-filing conversations were had about this new behavior, and the internals team made this change intentionally. They do not consider the PHP 5.2.1 behavior to be buggy or broken.

On Thursday, March 1st, 2007 at 2:45 pm, Lukas said:

> Ah ok .. I get it now.
>
> However the “internals team” is not such a homogeneous bunch as you make it sound. Unfortunately decisions are often not thought through all the way. So if you feel strongly about something try to softly check up the issue with multiple people. It pays to know the internal cliques as well. Not easy to dig through from the outside unfortunately :-/
>
> Anyways usually php.net tries to follow standards. I do not know if there was any reaction so far from anyone with the necessary karma.
>
> One more thing to note: While single developers have the say over their respective pecl packages, this changes once the code goes into core, at which point more people can influence the direction of the code. So without being a JSON expert myself, try to make your case clear and I think you should have a good shot at getting this fixed for 5.2.2. Also please consider phpt’ing your unit tests to prevent such breakage in the future.

On Friday, March 2nd, 2007 at 1:28 am, Clay said:

> @Lukas: You make it sound so much like high school, complete with cliques and everything.
> This is a significant part of what’s wrong with PHP.
>
> The case is made quite clear by the JSON Checker and the test suite it provides. The suggestion that one has to suck up to the _right_ group to get PHP’s JSON extension to behave like the JSON Checker is very illuminating.

On Friday, March 2nd, 2007 at 12:57 pm, Lukas said:

> Unfortunately thats the reality. However, this reality still did not stop php from getting where it is today. If you tell me which developer you spoke to, I can also see what I can do. Feel free to email me.
