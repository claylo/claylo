# Quickie Trac Notes

Two quick notes for [Trac](http://trac.edgewall.com/) users out there:

* I banged out all 33 lines of my first Trac plugin last night. The [FlexJsPlugin](http://trac-hacks.org/wiki/FlexJsPlugin) allows Trac users to add JavaScript to the <head> block of their Trac-powered sites without needing to hack ClearSilver templates.
* For PHP source files to display in the Trac Browser with default PHP syntax highlighting colors, use this:

  ```
  /* trac php syntax highlighting */
  .code-block {
      line-height: 1em;
      font-family: Courier, monotype;
      font-size: 12px;
      }
  .h_question { color: #0000BB; } /* highlight.default */
  .hphp_commentline { color: #FF8000; } /* highlight.comment */
  .hphp_operator { color: #007700; } /* highlight.keyword */
  .hphp_word { color: #007700; } /* highlight.keyword */
  .hphp_default {}
  .hphp_variable { color: #0000BB; } /* highlight.default */
  .hphp_hstring { color: #DD0000; } /* highlight.string */
  .hphp_simplestring { color: #DD0000; } /* highlight.string */
  .h_tagunknown {}
  .h_default {}
  ```

Drop the CSS in your project’s site\_css.cs file and you’ll feel a little less like a stranger in a strange land. And while I haven’t started playing too much with what some easily customizable JavaScript can bring to a Trac project, I’m looking forward to experimenting. Trac is great, but for all its coolness, it’s lacking a bit in the area of today’s JavaScript coolness.
