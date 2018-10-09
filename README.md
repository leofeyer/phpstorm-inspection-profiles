# PhpStorm Inspection Profiles

This package includes PhpStorm inspection profiles for Contao 3 and 4 as well
as one general profile. All profiles assume that the [EA Extended][1] plugin is
installed.

## Installation

First download or clone the repo, then open PhpStorm and navigate to
"Preferences" → "Inspections". Click the "Show Scheme Actions" button next to
the profile drop-down and choose "Import Profile…".

## Adjustments

The following adjustments have been made compared to the default scheme:

### General

**composer.json**

 * Do not warn about not installed packages

**HTML**

 * Disable completely

**JSON and JSON5**

 * Do not warn if not compliant with JSON schema

**PHP**

 * Warn about case mismatch in method call or class usage
 * Do not warn about redundant catch clauses
 * Do not warn about unhandled exception
 * Do not warn if a class overrides a field of its parent class
 * Report if `compact()` can be used
 * Do not warn if the addition operator is used on arrays
 * Do not warn if the security advisories package is missing
 * Do not warn about missing `@return` tags
 * Do not warn about missing `@throws` tags
 * Do not warn if a PHPDoc comment does not match the function/method signature
 * Do not warn about multiple class declarations

**RELAX NG**

 * Disable completely

**Spelling**

 * Disable completely

**XML**

 * Do not warn about unbound XML namespace prefixes

### Contao 4

Everything from the General profile plus:

**PHP**

 * Do not warn if a callable parameter usage violates its definition
 * Do not warn about long inheritance chains
 * Do not warn if there are constants without access modifier
 * Do not warn about static method invocation via `->`
 * Do not warn if a general `\Exception` is thrown
 * Do not warn if `strtr()` could be replaced with `str_replace()`
 * Do not warn about unsupported string offset operations
 * Do not warn about `strlen()` being misused
 * Do not warn about forgotten debug statements
 * Do not warn about undefined fields
 * Do not warn about unused parameters

### Contao 3

Everything from the Contao 4 profile plus:

**CSS**

 * Disable completely

**General**

 * Disable annotators

**PHP**

 * Do not warn if the declaration access can be weaker
 * Do not warn about missing or empty conditionals group statements
 * Do not warn about nested positive ifs
 * Do not warn about unnecessary double quotes
 * Do not warn about unnecessary parentheses
 * Do not warn about nested ternary operators
 * Do not warn if `isset()` constructs can be merged
 * Do not warn about non-optimal if conditions
 * Do not warn about redundant `else` keywords
 * Do not warn if `unset()` constructs can be merged
 * Do not warn if the `::class` constant can be used
 * Do not warn if a return type hint can be used
 * Do not warn if the short list syntax can be used
 * Do not warn about non-optimal regular expressions
 * Do not warn about class autoloading correctness
 * Do not warn about the magic methods validity
 * Do not warn about improper `preg_quote()` usage
 * Do not warn about type unsafe usages of `in_array()` and `array_search()`
 * Do not warn if a parameter could be declared as array
 * Do not warn about type unsafe comparisons
 * Do not warn about missing `break` statement
 * Do not warn about missing parent calls in constructors

[1]: https://plugins.jetbrains.com/plugin/7622-php-inspections-ea-extended-
