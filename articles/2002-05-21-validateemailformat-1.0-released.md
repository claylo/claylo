# validateEmailFormat 1.0 Released

May 21, 2002 -- KillerSoft is proud to release its PHP translation of Jeffrey E.F. Friedl's definitive Email Regex Program from O'Reilly's Mastering Regular Expressions.

This function is used to confirm if an e-mail address adheres to the RFC 822 specification for internet email addresses.

Why'd we do this?

Well, the PHP online docs say the following in the "add a note" section:

"(And if you're posting an example of validating email addresses, please don't bother. Your example is almost certainly wrong for some small subset of cases. See this information from O'Reilly Mastering Regular Expressions book for the gory details.)"

Good advice, I think. So good, in fact, that I figured it was time someone just went ahead and translated that regex into PHP. This code is distributed in accordance with O'Reilly's policy on re-use of code examples from their books. http://www.oreilly.com/ask_tim/codepolicy_1101.html

EXAMPLE:

```php
<?php
include("/path/to/validateEmailFormat.php");
$email = "foo@foo.com.au";
$isValid = validateEmailFormat($email);
if($isValid) {
    // do whatever you need to do
} else {
    echo "sorry, that address isn't formatted properly.";
}
?>
```

Additional examples included in the distributed file.

Download validateEmailFormat 1.0 Now!
