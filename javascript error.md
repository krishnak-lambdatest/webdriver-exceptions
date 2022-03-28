# Javascript error

The WebDriver error - javascript error, happens a user script execution fails.

The reason for the execution failure is generally provided in the error message, including a stacktrace of the error given by the browser's JavaScript engine.

## Example

The below script attempts to use an undefined variable. This usually is thrown as a `ReferenceError` by JavaScript. It is caught by WebDriver and is serialized as a JavaScript error:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
try:
    session.execute_script("return foo")
except exceptions.JavascriptException as e:
    print(e.message)
```

Output:
	
	JavascriptException: ReferenceError: foo is not defined
