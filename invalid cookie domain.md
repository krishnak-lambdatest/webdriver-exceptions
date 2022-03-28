# Invalid cookie domain error
The WebDriver error - invalid cookie domain error, occurs if a cookie is illegally attempted to be set under a different domain from the current document.

The WebDriver does not allow setting cookies for domains different from the domain of the current browsing context's document's domain.

This error also occurs when the document is not loaded via `http://`, `https://` or `ftp://`, that is, cookie-averse document. 

## Example

### Cookie-averse documents

This error can occur when visiting a cookie-averse document, for example, a file on your local file system:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
session.get("file:///home/jdoe/document.html")
try:
    foo_cookie = {"name": "foo", "value": "bar"}
    session.add_cookie(foo_cookie)
except exceptions.InvalidCookieDomainException as e:
    print(e.message)
```

Output:

	InvalidCookieDomainException: Document is cookie-averse

### Other domains

It is not possible to add a cookie for the domain `example.org` if the current domain is `example.com`:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
session.get("https://example.com/")
try:
    cookie = {"name": "foo",
              "value": "bar",
              "domain": "example.org"}
    session.add_cookie(cookie)
except exceptions.InvalidCookieDomainException as e:
    print(e.message)
```

Output:

	InvalidCookieDomainException: https://example.org/
