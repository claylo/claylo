# A Call for Feedback

After reviewing my Zend Download Server logs today for [Pearified.com](http://pearified.com/), I was surprised to see that there have been several hundred downloads of the Pearified JavaScript and other “front end” packages.

While the numbers are a little strange when you take dependencies into consideration, here’s what I’ve served so far:

```
JavaScript_Prototype        354
```

```
JavaScript_Scriptaculous    431
```

```
JavaScript_Behaviour        164
```

```
phpMyAdmin                  131
```

```
Role_Web                    169
```

Assuming that some people are downloading all of the packages, and some are downloading them for multiple sites, etc, I figure there are at least 80-100 people who are following (and maybe even using) these packages.

So, silent users, what do you think of this idea?

I’m starting to believe that PEAR-installed “front end” packages should go into a `/webpear` directory in a site’s DocumentRoot, with channel packages going in subdirectories of that `/webpear` directory.

Currently, the [Role\_Web](http://www.pearified.com/index.php?package=Role_Web) package allows the DocumentRoot to be set anywhere. That will not change; what I’m thinking of is a “socially-enforced” guideline rather than a programatically-enforced one.

There may be good reasons at times to have front end packages that are installed outside of the `/webpear` directory, but in general I’m suggesting that packages which use the Role\_Web role set their ‘baseinstalldir’ value to `/webpear/[channel]/[whatever is appropriate]`.

For example: One of today’s Icons\_Tango files would then become available at:

```
http://www.example.com/webpear/Pearified/Icons/Tango/48x48/categories/applications-games.png
```

The biggest benefit is that applications/packages that want to introduce dependencies on these files would know exactly where to find them, and how to call them without relying on any fancy footwork or additional configuration.

What do you think, silent ones? This would eliminate the need to symlink, import files via loaders, or set up Apache aliases for these files. The downside is that it would create some long paths within the `/webpear` directory … but, if you don’t like that, you could always do a symlink or alias anyway, just like you have to now.
