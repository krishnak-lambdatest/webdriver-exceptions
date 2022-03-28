# Stale element reference error

The WebDriver error - stale element reference error, happens when the referenced web element isn't attached to the DOM.

Dom elements in the WebDriver are identified by a unique reference called a web element. The web element reference is a globally unique identifier   which is utilised in executing commands to target particular elements like getting the property of an element etc.

In JavaScript, a stale element in the DOM has lost its connection to the document after it was deleted from the document or the document was changed. For example, staleness can occur when the web element reference from the document it is retrieved from is navigated away.

## Examples

### Document navigation

Upon navigating away from the page, all web element references to the previous page will be discarded. A stale element reference error occurs when subsequent interaction with a discarded web element fails because it is no longer in the document: 

```
import urllib

from selenium import webdriver
from selenium.common import exceptions

def inline(doc):
    return "data:text/html;charset=utf-8,{}".format(urllib.quote(doc))

session = webdriver.Firefox()
session.get(inline("<strong>foo</strong>"))
foo = session.find_element_by_css_selector("strong")

session.get(inline("<i>bar</i>"))
try:
    foo.tag_name
except exceptions.StaleElementReferenceException as e:
    print(e)

```

Copy to Clipboard

Output:

	StaleElementReferenceException: The element reference of e75a1764-ff73-40fa-93c1-08cb90394b65 is stale either the element is no longer attached to the DOM, it is not in the current frame context, or the document has been refreshed

### Node removal

A document node's web element reference will be invalidated when the node is deleted from the DOM. Any subsequent reference to the web element will also throw the same error:

```
import urllib

from selenium import webdriver
from selenium.common import exceptions

def inline(doc):
    return "data:text/html;charset=utf-8,{}".format(urllib.quote(doc))

session = webdriver.Firefox()
session.get(inline("<button>foo</button>"))
button = session.find_element_by_css_selector("button")
session.execute_script("""
    let [button] = arguments;
    button.remove();
    """, script_args=(button,))

try:
    button.click()
except exceptions.StaleElementReferenceException as e:
    print(e)
```

Output:

	StaleElementReferenceException: The element reference of e75a1764-ff73-40fa-93c1-08cb90394b65 is stale either the element is no longer attached to the DOM, it is not in the current frame context, or the document has been refreshed
