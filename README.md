# Curler


A fluent API wrapper for libcurl in php.  Setting options and headers is done using
method chaining instead of setting options explicitly using the libcurl constants.

Debugging cURL commands in php using the Curler class is insanely simple as well.
Just chain the `dryRun()` method onto the end of your method chain instead of
the `go()` method and it will dump out all of the cURL request information
without making the request.
 
See http://php.net/manual/en/book.curl.php for information on libcurl.

Note: This repo is in its infancy and may not be suitable for all
applications, however it is great for simple and semi-advanced 
requests.

Documentation is located in the `Curler.php` file for now, but examples on usage will be added.

## Examples

#### Getting a web-page
Grab the HTML for a web page to be displayed in the web browser without rendering the HTML.
```php
$curler = new Curler('https://github.com/');

$curler->followRedirects() // Will follow redirects option set to true.
    ->header('Connection', 'keep-alive')  // Set some headers
    ->header('Accept', 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8')
    ->header('Accept-Language', 'en-US,en;q=0.5')
    ->header('Host', 'github.com')
    ->header('Content-Type', 'application/x-www-form-urlencoded')
    ->cookieJar('/home/user/gitCookie') // Set a file to use as cookie jar.
    ->suppressOutput() // Sets the RETURNTRANSFER option to true so that output is fetched as string instead of displayed automatically.
    ->suppressRender() // Display in browser as HTML text instead of rendering the HTML.  Great for debugging!
;

$html = $curler->go(); // Replace go() with dryRun() to get debug info on the request without executing it.
var_dump($html);
```
