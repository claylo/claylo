# Change Your Life with Version Control: An Introduction to Subversion

*Imagine a world in which you work harmoniously with other developers, never fearing that your code changes will overwrite theirs—or worse, that their changes will overwrite yours. A world where all of your modifications are backed up, and where you can always perform an "undo" operation when your code tweaks take a turn for the worse. Sound like a dream come true? Welcome to the Subversion-managed life.*

---

If you're not already using a version control system to manage your work, you may be one of many developers with a nagging "Man, I need to take time to figure that out" thought in the back of your mind. The one that pops to the forefront every time you see a line like the following, in an open-source project you're hacking on:

```
$Id: index.php 3128 2005-05-01 22:02:26Z clay $
```

Or, you may be a developer who's been working for a while without using a version control system, and you think "Hey, I work alone and I get by just fine without that stuff. What's the big deal?"

Change to workflow management is something that simply gives a lot of developers the shivers. No one wants to time testing out new ways to work—if you're already overworked, adding new steps to your workflow is just going to make everything take longer, right?

In this article we'll explore why taking the time to integrate version control into your work is worth the effort. In doing so, I'll introduce you to Subversion, a version control tool that is rapidly gaining favor with the open source development community.

## What is Version Control?

Version control is the process of keeping track of changes that are made by one or more parties, to a collection of files.

The art of software development is often made up of a series of exploratory events. You may know the requirements of the project or task you're working on—you know what you ultimately want to achieve—but getting from the beginning of a project to the end may require some (or *lots* of) trial-and-error style exploration. Version control tools are designed to help you keep track of the small, incremental changes you make along the way, similar to the idea of leaving a trail of breadcrumbs behind you as you venture deep into the forest of your project. By making use of version control, you can always find your way back if you realize that you've gotten lost.

Beyond keeping a basic record of changes, version control systems also provide mechanisms to merge changes made by more than one person to the same file or files. It is this ability to manage *concurrent* changes by members of development teams that the magic of version control really starts to kick in.

## Why You Need Version Control

You may be like me—I resisted the idea of version control when I first learned about it. I started off working in web development as a self-taught independent contractor, and since I worked alone, I figured I did not need to use a tool that was designed to help teams of programmers work together. I had a little system of creating a copy of a file before I veered off in a radical new direction, and I knew that I could always go back to that saved version of the file if didn't like where the new direction took me.

There are a few problems with this approach. First, what if you have made some changes in your "new direction" version that you want to keep, but you want to discard some changes? It's hard to remember exactly everything you changed so that you can carry only the changes you want back to your saved backup.

Next, what if you forget to make enough backup copies? Often, the exploration of a new approach to solving the programming problem will involve a number of small branches that may seem too small to be worth saving entire backup copies of the files you're working on. The sense of security you had when you made your original backup copy is eroded when you realize you didn't have just one branch from the main development, but you've really made several branches.

How about the bugs you introduced during all that fiddling around with the code? Before I got hooked on version control, I spent many long hours backtracking through multiple-undo operations, hoping that my editor wouldn't crash while I was stepping backwards through changes to find where I'd goofed up.

On the positive side, what if what you're working on becomes The Next Big Thing? When other developers line up to help, they will want to be able to see how you got to the current state of the project, and they will want an easy way to help you out by contributing patches to your code. How do you manage all the helpful input and integrate it into your work?

All of these issues can be addressed effectively by integrating a version control regimen into your workflow.

## Introducing Subversion, Heir Apparent to CVS

The Concurrent Versions System (CVS) is the de-facto standard version control tool. CVS, which has been around in various incarnations since the late 1980s, evolved from a series of UNIX shell scripts written to solve the problem of merging the work of multiple developers working together on a project into a central copy of the work that combined the input from each developer into a unified whole. The container that holds this central copy, as well as the history of changes to it, is known as a *repository*.

Like many solutions that evolve organically as the problem definition clarifies itself, CVS was patched and extended in order to meet new requirements as they came up. Features such as secure network connections to a repository server and versioning of binary files (such as images), in CVS, behave almost as though they were afterthoughts, and require the user of the system to remember special incantations in order to use those features properly.

After more than a decade of CVS use as the primary solution to the version control problem, the requirements of a complete version control workflow were well-known. In early 2000, a group of developers began work on a new version control system called Subversion, whose primary goal was re-imagining CVS' solution to the version control concept from the ground up, without any of CVS' quirks and design flaws.

Subversion can handle several aspects of versioning a project that CVS cannot; for example:

- Subversion tracks changes to directories and files; CVS can only track changes to files.
- Subversion allows flexible access and authentication policies over HTTP, HTTPS, and SSH.
- Subversion can track metadata properties related to the files and directories in a repository, in addition to changes to the files and directories themselves.
- Subversion tracks revisions as they relate to an entire project, not only as they relate to individual files within a project.

While there are many version control tools available today, whose implementations improve upon the concepts pioneered by CVS, Subversion is the only free, open source solution designed specifically to duplicate CVS' use in a development workflow.

## Conceptual Overview: What are we trying to do?

There are a variety of ways to take advantage of Subversion: command-line tools, GUI applications, integrated solutions that provide access to Subversion as part of a larger application, and web-based Subversion interfaces. We'll cover all of those methods, but before we dive into the details of basic svn usage, let's describe what we're really trying to accomplish with Subversion, and version control in general.

First, we need a place to store the code for the project we'll be tracking with version control—that place is called the repository. A Subversion repository can be created locally on your development machine, on your development server, or it can be provided for you as part of Subversion repository hosting service.

Some version control novices are confused by the concept of the repository, since they are used to only having one copy of the code for their projects stored in a local directory where they make edits, and a web server that the files are uploaded to when edits are complete. If you find the repository idea confusing, you're not alone; I found the concept of an invisible, all-knowing repository the most difficult to get a grasp on when I first began working with version control tools.

Think of the repository as a refrigerator—you store a pizza in the fridge, take it out and "work on it" by eating a slice or two, and then put the modified pizza back in the fridge. A repository is similar in that you keep your code in the repository, and you `checkout` a copy of the code to work on it. (A repository isn't exactly the same as a refrigerator—the repository keeps copies of all previous versions of the project, enabling you to go back to any specific revision if you need to. I wish my fridge let me do that with pizza!)

If you are not working on a project that already lives in a Subversion repository, you will first need to `import` the project that you want to track revisions on. If you're starting work on a new project, it's a good idea to import an initial directory structure for the project to establish a starting point.

The checked-out copy of the code is called a *working copy*. Just like when you're working on a non-version controlled project, you often need to do any or all of the following tasks while making edits: make changes to one or more lines of code in files already in the project, `add` new files to the project, `copy` files from one directory to another, `move` files around, and possibly even `delete` files or directories entirely.

When you're finished making changes to your working copy, you tell the repository about the changes you've made by performing a `commit` operation. Occasionally you may find that you need to stop working on the project for awhile to handle something else before you've been able to commit your changes. When you get back to working on the project (hours, or even days or weeks later), you'll probably want to take a moment to figure out the `status` of the changes you made during the last session to you can determine exactly where you left off.

If you will be working on a project with others, or even just making custom modifications to an open source project that is housed in a Subversion repository, you will want to make sure that your working copy is current before each editing session. To do that, you will need to perform an `update` operation, which will pull down anything that has changed from the repository since your last editing session.

When updating your working copy on a project that is being worked on by multiple developers, you may find that someone else has made changes to files that you've been editing. In that event, you'll need to *merge* the changes you've made with the changes the other developers working on the project have made. Sometimes the changes you've each made will be to different sections of the same file, in which case merging is an easy task. There are times, however, when you find that you've each been working on the same section. In those instances, you've got a *conflict* that you will need to *resolve*.

If the series of events I've described above sounds somewhat similar to your work flow process, now, integrating Subversion into your routine will be a piece of cake.

## Basic Subversion Setup & Workflow

If you've followed me this far, we only have a few small steps to take to get you up and running using Subversion to manage your projects.

As I mentioned there are several Subversion-aware tools available to make it easy to manage your work, in a repository. All tools are based on the fundamental svn command-line tool, so for now we will focus on converting the conceptual narrative above into usable commands with svn.

First, let's assume that we've got Subversion installed on our example.com server at `https://svn.example.com/`. The main Subversion website offers detailed installation instructions, as well as links to several pre-packaged installers for a wide variety of platforms. I will also assume (and suggest!) that you have the latest stable version installed, Subversion 1.1.

You also need to consider the access methods you want to allow to your repository. Repositories, and directories within repositories, may be controlled with an access control list (ACL). You can use an ACL to set whether projects are read-only, publicly readable but require authentication for writing, or totally private, where read and write operations require valid authentication. Authentication can be secured via SSL or SSH, or "non-secured," meaning that authentication credentials can be required, but will be transmitted in plaintext over the network. Server-based repositories can be set up using any or all of the following methods:

- **svn://**: A non-secured protocol which does not require anything other than the standard Subversion installation. Network access is facilitated via the svnserve daemon.
- **svn+ssh://**: Secured protocol which uses system accounts for authentication, and upon successful login, spawns an svnserve process as the authenticated user.
- **http://**: A non-secured access method that utilizes HTTP for communication. Requires Apache2 with Subversion modules installed.
- **https://**: Secured access method using HTTP and SSL. Requires Apache2 with Subversion and mod_ssl modules installed, plus an SSL certificate. (May be a self-signed certificate or a certificate issued by any SSL vendor. Try out a GoDaddy.com SSL cert if you feel your project might meet the requirements for their free open source SSL certificate.)

If you choose either the http:// or https:// method, make sure you set your repository's permissions so that the directory is owned by the Apache2 user.

Begin by creating a repository, if you do not already have a repository available:

```bash
$ svnadmin create —fs-type fsfs /var/lib/svn
```

The `svnadmin create` command does not generate any output upon success. The options we've passed to the command specify a filesystem-only type of file storage, and the path where we'd like the repository to live on the server. Two file storage types are available for a repository: BerkeleyDB and the filesystem type. As of the upcoming Subversion 1.2, fsfs is the default and recommended type of repository storage, so if you're starting a new repository it's a good idea to get started with what will be the standard, going forward. Finally, please modify the repository path of /var/lib/svn as needed to fit your environment.

Now, let's create a test project with an empty file structure.

```bash
$ mkdir tmpdir && cd tmpdir
$ mkdir -p testproj/trunk testproj/branches testproj/tags
$ svn import . https://svn.example.com —user exampleuser \
    —password examplepass \
    —message "Project starter layout"
$ cd .. && rm –R tmpdir
```

The empty directory structure that you've given to your test project follows the standard layout suggested by the Subversion documentation. This layout is generally adhered to by most Subversion users.

The purpose of the directories in an empty project structure break down like this:

- **trunk**: The main thread of current development in the project.
- **branches**: Experimental development branches that may eventually be merged into the project trunk.
- **tags**: Directory for saving, or "tagging", copies of the project at a particular point in time, such as version releases, site launch milestones, etc.

So now you've got a shell for your project in the repository. The next thing to do is to check out the project into your working area, where you can add files, test your changes, and generally, just hack away.

```bash
$ svn checkout https://svn.example.com/testproj \
    —user exampleuser —password examplepass \
    ~/sandbox/testproj
A    testproj/branches
A    testproj/tags
A    testproj/trunk
—
Checked out revision 1.
```

What just happened? You checked out your test project from the repository, and saved a working copy of the project in your "sandbox" development area. The letter A in front of each directory indicates that the directory was added to your working copy. If you are actually using an https://-based repository, the above output would also include a prompt for acceptance of the remote server's certificate credentials.

After seeing the first svn command with username and password arguments, you may be wondering if you'll have to use those arguments with every command. The good news is: No! While the above example shows the username and password as part of the command, by default Subversion only requires this on the first command. Subversion will attempt to cache the credentials used to access the repository, and will use them transparently for future operations. (Note: the svn+ssh:// method does not attempt to cache credentials.)

If you are using a shared machine, you may be concerned about the security risks of credentials caching. Cached credentials are stored in ~/.svn/auth (or %APPDATA%/Subversion/auth if you're using Windows) in a permission-protected state which allows only the user who issued the command that cached the credentials to read them. In other words, other users on the machine will not be able to access your credentials—just make sure you log out of your session before leaving the machine unattended!

If you are still concerned about the security of Subversion's default credentials-caching behavior, you can disable authentication caching for single commands by adding the `—no-auth-cache` option, or by disabling caching permanently in the Subversion run-time config file that lives alongside the auth/ directory mentioned above. See the Subversion manual's section on "Client Credentials Caching" for more details.

With a working copy of our test project checked out in our "sandbox," it's time to get started—working just like you normally would. Using the testproj/trunk directory, create files as needed, add directories as needed, and conduct your development as usual. The notion of version control comes back into play when you're ready to commit a version of what you're working on.

In our test project, let's assume that we've copied in a couple of standard files that you may find in many projects: README, COPYING and INSTALL. Put those files in your trunk directory, either by creating new files or copying them in from another project. Now, let's see what we've got:

```bash
$ svn status
?       README
?       COPYING
?       INSTALL
```

What that tells you is that Subversion sees that there are some files in a version-controlled directory (your working copy) that it doesn't know about. To tell Subversion that you want to track revisions on these files, you need to formally add them to your test project.

```bash
$ svn add README
A       README
$ svn add COPYING
A       COPYING
$ svn add INSTALL
A       INSTALL
```

Now Subversion knows about these three files, and will display an A instead of a question mark if you perform another `svn status` operation. Now that your working copy knows that these files should be tracked, you can commit them to the repository.

```bash
$ svn commit –m "Adding basic info & doc files to project"
Sending        README
Sending        COPYING
Sending        INSTALL
Transmitting file data ...
Committed revision 2.
```

Note that since we were committing all of the files that we added, we did not need to specify what files we were committing in the `svn commit` command. The message "Adding basic info & doc files to project" will be recorded in the repository log along with your username and a timestamp. *Please* make a habit of writing something informative in your commit messages—you never know if the project you're tinkering with will become the next phpMyAdmin. If that happens, other developers will appreciate your efforts in documenting your changes. A sentence or two will do! Don't be lazy and commit a series of changes with a message stating "fixed some bugs"—that kind of message won't help you or anyone else if and when it's time to backtrack through the log.

How do you know when to commit a version, or revision? That's a good question, and one whose answer may vary on a case-by-case basis. For example, you may be learning version control techniques to become a participating member of a multi-developer project. If that is the case, find out from the project leaders what their repository commit policy is, if any. A good rule of thumb is to commit a revision when you get to a point where you feel you would not like to have to re-do what you've done, much like the decision you make on when to hit Save in your editor. Another good rule is to try to commit changes that actually work. If you feel like you must (or should) commit a revision that you know is broken in some way, make a point to note what is broken clearly in your commit message.

If you find that you need to commit some of the files that have changed in your current working copy, but you're not ready to commit them all—or if it does not make sense to commit all current changes under one commit message—then you need the `—targets` command option. This option allows you to reference a file that lists out all of the files in the working copy that should be included in the current commit operation, and therefore tagged with that commit message.

A handy way to make use of this feature is to keep an alias to a file called svn, which resides in the home directory, somewhere close at hand (I keep mine in the Mac OS X dock—adjust this suggestion to your operating system of choice). That way, you can quickly open the ~/svn file and add a list of files that you want to commit. Using this technique, every `—targets` commit can look like this:

```bash
$ svn —targets=~/svn –m "Added new maintainer to package."
```

Create files and directories, add them to the project with `svn add`, and commit. Repeat. Make changes, commit with useful log messages, repeat. Keep up this routine, and it will pay dividends later. A few things that strict adherence to this allow you to do:

**Look back on the long, strange trip.** It's a fairly common practice to build ChangeLogs out of repository commit messages. Detailed commit messages, combined with `svn log`, can give you a nice overview of the progression of a project's codebase.

**How'd we get here?** Dig back into the past to find out what specific changes were made to a file to get to the current state. For example, `svn diff -r10 index.php` will compare the current revision (also known as HEAD) of index.php with revision 10 of index.php.

**Abort, Abort!** `svn revert` can let you back out of all changes you've made since the last revision was committed.

## Working and Playing Well with Others

So far, the techniques we've covered outline the benefits and basic usage of Subversion for an individual. The main points to know when using Subversion as part of a development team are how to merge changes and resolve conflicts, and the importance of `svn update`.

When working with a group, it is important to remember to run `svn update` in your working copy at the start of every editing session. (If you're working on a particularly active project, it may make sense to run it several times during a single editing session.) `svn update` updates your working copy with the current revisions in the repository.

Often, running `svn update` will be a smooth operation. The command will put out a list of changed files that it has updated in your working copy, new files that have been added, and possibly files or directories that have been deleted. Subversion will note these changes in your working copy by listing the related files, prefixed with U, A or D, respectively.

However, on occasion `svn update` will pull changes from the repository that affect files that you have been editing in your working copy. In these instances, those files will be denoted with a G, for merged, or a C, for conflict. When you see a G, it means that Subversion noticed that you'd been making changes to the same file, but your changes did not overlap the changes made to the version in the repository, so Subversion automatically merged your changes in with the new revision.

In the event of a conflict, that means you and another developer were working on the same section of code within a file. To bring the world back into harmonious balance, you will need to manually review the differences between your edits and those of your colleague. Subversion tries to make this process easier by creating a few extra files in your working copy.

Let's say that you've been making changes to the opening paragraph of your project's README document, while another developer has been making changes to the same section. When you run your `svn update` command, something like the following will occur:

```bash
$ svn update
C       README
Updated to revision 3.
$ ls -1
README
README.mine
README.r2
README.r3
```

The three additional files alongside README are called *conflict markers*. At this point, you have three choices:

1. Manually compare README.mine with README.r3, and if necessary, README.r2. README.r3, in this example, is the revision you just pulled from the repository. README.mine reflects your current changes, and README.r2 reflects how README looked before any editing started by either party. When you're done manually examining the files, make edits to README, as appropriate.

2. Copy one of the three conflict markers over README.

3. Run `svn revert README` to discard your changes.

After completing one of the above three choices, you should then run `svn resolve` to let Subversion know that you feel you've taken care of the conflict.

At the risk of stating the obvious, it is important to realize that when Subversion successfully merges your working copy file with a changed file from the repository, what you're left with may very well *not* be a functional file. In my (very) early days of understanding version control concepts, I wondered "How does the merge operation know if the changes from the repository should be merged with my changes?" The answer, of course, is that the tool doesn't know—it's just a tool, not an omniscient guardian angel. All that happens when Subversion automatically and "successfully" merges your working copy with the newly retrieved version of a file is that Subversion feels comfortable that the lines that another developer changed in the file are not in the immediate vicinity of the lines *you* are in the middle of changing.

Hence, the guideline is to make sure you pay close attention what's taken place whenever you perform an `svn update` operation, and double-check any merges or conflicts that the output of the command warns you about.

## Fun for the Whole Team

When working as part of a diverse group that may include more than developers—or if you, yourself, prefer to stay away from command-line tools—there are a wide range of tools that have Subversion support built-in. A short and by no means complete list:

- **BBEdit**: Version 8.1 of the venerable Mac editor offers built-in Subversion support. http://barebones.com/
- **SVN for Macromedia Dreamweaver**: Third-party plugin available in free and commercial versions. Currently Windows-only. http://grafxsoftware.com/
- **psvn.el**: Subversion interface for emacs, for the hard-core among us. http://xsteve.nit.at/prg/vc_svn/
- **TortiseSVN**: Standalone Windows GUI client for Subversion. http://tortisesvn.tigris.org/
- **SCPlugin**: Contextual Menu plugin for Mac OS X that adds Subversion support to the Mac OS X Finder. http://scplugin.tigris.org/

While it may be a challenge, it is worthwhile to try to integrate Subversion usage into an entire team, including copywriters, graphic designers, and yes, even marketing folks. A historical record of an entire project (not just the code portion) in one place is an extremely valuable resource if you can get buy-in on the concept from an entire team.

## Leveraging Subversion in Your Projects

So, what's all this got to do with PHP, seeing as this is a PHP magazine?

From the beginning, Subversion has offered very tight integration with Perl, Python and Java. Subversion also comes with C libraries that can add Subversion functionality in applications such as those mentioned in the previous section. Until recently, Subversion integration with PHP has been lacking.

There are two PHP packages available to make it easier to take advantage of a Subversion repository in your projects.

**PEAR::VersionControl_SVN**: An OOP wrapper for the svn command. http://pear.php.net/package/VersionControl_SVN

**ext_svn**: A PECL extension for Subversion. Uses the svn client libraries to add native Subversion functionality to PHP. Available from CVS only as of this writing. http://cvs.php.net/pecl/svn/

In addition to basic repository browsing functionality (See the cool FlexySvn for an example of that: http://newweb.akbkhome.com/svn.php), these packages can be used to add robust version control capability to web applications.

For example, imagine a message board templating system that allows forum administrators to tweak templates with a browser interface, but saves those changes to a server-side working copy of the forum's distributed template set. The web interface could also trigger periodic `svn update` commands to a publicly-readable repository to merge distribution-level template changes with customized templates.

A number of CMS applications offer some form of internal versioning, but none of those custom-built versioning systems allows external editing of those versioned documents. With the integration of Subversion capability, a CMS application could be extended to allow content editing from within its interface, or via Subversion, with changes accessed again through a server-side, PHP application-triggered repository checkout. (Note: `svn export` might be a better command to trigger in that type of scenario.)

The VersionControl_SVN package is well documented with examples for each method it offers—please see the online documentation at the PEAR website for more ideas on how to integrate Subversion into your applications.

## Start Tracking Changes Today!

I know that adding version control to your working process can be a chore that does not seem like it is worth the effort. However, I hope that I've shed some light on what benefits await you if you take the time to integrate Subversion into your work.

Don't waste time getting on the bandwagon—put down this magazine and jump online and Google for "Subversion hosting." There are a number of services that offer relatively inexpensive repository hosting, and many of those offer free trial periods. Try out what you've learned, immediately, without getting bogged down in the details of setting up your own repository server.

Good luck, and don't forget to commit your work, often!

---

*Clay Loveless has been developing web applications with PHP since 1997's PHP/FI 2.0b6. A New York University-trained actor, Clay now works from California as an independent internet solutions consultant under the name Killersoft (http://www.killersoft.com). He is also actively involved in maintaining Pearified.com. Clay is a husband, father of a very cool one year old son, and a dedicated Boston Celtics fan. Reach Clay via clay@killersoft.com.*
