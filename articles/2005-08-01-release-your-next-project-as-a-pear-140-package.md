# Release Your Next Project as a PEAR 1.4.0 Package

*With the release of a stable PEAR 1.4.0 installer on the horizon, now is a good time to get familiar with the new features provided by PEAR 1.4.0 that can make distribution of your open source and proprietary libraries and applications easier than ever before.*

---

The upcoming release of PEAR 1.4.0 is an exciting milestone not only for PHP developers already familiar with PEAR, but for any PHP developer who is responsible for distributing applications on a large or small scale.

That's right, *applications*. While PEAR is an acronym for PHP Extension and Application Repository, the PEAR installer has never been particularly well suited for installing or maintaining installations of full-blown applications—until now. With the new features of PEAR 1.4.0, distributing full applications complete with dependency checking, customized environment modifications upon upgrades, and more are possible with just a little bit of extra work. As you'll see, the benefits of taking advantage of the new PEAR 1.4.0 distribution options far outweigh the extra work required.

## What's New in PEAR 1.4.0

There are several major new features in PEAR 1.4.0, the largest of which is support for channels. A PEAR channel is essentially a server that behaves just like the pear.php.net package distribution server, but can be served from another domain. That means that anyone may set up a PEAR channel server and serve PEAR-compatible packages. All an end-user needs to do is make their PEAR installation aware of the additional channels, and install from those channels, specifically.

In order to do this, let's get ready by updating your PEAR installation to the latest PEAR alpha that supports channels. Then we'll upgrade your PEAR installation, and add an example channel.

```bash
$ pear config-set preferred_state alpha
$ pear upgrade PEAR
$ pear channel-discover pearified.com
$ pear list -c pearified
```

What we should have now is an upgraded version of PEAR (1.4.0a12 at this writing), and a PEAR installation that is aware of two PEAR channels: the default PEAR channel at pear.php.net, and the new "Pearified" channel at pearified.com. Now, packages can be installed and maintained, including full dependency resolution, from both locations.

The next most significant feature of PEAR 1.4.0 is support for post-install scripts. A post-install script is run when called, like this:

```bash
$ pear run-scripts Example_Package
```

If `Example_Package` has defined post-install scripts, the PEAR installer will alert you following successful installation of the package. Scripts are never automatically executed for security reasons—you must explicitly run them using `pear run-scripts` as illustrated above.

A post-install script can perform just about any function you can imagine, provided that the user running the script has the proper permissions. Examples of good post-install script ideas are setting up default users of a permission system, installing or upgrading database schemas, or perhaps setting up a directory structure required by an application, complete with necessary permissions on those directories.

While there are several other enhancements in PEAR 1.4.0, the last one we'll discuss in this article is the very handy capability to manage remote PEAR installations over FTP. Frequently when doing contract work, I find that I'd like to use PEAR for an application, but since the client's web hosting account does not offer shell access, I'm forced to either use the web browser front-end to PEAR, or maintain the PEAR installation manually over FTP. With PEAR 1.4.0, it is now possible to specify a remote configuration file, which stores relevant install path information for the remote server, and then use the command-line PEAR command to synchronize your local PEAR installation with the remote PEAR installation.

For more details on all of PEAR 1.4.0's new features, review the PEAR documentation at http://pear.php.net/manual/en/guide-migrating.php. PEAR 1.4.0's primary developer, Greg Beaver, also maintains a weblog with several entries that discuss PEAR 1.4.0's architecture in detail. Visit Greg's blog at http://greg.chiaraquartet.net/categories/3-PEAR.

## Why PEAR packaging makes sense now

PHP is maturing quickly, and as it does, more and more packages that handle core application functionality (such as database abstraction, form validation and unit testing) are maturing as well. Naturally, it follows that more and more of the applications you build for internal or external distribution will depend on at least one of these supporting packages. (You *are* looking for ways not to re-invent the wheel, aren't you?)

Whenever an application becomes dependent upon a third-party library, the question then becomes how to stay on top of updates to the external library along with maintaining the application that depends on it. For a long time, the "solution" to this for many applications was simply to bundle a copy of the dependency with the application.

Unfortunately, the "bundle-the-dependency" solution does not work well in the event of critical updates to the dependency. For example, many applications depend on PEAR's XML-RPC package, versions up to and including 1.3 of which was discovered to contain some rather serious potential security holes on June 29, 2005. (See http://secunia.com/advisories/15852/ for details.) Following the discovery of these security holes, a scramble ensued by maintainers of applications dependent upon the PEAR::XML_RPC package to release updates containing a new bundled version of the patched package, PEAR::XML_RPC 1.3.1.

Since this initial scramble, PEAR::XML-RPC has had two more updates, but none of the applications that I use which depend on PEAR::XML-RPC have released updates to reflect the updated dependency—the current release as of this writing is 1.3.3, which contains two additional security and performance updates since version 1.3.1.

The answer? Convert your applications to PEAR installer-managed packages, and encourage the maintainers of the applications you use to do the same. With PEAR 1.4.0 managed packages, an application's dependencies can be updated as needed for security fixes and performance enhancements without the need to wait for an update release of the entire package in hopes that it will contain updated bundled dependencies as well.

A common counter-argument to relying on non-bundled dependencies is "What if a release for a dependency breaks backwards-compatibility?" If you or an application maintainer is particularly concerned about that possibility, it is trivial to specify limits on dependency versions in the definition of an application's package. (We'll explore how to do that a bit later.) Given that PEAR packages are not *supposed* to break backwards compatibility except on major version number increases, applications distributed as PEAR packages could avoid backwards-compatibility breakage concerns by specifying, for example, that any PEAR::XML_RPC package less than version 2.0 be acceptable for use by an application.

Given the increased usage of external library dependencies in PHP applications, it just makes sense to implement a structured package management system into your build-release protocol. PEAR 1.4.0 provides an excellent system for that purpose—and given that PEAR is installed by default in most PHP installations, soon PEAR 1.4.0 will make its way into a majority of PHP environments.

## Candidates for PEAR package management

What type of application or set of PHP scripts makes sense as a PEAR package? Thanks to PEAR 1.4.0, just about any type. Let's take a look at a short list of various scenarios where PEAR packaging would be a good idea.

**Library distribution**—This is how PEAR itself got started, so it makes sense that packaging a code library intended for re-use would be a good candidate for PEAR packaging.

**"Off-the-shelf" application distribution**—Whether an application is fully object-oriented or not, PEAR packaging makes sense primarily due to its intelligent handling of dependencies.

**Custom closed-source applications**—Even if the target installation is only a specific client's server, PEAR packaging can offer a tremendous advantage. Beyond the dependency management that is likely to be beneficial in this type of application, the code may also need to be deployed on a server that not everyone has access to. For example, consider that you're a consultant that is building an application for a client, yet due to security reasons you may not have access to install the application on the production server where it will ultimately reside. You can reduce the back-and-forth communication along the lines of "Oh yeah, make sure you have version 2.x of Package XYZ installed" by managing the distribution of your work with a PEAR package. All the person with clearance to install the application on the production server would need to do is:

```bash
$ pear upgrade -o consultant_channel/Custom_Application
```

in order to get their installation upgraded with whatever dependencies are required. In other words, you can control the installation environment much more with a PEAR-managed package, without having to bother the client with the details.

You may be wondering if there's a typo in this article—did I really just say that object-oriented code is not a requirement for a PEAR package? It's true that packages that are submitted to PEAR itself are generally required to have an OOP structure, however, that requirement does not extend to a package you may create to be compatible with the PEAR installer. The PEAR installer itself doesn't care whether the files in your package are OOP-based, procedural or a combination of the two. You can also install graphics, JavaScript files, and whatever else you need to with the PEAR installer. All that's required to do this is building your package in such a way that the installer knows what to do with each file in the distribution.

## Where PEAR 1.4.0 Installs Stuff

As soon as we start thinking about installing all kinds of applications, packages, and any other files we might consider including in a distributed application, the first thing you'll probably worry about is what file will get installed where. By default, PEAR 1.4.0 (and older versions as well) installs files in a set of pre-defined locations.

Every PEAR installation has a default base working directory, known conveniently as the "PEAR Directory". The location of the PEAR Directory varies from platform to platform—though it is often in `/usr/lib/php` (the default) or `/usr/share/php`. To find out what the PEAR Directory is set to in your PEAR installation, just use:

```bash
$ pear config-show
```

Check the output of the above command for "PEAR Directory", which is also known by its variable name of `php_dir`.

Within the PEAR Directory, there are a series of subdirectories:

- **data_dir**: The data directory, where any data files that are associated with a package are installed.
- **doc_dir**: The documentation directory, where documentation that accompanies a package is installed.
- **test_dir**: The tests directory, where package regression tests are installed.

With these install directories in mind, and assuming you need to package an application with "front end" capabilities (in other words, portions of your packaged application need to be directly accessible by a web browser), you can proceed with configuring your package to be installed three different ways: the "Change PEAR Config Each Time" method, the "PEAR Default + Aliasing" method, or the "PEAR Custom Roles" method. We'll explore each below.

## The "Change PEAR Config Each Time" Method

At first glance, it may make sense to just change PEAR's configuration based on the needs of your packaged application. Let's say that everything in your packaged application needs to be directly accessible via a web browser, so all files in the package need to be installed relative to the web site's document root (such as `/path/to/htdocs` or `/path/to/public_html`).

Easy enough—just run:

```bash
$ pear config-set php_dir /path/to/htdocs
$ pear install -o consultant_channel/Custom_Application
$ pear config-set php_dir /usr/lib/php
```

Right? Wrong.

Choosing this method of installing PEAR-packaged applications is bound to get you into trouble eventually. You may forget to set the configuration back to what it was, or using the `-a` flag during installation, which automatically installs any necessary dependencies, you may wind up with your dependencies installed in all kinds of strange and unexpected places.

In other words—*don't use this method*, even if it seems to make sense to do so.

## The "PEAR Default + Aliasing" Method

Using this method, a package would be configured to use the default PEAR Directory structure. Our `Custom_Application` package might be installed in `[php_dir]/Consultant/Custom_Application`. Once installed there, the installation location could be aliased by creating a symbolic link or by using Apache's `Alias` directive. (See http://httpd.apache.org/docs/urlmapping.html for details.)

The primary benefit to this method is that if the application being distributed can potentially have multiple installations on the same server, all installations that are symbolically linked or aliased to the location within the PEAR Default directory structure can be upgraded in a single operation. This behavior may be a positive or a negative, depending on your point of view and/or particular situation.

## The "PEAR Custom Roles" Method

Beginning with PEAR 1.4.0, a custom file role may be defined by a package configuration file that dictates a special location where certain files should be installed.

Prior to PEAR 1.4.0, package file roles were limited to a pre-defined list of roles:

- **php**: The default and most common role, this type of file is just a PHP file within a package.
- **ext**: Files of this role type should provide a binary extension to PHP.
- **src**: Files of this type are considered source files used for compiling PECL extensions.
- **test**: Regression tests for a package should be given the role test, and will be automatically installed in the PEAR Directory's `test_dir` directory.
- **data**: Considered to be supplementary to the package itself, data role files are for documentation, database schemas, examples of package usage, etc.
- **script**: Command-line scripts for use with a package should be assigned the role of script. (Tip: the `pear` command-line tool is defined as a script role type in the package configuration for PEAR itself.)

PEAR 1.4.0 allows package maintainers to expand upon this list of roles. By defining a custom role for a file, you are able to determine where files of that type are installed by default. Plus, with custom roles you are also able to extend PEAR's configuration commands (`config-set`/`config-show`/`config-get`) to allow for further customization of how particular roles are handled.

Since we are exploring the installation of an application that requires files that are directly accessible with a browser, a helpful file role would be a role that automatically sets the installation path for that type of file to a web site's `$DOCUMENT_ROOT`. The details of how to create such a role are outside the scope of this article—however, you can find a detailed explanation of creating custom file roles for PEAR packages in the PEAR online documentation. Meanwhile, a custom role called "Web" is included with the files related to this article. (See Role_Web-1.0.0.tgz in the code archive.)

With the custom Web role installed, PEAR has been extended to recognize a new configuration directive called `web_dir`. Using this directive, we are able to issue this command:

```bash
$ pear config-set web_dir /var/www/htdocs
```

Following that command, any file with a role of `web` will have the value of `web_dir` prepended to its installation path.

## Putting Together a Real Package

Now that we've covered the basic issues of how to install an application with "front end" requirements as a PEAR package in a hypothetical sense, let's apply these theories to a real-live application.

Rather than build a sample application from scratch, we'll focus applying these theories to an existing application that was built without any consideration for the default PEAR directory structure, or any other PEAR concepts for that matter. In doing so, I hope to illustrate how you can make *any* of your existing projects PEAR-installable—as well as any future projects you may develop.

## PEARifying phpMyAdmin

If you've been using PHP for any length of time at all, you're no doubt familiar with the venerable phpMyAdmin (http://www.phpmyadmin.net/). This popular and robust application has been around for many years, and is used by a very large number of PHP users ranging from novice to expert level. It also happens to be about as far away from the traditional notion of a PEAR package as we can get—making it an excellent guinea pig for learning how turn any PHP application into a PEAR-installable application.

Start off with downloading the latest release of phpMyAdmin (as of this writing, the latest version is 2.6.3-pl1). A glance through the directory structure of the standard distribution indicates that phpMyAdmin is intended to be fully accessible with a browser. In other words, the authors intend for the entire distribution to be located at `http://www.example.com/path/to/phpMyAdmin_Distribution/`. Based on this structure, we know that we need to use one of the two acceptable methods described above for installing a package that requires directly-accessible files.

The only other significant concern with a PEARified phpMyAdmin is to be sensitive regarding the application's configuration file. phpMyAdmin stores its configuration in a file called `config.inc.php`, which is located in the root directory of the distribution. The concern with this layout is that any upgrades handled by the PEAR installer will overwrite files with the same name in a directory structure by default; meaning that any future upgrade would overwrite a customized `config.inc.php` file with the distributed version of that file, and we will lose all our local customizations. To avoid this problem, we need to change the way our PEAR packaged distribution of phpMyAdmin distributes `config.inc.php` by renaming the file in the distribution to `config.inc.php.dist` and instructing users to make a copy of that file to `config.inc.php` in order to set up their installation.

Finally, since we know that phpMyAdmin releases updates on a fairly regular basis, we need to be prepared to update our PEAR packaged version quickly to reflect new releases by the phpMyAdmin team. To do that, we'll take advantage of the powerful PEAR_PackageFileManager package.

## PackageFileManager Crash Course

Throughout this article, I've made several references to "configuring your package." A PEAR packaged application or library carries with it a file called `package.xml` (and possibly a file called `package2.xml` for packages designed to be compatible with PEAR 1.3.x and PEAR 1.4.x). The `package.xml` file is the configuration file that tells the PEAR installer how to handle your packaged application. A wide range of configuration options are available, but the primary behaviours we'll want to keep in mind are how to configure dependencies, how to describe where our packaged applications comes from and what it does, and how to deal with installing individual files.

Greg Beaver's PEAR_PackageFileManager can be a somewhat daunting tool—to the point where many PEAR developers opt to manage their `package.xml` files manually. However, there is nothing to be afraid of regarding PackageFileManager. A little patience in configuring a package construction script that uses PackageFileManager pays off with huge dividends later when you need to make a quick release of your package and don't want be bothered with recalling the specifics of the complex `package.xml` structure each time you need to make a change.

Since we are building a package that leverages PEAR 1.4.0's capabilities, we will not concern ourselves with a PEAR 1.3.x compatible package in this article—we'll stay focused on PEAR 1.4.0's `package.xml` format, known as package.xml 2.0. Also, since PEAR 1.4.0 is still in an alpha state at this writing, PEAR_PackageFileManager's support of PEAR 1.4.0 compatible `package.xml` files is also in an alpha state. We will build as much of our `package.xml` as we can with PackageFileManager, and finish up with a few manual edits before doing the actual packaging. As PackageFileManager's support for the new package.xml 2.0 format matures, you should eventually be able to eliminate the need for any manual editing of your `package.xml` configuration files. For full documentation regarding the package.xml 2.0 format, please see http://pear.php.net/manual/en/guide.developers.package2.php.

With that overview under your belt, please refer to the listing below for a fully commented, step-by-step walkthrough of how we'll use PackageFileManager to build the `package.xml` file for our PEAR-installable phpMyAdmin distribution.

Please note that you will need the latest alpha version of PEAR_PackageFileManager in order to run the packager script.

```bash
$ pear config-set preferred_state alpha
$ pear install -o PEAR_PackageFileManager
```

With the latest alpha PEAR_PackageFileManager (PPFM from here on) installed, we're ready to begin packaging a PEAR 1.4.0-ready "front-end" web application.

## Packaging phpMyAdmin: Step by Step

Before we begin, make sure you've got a working directory that contains a PHP script, which we'll call "packager.php," that knows about your `include_path` (so that it can find PPFM packages). In that same working directory, download and expand a copy of phpMyAdmin 2.6.3-pl1.

As we discussed above, we need to choose a method for handling the installation of the "front end" web files. (The bulk of a phpMyAdmin installation should be considered front end files, due to the way the application is structured.) I recommend using the "Custom File Role" approach, which requires an explicit installation for each website it will be used for. There are a few good reasons for this approach with phpMyAdmin:

**Configuration file**: phpMyAdmin requires a configuration file that lives within the phpMyAdmin directory. If we chose a symbolic link method, we would create a symbolic link to the `[php_dir]/phpMyAdmin` directory as a whole, which means we would also need to modify files within the phpMyAdmin distribution to allow for the inclusion of config files from a location other than within the phpMyAdmin directory. Maintaining a package is enough work as it is—we don't want to get into maintaining a package of a patched version the application if we can avoid it.

**Selective upgrades**: by explicitly installing phpMyAdmin on each site that needs it, you are able to selectively perform upgrades as new releases are available. In the event of an upgrade that does not go well for some reason, you wind up only affecting a single site's phpMyAdmin functionality, limiting any potential disruption. True, this method means slightly more busywork if you need to upgrade multiple installations on one machine, but the peace of mind factor often wins in this scenario.

Since we have chosen the "Custom File Role" method for handling the front end files, we need to install a custom file role that suits our needs as discussed in the "PEAR Custom Roles" section above. Please make sure you have installed the Role_Web package, which provides the `web` custom file role, before continuing.

Now we're ready to go. Here's the complete packager script:

```php
<?php
/**
 * Before continuing, make sure you've installed the
 * Role_Web-1.0.0.tgz package. It is included with the
 * article files. You may also install it like this:
 *
 * $ pear channel-discover pearified.com
 * $ pear install pearified/Role_Web
 *
 * It is important to install this custom role before
 * continuing.
 */

require_once 'PEAR/PackageFileManager2.php';
PEAR::setErrorHandling(PEAR_ERROR_DIE);
$pkg = new PEAR_PackageFileManager2;

// Set options
$options = array();

// We'll install in a 'pma' directory
$options['baseinstalldir'] = '/pma';

// Where are we reading the files for our package from?
$options['packagedirectory'] =
    dirname(__FILE__).'/phpMyAdmin-2.6.3-pl1/';

$options['filelistgenerator'] = 'file';

// Define exact names of documentation and data files
$options['exceptions'] = array(
    'Documentation.txt'      => 'doc',
    'ChangeLog'              => 'doc',
    'CREDITS'                => 'doc',
    'INSTALL'                => 'doc',
    'LICENSE'                => 'doc',
    'README'                 => 'doc',
    'RELEASE-DATE-2.6.3-pl1' => 'data',
    'TODO'                   => 'doc'
);
$options['dir_roles'] = array('scripts' => 'data');

// Set up our custom web role with a wildcard
$options['roles'] = array('*' => 'web');
$pkg->setOptions($options);

// Set basic application information
$pkg->setPackage('phpMyAdmin');
$pkg->setSummary('MySQL Database Administration Tool');

$pkg->setDescription('phpMyAdmin is a tool written in
PHP intended to handle the administration of MySQL over
the Web. Currently it can create and drop databases,
create/drop/alter tables, delete/edit/add fields,
execute any SQL statement, manage keys on fields,
manage privileges, export data into various formats,
and is available in 50 languages.

** PLEASE NOTE: When installing for the first time,
copy config.inc.php.dist to config.inc.php, then make
changes to that copy.');

$pkg->setLicense('GPL',
    'http://www.phpmyadmin.net/documentation/LICENSE');

// 2.6.3-pl1 becomes 2.6.3pl1
$pkg->setReleaseVersion('2.6.3pl1');
$pkg->setAPIVersion('2.6.3pl1');

// Stability settings - dev, alpha, beta or stable
$pkg->setReleaseStability('stable');
$pkg->setAPIStability('stable');

// A 'php' Package type is a PEAR-style package
$pkg->setPackageType('php');

// Require at least PHP 4.1.0, as required by phpMyAdmin
$pkg->setPhpDep('4.1.0');

// Since this is a PEAR 1.4 package, after all ...
$pkg->setPearinstallerDep('1.4.0a12');

// Set the channel - you'd use your own channel server
// information here.
$pkg->setChannel('pearified.com');

// Add the package maintainer, who may not necessarily
// be a package developer. I'm the lead package maintainer
// in this case.
$pkg->addMaintainer(
    'lead','clay','Clay Loveless','clay@killersoft.com');

// Make sure we handle the config.inc.php to
// config.inc.php.dist renaming consistently.
$pkg->addInstallAs('config.inc.php', 'config.inc.php.dist');

// Add a release, and notes about this release.
$pkg->addRelease();
$pkg->setNotes('Initial PEAR-packaged release.');

// Generate the file list
$pkg->generateContents();

// Debug the package file by default, and
// create the actual package.xml file if this script
// is called with a 'make' argument.
if (isset($argv[1]) && $argv[1] == 'make') {
    $pkg->writePackageFile();

    // Add the 'usesrole' section for our custom file role.
    // PPFM1.6.0a1 does not have a method for automating this.
    $pkgxml = file_get_contents(
        $options['packagedirectory'].'package.xml');
    $usesrole = "  <usesrole>\n";
    $usesrole .= "    <role>web</role>\n";
    $usesrole .= "    <package>Role_Web</package>\n";
    $usesrole .= "    <channel>pearified.com</channel>\n";
    $usesrole .= "  </usesrole>";
    $pkgxml = str_replace("</dependencies>",
        "</dependencies>\n$usesrole",
        $pkgxml);
    $fp = fopen($options['packagedirectory'].'package.xml',
        'w');
    fwrite($fp, $pkgxml);
    fclose($fp);

} else {
    $pkg->debugPackageFile();
}
?>
```

Lines 14-19 set the stage by including the package.xml 2.0-aware PPFM, instantiating it, and setting an empty options array. In lines 21-27, we establish that we're going to be installing phpMyAdmin in a directory called `pma`, and that we're building the package from our downloaded copy of phpMyAdmin 2.6.3-pl1.

In line 28, we tell PPFM how to read our package directory. We're using the default "file" method, but if your package directory is actually a working copy checked out from a CVS or Subversion repository, you may use the "Cvs" or "Svn" methods, respectively. Other supported methods include "Perforce," "XMLOutput," and "SimpleGenerator."

PEAR-compatible packages generally install documentation and general data files in the respective `doc_dir` and `data_dir` locations, inside a subfolder with the same name as the package itself. In lines 31-40, we specifically declare some documentation and informational files to be filed according to this standard. We don't specify phpMyAdmin's `documentation.html`, `docs.css` or `translators.html` file, since moving those outside of the main application installation directory would break the functionality of the application.

Similarly, on line 41, we specify the entire `scripts` directory within the standard phpMyAdmin distribution as a data directory, since it contains a variety of files (some scripts, some schema files, etc.) which are not essential for phpMyAdmin to function.

The "web application" magic begins on line 44, as we override PPFM's default file roles to set everything we haven't already specified as files of the "web" role type. That will result in everything else being installed in the location specified by our new, custom `web_dir` PEAR configuration value. Note that you won't want to override the defaults in every scenario—but due to the architecture of the phpMyAdmin application, it makes sense to do it in this case. That completes our options setup, so we set the options in line 45.

Lines 48-64 define some basic information about phpMyAdmin, lifted nearly verbatim from descriptions on http://phpmyadmin.net. We make a slight adjustment to the official release version number on lines 67 and 68, due to the fact that PEAR does not consider version numbers with hyphens to be valid.

This version of phpMyAdmin is considered stable, so we set the package to the corresponding state in lines 71 and 72.

We're building a PEAR-style package (as opposed to a PECL extension source package or a binary extension distribution), so we set the package type to `php` in line 75.

In lines 78 and 81, we set a few basic dependencies. Since phpMyAdmin does not currently have any external dependencies, let's digress for a moment and illustrate how we would declare a dependency on the PEAR::DB package if that were an actual requirement of phpMyAdmin:

```php
$pkg->addPackageDepWithChannel(
    'DB',           // package name
    'pear.php.net', // package channel
    '1.6.0',        // minimum version
    false,          // no maximum version
    '1.7.6'         // recommended version
);
```

But, since we don't need that dependency for this package, just keep this in mind when you build you own application packages.

On lines 85 and 90, we set a little personal information. I have nothing to do with the phpMyAdmin package formally, but every package needs a maintainer and a channel server. So, we set those values here—your values for your own packages will most certainly be different!

Line 95 contains an important trick to keep future upgrades to this package from stepping on previous installations. As we discussed above, every phpMyAdmin installation needs a `config.inc.php` file at the top level of the phpMyAdmin installation directory. To avoid overwriting a customized `config.inc.php` file in the future, line 95 automatically renames `config.inc.php` to `config.inc.php.dist` at install-time.

Lines 98-102 complete a few formalities, and we're then ready to test the package file.

If your packager.php script is called with an argument of "make", lines 108-125 will write out the package file and manually add details relating to our custom file role. Otherwise, the script will display debug output relating to our package file on line 128.

Run the script like so:

```bash
$ php -f packager.php
```

If there are no errors, you can write out the package file.

```bash
$ php -f packager.php make
```

You will wind up with a file called `package.xml` inside the phpMyAdmin distribution directory. Create the package file itself by moving to the phpMyAdmin directory and running the package command.

```bash
$ cd phpMyAdmin-2.6.3-pl1
$ pear package
```

Presto! Now you've got a PEAR-installable distribution of phpMyAdmin.

## Further Reading

Now that you're sold on the benefits and ease of distributing applications via PEAR 1.4.0 packages, check out these resources for excellent documentation on configuring PEAR post-install scripts, setting up remote PEAR installations over FTP, and building your own PEAR channel server.

**PEAR post-install script documentation:**
- http://pear.php.net/manual/en/guide.migrating.postinstall.php
- http://pear.php.net/manual/en/guide.developers.package2.tasks.php#guide.developers.package2.tasks.postinstallscript

**Remote PEAR installation over FTP:**
- http://greg.chiaraquartet.net/archives/31-Using-PEAR-1.4.0-to-install-PEAR-packages-on-a-remote-host.html

**Setting up a PEAR channel server:**
- http://www.schlitt.info/applications/blog/index.php?/archives/308-Set-up-your-own-PEAR-channel.html

## Start distributing now

If you're not interested in getting your hands dirty setting up your own PEAR channel server, Pearified.com offers free hosting of open source PEAR 1.4.0-compatible packages, as well as commercial hosting solutions for closed-source and private packages. The service also offers a helpful wizard for converting your non-PEAR distribution into a PEAR-compatible distribution—essentially replacing the need for you to understand the ins and outs of PEAR_PackageFileManager.

## It's a Good Thing™

There is no question that changing the way you distribute your code can feel like a bother, and may not seem like it is worth the effort. However, the flexibility offered by the PEAR 1.4.0 installer can result in smaller distributions and fewer installation headaches for your end users.

A mature application packaging system is often a sign of a mature platform or language. As PHP continues to mature into an enterprise-class development platform, it is only fitting that the PEAR installer is maturing along with it. Once the PHP development community fully embraces library and application distribution through via PEAR packaging, we will all benefit from easily installable and reusable application components.

---

*Clay Loveless has been developing web applications with PHP since 1997's PHP/FI 2.0b6. A New York University-trained actor, Clay now works from California as an independent internet solutions consultant under the name Killersoft (http://www.killersoft.com). He is also actively involved in maintaining Pearified.com. Clay is a husband, father of a very cool one year old son, and a Zend Certified Engineer. Reach Clay via clay@killersoft.com.*
