# RESTful Routing, LocationMatch, ForceType and SetHandler

For years I've been seeing articles about RESTful routing, and watching developers contort their code including route aware this and that. All these gyrations come with a performance penalty, not to mention a code maintenance cost. (More lines to maintain = more pain in the ass.)

There are a few brave souls who've bucked this trend and gone with the original tools designed for this job — mod_rewrite and the like.

What I haven't seen much that makes perfect sense to me is extension-free files with a ForceType or SetHandler directive applied to them.

I know examples with Apache and PHP show that I'm a geezer, but humor me anyway.

```apache
# for you mod_php5 fans
<VirtualHost *:80>
    # ...
    <LocationMatch "^/(foo|bar|baz)/.*$">
        ForceType application/x-httpd-php
    </LocationMatch>
</VirtualHost>

# for the PHP-FPM lovers
<VirtualHost *:80>
    # ...
    <LocationMatch "^/(foo|bar|baz)/.*$">
        SetHandler php-fpm
    </LocationMatch>
</VirtualHost>
```

In either case, you create a file called 'foo' (no extension) in your document root. In it, you put something like this:

How you'd do this with funky new stuff such as Lighty, Nginx, and node.js, I don't know exactly. I'm sure it's possible. But, it's an exercise for those of you fascinated by the shiny and the new.

The point is this: save your CPU cycles for the stuff that actually matters. Leave the easy stuff like routing where it belongs: outside your app.
