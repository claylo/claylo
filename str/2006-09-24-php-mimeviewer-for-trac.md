# PHP MimeViewer for Trac

As John Herren pointed out in the comments to yesterday’s post, my suggestion for PHP syntax coloring wasn’t working for several versions of Trac.

After a little digging, it turned out that my CSS rules were based on the non-standard SilverCity highlighting output, rather than the newer and more common native PHP highlighting.

While reviewing the output from the native PHP highlighter, I noticed that Trac’s manipulation of the output from highlight\_string() isn’t quite right. The way things are now, as of Trac 0.10rc1, an intended multi-line docblock only has the first “/\*\*” highlighted as a comment … the rest of the docblock is highlighted as default PHP (the code-lang class).

I’ve been clamoring for good PHP syntax coloring output in Trac [for a long time](http://lists.edgewall.com/archive/trac/2005-April/002593.html). Rather than pass the buck and put this on the Trac team, I’ve released a little PHP-based shell script called [php\_mimeview](http://pearified.com/index.php?package=Tools_PHP_MimeView).

With php\_mimeview installed, simply update the [mimeviewer] config section of trac.ini in your Trac project to point php\_path to the full path location of php\_mimeview. With that script, plus these rules in your site\_css.cs template file:

```
.code-keyword { color: #007700; }
.code-lang { color: #0000BB; }
.code-comment { color: #FF8000; }
.code-string { color: #DD0000; }
```

… you’ll get what you’re probably used to seeing in syntax-highlighted PHP code.

Thanks to John Herren for the nudge to investigate this further.
