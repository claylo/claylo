# Let There Be Good Looking Applications

Let There Be Good Looking ApplicationsIn another small step toward putting a slick application together completely out PEAR-installable components, I put up a PEAR package of the [Tango Desktop Project](http://tango-project.org/) icons today.

I’m looking forward to putting these to use in a few things, and I’ll be interested to hear if anyone else finds PEAR-installable icons handy as well.

[Grab a copy of the icons:](http://www.pearified.com/index.php?package=Icons_Tango)

```
$ pear channel-discover pearified.com
```

```
$ pear install pearified/Icons_Tango
```

That will create a directory in /[path to pear]/Pearified/Icons/Tango. You can then access the icons a number of ways in your applications:

* Create a loader.php script that outputs a PNG header and then does a readfile() on the image you want.
* Create a symbolic link in your web document root to the Pearified/Icons/Tango directory, then use regular HTML img tags to use the icons.
* Or, if you’re using Apache and control your config files, use an Alias directive in your VirtualHost container (sorry, .htaccess files don’t allow the Alias directive) to point to the location of the Pearified/Icons/Tango directory.

Why not use the Role\_Web package? I thought about packaging them that way, and may switch to that at some point in the future. If you’d prefer the Role\_Web method of packging these icons, please speak up in the comments.
