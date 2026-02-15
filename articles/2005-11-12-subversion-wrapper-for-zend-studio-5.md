# Subversion Wrapper for Zend Studio 5

As I mentioned [yesterday](http://www.killersoft.com/randomstrings/index.php?url=2005/11/10/8-Switching-Pains-BBEdit-8-to-Zend-Studio-5.html#comment25), one of the things about Zend Studio 5 that’s been really irritating is the unnecessary use of, and escaping of, double quotes in Subversion commit messages triggered by Zend Studio 5.

The following little script fixes that behavior by dropping the opening and closing double quotes, and stripping slahses within the commit message, as they simply don’t need to be there. The script is written with the Mac OS X environment in mind, so tweak as you need to if you’re also experiencing this problem.

`#!/usr/bin/php  
/**  
* zendsvn  
*  
* Wrapper script to strip unnecessary quotes from latest Zend Studio 5  
* SVN commit message.  
*  
* Copyright (c) 2005 Clay Loveless (http://www.killersoft.com)  
*  
* Permission is hereby granted, free of charge, to any person obtaining  
* a copy of this software and associated documentation files (the  
* “Software”), to deal in the Software without restriction, including  
* without limitation the rights to use, copy, modify, merge, publish,  
* distribute, sublicense, and/or sell copies of the Software, and to  
* permit persons to whom the Software is furnished to do so, subject to  
* the following conditions:  
*  
* The above copyright notice and this permission notice shall be  
* included in all copies or substantial portions of the Software.  
*  
* THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND,  
* EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF  
* MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND  
* NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE  
* LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION  
* OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION  
* WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.  
*/`

/\*\*  
\* Use PEAR’s system command to find the svn executable  
\*/  
require\_once ‘System.php’;

$svnargs = ‘’;  
if (!empty($argv)) {  
    // Is this a commit message?  
    if ($argv[1] == ‘commit’ || $argv[1] == ‘ci’) {  
        // Commit message is written to temporary file stored in a location passed in $argv[4]  
        $lastCommitTmp = $argv[4];  
        $lastCommitMsg = file\_get\_contents($lastCommitTmp);  
        // Get rid of encapsulating quotes  
        $lastCommitMsg = substr($lastCommitMsg, 1, -1);  
        $lastCommitMsg = stripslashes($lastCommitMsg);

        // Write it back for use by SVN  
        echo “Fixing Zendism in $lastCommitTmp …\n”;  
if ($fp = fopen($lastCommitTmp, ‘w’)) {  
            fwrite($fp, $lastCommitMsg);  
            fclose($fp);  
}  
}  
    $argvlen = count($argv);  
for ($i = 1; $i < $argvlen; $i++) {  
        $svnargs .= $argv[$i].‘ ‘;  
}  
}  
$svn = System::which(’svn’, ‘/usr/local/bin/svn’);  
passthru(“$svn $svnargs”);  
?>

To use the script, just copy it into your executable path, make it executable, then select it as your SVN command-line tool in Preferences » Source Control » Path to SVN.

The above script is released under the [MIT License](http://www.opensource.org/licenses/mit-license.php), so run with it as you see fit.
