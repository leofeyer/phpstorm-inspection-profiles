# PhpStorm Inspection Profiles

This package includes a PhpStorm inspection profile for Contao as well as a
general one. Both profiles assume that the [EA Extended][1] plugin is
installed.

## Installation

First download or clone the repo, then open PhpStorm and navigate to
"Preferences" → "Inspections". Click the "Show Scheme Actions" button next to
the profile drop-down and choose "Import Profile…".

## Adjustments

The following adjustments have been made compared to the default scheme:

### General

**Do not warn if the addition operator is used on arrays**
 
Using the addition operator is a good way to add not configured default options
to an array, therefore do not warn if the operator is used.

**Report if `compact()` can be used**

Using `compact()` can improve the readability of the code, therefore report if
it can be used.

**phpDoc comments**

Duplicating meta information in both type hints and phpDoc comments will lead
to inconsistent data, therefore only document what is not already in the method
signature.

Code snippet with duplicate meta data:

```php
class Foo
{
    /**
     * Description of what the method does.
     * 
     * @param string $str
     * @param int    $int
     * @param bool   $bool
     *
     * @return array
     */
    public method bar(string $str, int $int, bool $bool): array
    {
    }
}
```

Code snippet without duplicate meta data:

```php
class Foo
{
    /**
     * Description of what the method does.
     */
    public method bar(string $str, int $int, bool $bool): array
    {
    }
}
```

To keep PhpStorm from warning us about the missing phpDoc tags, the following
rules have been adjusted:

 * Do not warn about missing `@return` tags
 * Do not warn about missing `@throws` tags
 * Do not warn if a PHPDoc comment does not match the function/method signature

**Exception handling**
 
The exception checks in PhpStorm generate a lot of false-positives if not all
`@throws` tags are set correctly (and recursively!), therefore:

 * Do not warn about unhandled exception
 * Do not warn about redundant catch clauses

**Warn about case mismatch in method call or class usage**

Even though method calls are case-insensitive in PHP, it seems a good practice
to use the correct case.

**Do not warn if the security advisories package is missing**

Even though the security advisories package is a good thing, it is not always
necessary to add it to your `composer.json` file (e.g. if you maintain your own
security meta package or if you use the [Symfony Security Checker][2] instead),
therefore do not warn if it is not present.

**Do not warn if `strtr()` could be replaced with `str_replace()`**

Using `str_replace()` is not much different from using `strtr()` in terms of
code readability, therefore do not suggest to replace it.

### Contao

The Contao profile includes everything from the General profile plus:

**Do not warn about undefined fields**

Contao models use `@property` tags to define the fields which are accessible
through magic methods. However, since models can be extended and there is no
way to add `@property` tags on the fly, a lot of false-positive warnings about
undefined fields will be generated. 

**Do not warn about unused parameters**

Sometimes using an interface or a hook requires a certain method signature,
even though not all arguments are used in the method body, therefore disable
the check.

**Do not warn about static method invocation via `->`**

Contao uses adapters to allow unit-testing methods of the old Contao 3
framework. Since most of these methods are static but are not invoked
statically through the adapter, disable this check.

**Do not warn about unsupported string offset operations**

PhpStorm generates a lot of false-positive warnings about unsupported string
offset operations when working with the globals array like this:

```php
$GLOBALS['TL_LANG']['MSC']['articlePicker'] = 'Article picker';
```

Therefore disable this check.

[1]: https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended-
[2]: https://security.symfony.com
