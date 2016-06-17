# The TSR Coding Standard

This repository outlines the coding standard in use at TSR.

## Introduction

Coding Standards are an important factor for achieving high quality code.
A common visual style, naming conventions and other technical settings allow us
to produce consistent, readable and maintainable code.

The key to a good coding standard is consistency. Consistency with this standard
is important. Consistency within a project is more important. Consistency within
one class or function is the most important.

However, know when to be inconsistent -- sometimes standard recommendations just
aren't applicable. When in doubt, use your best judgment. Look at other examples
and decide what looks best. And don't hesitate to ask!

Not all important factors can be covered by rules and coding standards.
Equally important is the style in which certain problems are solved
programmatically - it’s the personality and experience of the individual
developer which shines through and ultimately makes the difference between
technically okay code or a well considered, mature solution.

## Our Standard

The TSR standard is an amalgamation of elements of [PSR 1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
and [PSR 2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) along with
our own requirements. It aims to strike a balance between defined rules and
developer freedom. As such, where a particular case or style is not indicated or
defined, developers are free to apply their own coding style - bearing in mind
the points on consistency made above.

The standard is also open to change - if you spot an error or ommission, have a
suggestion or think something should be changed, then bring it up!

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this standard are to be
interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

### 1. Overview

### 2. Files

#### 2.1. PHP Tags

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the
 other tag variations.

#### 2.2. Character Encoding

PHP code MUST use only UTF-8 without BOM.

#### 2.3. Line Endings

PHP code files MUST use the Unix LF (linefeed) line ending.

There MUST NOT be trailing whitespace at the end of lines.

#### 2.4. Indentation

PHP code MUST use an indent of 4 spaces, and MUST NOT use tabs for indenting.

#### 2.5. Side Effects

A file SHOULD declare new symbols (classes, functions, constants, etc.) and
cause no other side effects, or it SHOULD execute logic with side effects,
but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

#### 2.6. General

There SHOULD NOT be more than one statement per line.

The closing ?> tag MUST be omitted from files containing only PHP.

### 3. Namespaces and Use Statements

Code written for PHP 5.3 and after MUST use formal namespaces.

Namespaces and classes MUST follow an "autoloading" PSR. This SHOULD be
[PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md),
however [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md)
MAY be used where absolutely neccessary.

This means each class is in a file by itself, and is in a namespace of at least
one level.

When present, there MUST be one blank line after the namespace declaration.

When present, all use declarations MUST go after the namespace declaration.

There MUST be one use keyword per declaration.

There MUST be one blank line after the use block.

For example:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```

### 4. Classes

The term "class" refers to all classes, interfaces, and traits.

#### 4.1. DocBlocks

All classes MUST have a DocBlock describing the purpose of the class.

#### 4.2. Naming

Class names MUST be declared in StudlyCaps.

#### 4.3. Extends and Implements

The extends and implements keywords MUST be declared on the same line as the
class name.

The opening brace for the class SHOULD also go on this line (see exception
below); the closing brace for the class MUST go on the next line after the body.

```php
class ClassName extends ParentClass implements \ArrayAccess, \Countable {
    // constants, properties, methods
}
```

Lists of implements MAY be split across multiple lines, where each subsequent
line is indented once. When doing so, the first item in the list MUST be on the
next line, there MUST be only one interface per line and the opening brace for
the class MUST go on its own line.

```php
class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

#### 4.4. Properties

Visibility MUST be declared on all properties.

When present, the `static` declaration MUST come after the visibility
declaration.

The var keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

Property names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

This standard intentionally avoids any recommendation regarding the use of
`$StudlyCaps`, `$camelCase`, or `$under_score` property names.

Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.

#### 4.5. Methods

All methods MUST have a DocBlock describing the purpose of the method. The
`@param` definitions MUST match the method's argument list.

Visibility MUST be declared on all methods.

When present, the `abstract` and `final` declarations MUST precede the
visibility declaration.

When present, the `static` declaration MUST come after the visibility
declaration.

Method names MUST be declared in camelCase().

Method names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

The opening brace MUST go on the same line as the method name, and the closing
brace MUST go on the next line following the body.

In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument list.

Argument lists MAY be split across multiple lines, where each subsequent line is
indented once. When doing so, the first item in the list MUST be on the next
line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed together on their own line with one space
between them.

```php
class ClassName {
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

#### 4.6. Method and Property Ordering

To assist navigation within a class, methods and properties SHOULD be defined in
the following order `public`, `protected`, `private`.

Where modifiers are used the sub-order SHOULD be `abstract`, `static`, `final`.

```php
class ClassName {

    public static $var1;
    public $var2;

    protected static $var3;
    protected $var4;

    private static $var5;
    private $var6;

    abstract public function method1();

    public static function method2() {
        // method body
    }
    
    final public function method3() {
        // method body
    }
    
    public function method4() {
        // method body
    }
    
    // abstract protected methods
    // static protected methods
    // final protected methods
    // protected methods

    // abstract private methods
    // static private methods
    // final private methods
    // private methods

}
```

### 5. General

#### 5.1. Constants

Global constants (via `define()`) SHOULD be avoided.

The PHP constants `true`, `false`, and `null` MUST be in lower case.

All other constants MUST be declared in all upper case with underscore separators.



#### 5.2. Control Structures

This standard is intentionally flexible regarding the formatting of control
structures, with the following caveats.

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look, and reduces the likelihood of introducing errors as new
lines get added to the body.

The opening brace MUST go on the same line as the opening statement, and the
closingbrace MUST go on the next line following the structure body.

The keyword `elseif` SHOULD be used instead of `else if` so that all control
keywords look like single words.

The `case` statement MUST be indented once from `switch`, and the `break`
keyword (or other terminating keyword) MUST be indented at the same level as the
`case` body. There MUST be a comment such as `// no break` when fall-through is
intentional in a non-empty case body.

Whatever other formatting convention is used SHOULD be applied consistently
within a reasonable scope. That scope may be vendor-level, package-level,
class-level, or method-level.

#### 5.3. General

Super-globals MUST NOT be accessed directly.

The following keywords and functions MUST NOT be used: `goto`, `die`, `eval`,
`exit`, `global`.

The error control operator `@` SHOULD NOT be used.

Comma delimiters SHOULD be followed by a single space.

Binary operators (==, &&, ...) SHOULD be surrounded by a single space, with the
exception of the concatenation (.) operator.

For type-hinting in PHPDocs and casting the following SHOULD be used:
* `bool` (instead of `boolean` or `Boolean`)
* `int` (instead of `integer`)
* `float` (instead of `double` or `real`)
