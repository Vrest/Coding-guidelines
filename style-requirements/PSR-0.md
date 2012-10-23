The following describes the mandatory requirements that must be adhered
to for autoloader interoperability.

Mandatory
---------

* A fully-qualified namespace and class must have the following
  structure `\<Vendor Name>\(<Namespace>\)*<Class Name>`
* Each namespace must have a top-level namespace ("Vendor Name").
* Each namespace can have as many sub-namespaces as it wishes.
* Each namespace separator is converted to a `DIRECTORY_SEPARATOR` when
  loading from the file system.
* The fully-qualified namespace and class is suffixed with ".php" when
  loading from the file system.
* Alphabetic characters in vendor names, namespaces, and class names may
  be of any combination of lower case and upper case.

Examples
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

Underscores in Namespaces and Class Names
-----------------------------------------

Underscores are illegal in Namespace names, class names and method names (except for the magic php functions).
