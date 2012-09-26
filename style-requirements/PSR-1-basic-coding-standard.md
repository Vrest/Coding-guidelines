Coding standards and guidelines
===============================

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt


What you need to know first.
----------------------------
PHP as a language does not offer some things developers have come to take for granted in other languages. For some of these things relatively simple workarounds exist:

### Static constructors
Any code directly after a class declaration is considered the static constructor.
Unlike for example c#, static constructors are **not** guaranteed to be executed before any other code is executed.

### Properties vs. fields
A property is conceptually just an attribute of some object that can be inspected or manipulated or both. PHPs properties do not offer the distinction required. From here on. We take on the following connotation:

* php properties SHALL NOT EVER be declared public
* php properties will henceforth be referred to as "fields" or "backing fields"
* a property is a piece of API, therefor implemented in methods.
* properties can be expressed in any combination of getters and setters
* a setter method name MUST always start with `set`.
* a getter method name MUST always start with `get` except when the property clearly refers to a boolean value, in which case it MAY also start with `is`, `has`, `wants`, etc.* 

#### Fields
Fields MUST NOT be declared public.

### Inner Classes
Since In PHP it is not possible to nest class declarations, but it may still be very useful


1. Overview
-----------

- Files MUST use only `<?php` and `<?=` tags.
- Files MUST use only UTF-8 without BOM for PHP code.
- Files SHOULD *either* declare symbols (classes, functions, constants, etc.)
  *or* cause side-effects (e.g. generate output, change .ini settings, etc.)
  but MUST NOT do both.
- Namespaces and classes MUST follow [PSR-0][].
- Class names MUST be declared in `PascalCase`.
- Class constants SHOULD be declared in all upper case with underscore separators. With an exception for labels in `Enum` subclasses.
- Method names MUST be declared in `camelCase`.


2. Files
--------

### 2.1. PHP Tags

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the other tag variations.

### 2.2. Character Encoding

PHP code MUST use only UTF-8 without BOM.

### 2.3. Side Effects

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

```
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

```
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```

3. Namespace and Class Names
----------------------------

Namespaces and classes MUST follow [PSR-0][].

This means each class is in a file by itself, and is in a namespace of at
least one level: a top-level vendor name.

Class names MUST be declared in `PascalCase`.

Code MUST use formal namespaces.

For example:

```
<?php

namespace Vendor\Model
{
	class Foo
	{
	}
}

#EOF

```

4. Class Constants, Fields, and Methods
-------------------------------------------

The term "class" refers to all classes, interfaces, and traits.

### 4.1. Constants

Class constants MUST be declared in all upper case with underscore separators.
For example:

```
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. Fields

This guide intentionally avoids any recommendation regarding the use of
`$PascalCase`, `$camelCase`, or `$under_score` field names.

Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.

### 4.3. Methods

Method names MUST be declared in `camelCase()`.


