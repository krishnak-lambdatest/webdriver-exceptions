# Invalid session ID

This WebDriver error - invalid session ID error, happens if the unique session identifier is not recognized by the server. It also occurs when the session ID is not valid or the session has been removed.

## Example

### Explicit session removal

When quitting, a WebDriver is explicitly removed:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
print("Current session is {}".format(session.session_id))
session.quit()

try:
    session.get("https://mozilla.org")
except exceptions.InvalidSessionIdException as e:
    print(e.message)
```

Output:

	Current session is 46197c16-8373-469b-bc56-4c4d9e4132b4
	No active session with ID 46197c16-8373-469b-bc56-4c4d9e4132b4

### Implicit session removal

If the last window or tab is closed, the session is _implicitly deleted_:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
print("Current session is {}".format(session.session_id))

# closes current window/tab
session.close()

try:
    session.get("https://mozilla.org")
except exceptions.InvalidSessionIdException as e:
    print(e.message)
```

Output:

	Current session is 46197c16-8373-469b-bc56-4c4d9e4132b4
	No active session with ID 46197c16-8373-469b-bc56-4c4d9e4132b4
