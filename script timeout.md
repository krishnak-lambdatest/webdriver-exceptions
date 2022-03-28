# Script timeout
The WebDriver error - script timeout error happens when a user script fails to complete before the script timeout duration of the session expires.

The script timeout duration is a configurable capability—meaning you can change how long it takes for the driver to interrupt an injected script. The driver will wait up to 30 seconds, by default, before interrupting the script and returning with a script timeout error. This can be modified to be longer, shorter, or indefinite. 

If the session script timeout duration is set to null,  the timeout duration to becomes indefinite, and there is a risk of a non-recoverable session state.

## Example

The following asynchronous script will resolve the promise or invoke the callback after 35 seconds have passed:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
try:
    session.execute_script("""
        let [resolve] = arguments;
        window.setTimeout(resolve, 35000);
        """)
except exceptions.ScriptTimeoutException as e:
    print(e.message)
```

Output:

	ScriptTimeoutException: Timed out after 35000 ms
	
You can extend the default script timeout by using capabilities if you have a script that you expect will take longer to run:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox(capabilities={"alwaysMatch": {"timeouts": {"script": 150000}}})
session.execute_script("""
    let [resolve] = arguments;
    window.setTimeout(resolve, 35000);
    """)
print("finished successfully")
```

Output:

	finished successfully
