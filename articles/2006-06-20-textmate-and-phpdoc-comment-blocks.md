# TextMate and phpDoc Comment Blocks

I’ve been checking out [TextMate](http://macromates.com/) for the last few days, and have been enjoying it. I’ve been a [BBEdit](http://www.barebones.com/) user for a decade, and despite my switch to [Zend Studio](http://www.zend.com/products/zend_studio) [last fall](http://www.killersoft.com/randomstrings/2005/11/10/switching-pains-bbedit-8-to-zend-studio-5/) for the bulk of my PHP development, I still find myself going to plain text editors for little tweaks, or less formal “hack it out” efforts. Up until this past weekend, BBEdit has been my go-to editor for these smaller projects.

The verdict is still out on TextMate, but I’m really liking certain aspects of it.

To you loyal BBEdit users who are no doubt thinking “Traitor!” — as I myself thought several times as I’ve followed the TextMate hype over the last six months or so — I **did** spend a good chunk of the wee hours on Sunday going through BBEdit features such as Glossaries and File Groups in an effort to mimic some TextMate capabilities. After all, BBEdit is a very powerful editor — surely all this TextMate hocus-pocus can be achieved with BBEdit as well?

I gave up on that after a couple of hours. I don’t know that I’m giving up on BBEdit at this point, but TextMate has earned “Keep In Dock” status. I’m sure I’ll continue upgrading BBEdit as new versions come out, at least for awhile. However, TextMate’s understanding of what I want as a developer is just too keen to ignore.

There are a few things that I’ve grown very accustomed to as a Zend Studio user over the past several months. One of those is typing

```
/**
```

in a PHP document and having a full phpDocumentor docblock appear magically, with the cursor insertion point set on the first line of the comment area.

That’s cool. A similar effect can be achieved in TextMate by typing

```
doc_cp
```

… followed by a TAB stroke.

However, where Zend Studio trumps TextMate related to phpDoc docblocks is in the handling of multi-line comments. If you’re already in a comment block and you hit enter for a new line of the comment, Zend Studio will automatically add proper docblock formatting to the new line. For example:

```
/**
```

```
 * Here's a comment
```

```
 **/
```

In Zend Studio, a return/enter keystroke after the “t” in “comment” will result in:

```
/**
```

```
 * Here's a comment
```

```
 *
```

```
 **/
```

The cursor is inserted directly under the “H”, with one space after the asterisk on the new line. This is a great feature, as it allows you to worry about what you’re writing in the comment, rather than worrying about the formatting of the comment block.

By default, TextMate doesn’t follow suit. Yes, you can insert some auto-formatted comment blocks. As I mentioned earlier,

```
doc_cp
```

followed by a TAB results in this block:

```
/**
```

```
 * undocumented class
```

```
 *
```

```
 * @package default
```

```
 * @author Clay Loveless
```

```
 **/
```

As a bonus, the words “undocumented class” are selected in the resulting block, so that I can begin typing immediately — those words are removed and replaced by what I’m typing. Again, that’s cool. However, a new line kills the joy of this feature. If my comment is “Killersoft\_Foo — A class for all that and a bag of chips” followed by a new line, I’ll wind up with this:

```
/**
```

```
 * Killersoft_Foo -- A class for all that and a bag of chips
```

```

```

```
 * @package default
```

```
 * @author Clay Loveless
```

```
 **/
```

That’s **not** cool. Once you’re used to Zend Studio’s behavior in this situation, it’s hard to go back to life without it.

Fortunately, TextMate has some very powerful scripting capabilities. Execute the following steps (assuming TextMate 1.5.2 or later), and you can get the same auto-comment-formatting magic in TextMate.

* **Open the Bundle Editor.** From the **Bundles** menu, select **Bundle Editor** => **Show Bundle Editor**.
* **Create a new Snippet.** At the bottom of the list of bundles, shortcuts, etc. on the left side of the **Bundle Editor** dialog, there’s an interface element with a plus sign and a “down arrow.” Choose **New Snippet** from there.
* **Enter Regular Expression.** Clear out the default snippet hint text (which starts with “Syntax Summary”), and enter the following code:

```
${TM_CURRENT_LINE/(.**/$)|.*?(/*(?!.**/)).*|.*/(?1:
```

```
:
```

```
(?2: )* )/}
```

(line breaks are intentional, and necessary. [See txt-only version.](http://www.killersoft.com/randomstrings/wp-content/uploads/2006/06/CommentNewline.txt))

* **Assign Activation and Scope.** Choose “Key Equivalent” as the Activation method. Click in the input box and hit your “Return” key. In the “Scope Selector” field, type

  ```
  source.php comment.block
  ```
* **Clean up.** The snippet should be in a bundle referenced by your name. For example, mine is under “Clay Loveless’s Bundle.” Change the name of the bundle to something more meaningful than “untitled”, such as “Comment Newline”.

You should now get properly formatted new lines in your PHP comment blocks, just like Zend Studio. Enjoy!

Thanks to [Paul M. Jones](http://paul-m-jones.com/) for suggesting that I take another look at TextMate. And, thanks to [Brad Choate](http://www.bradchoate.com/) for the cool blogging bundle that I used to publish this post directly from TextMate.

[![blogged from TextMate](http://www.killersoft.com/images/layout/bloggedfromTM.png)](http://macromates.com/)
