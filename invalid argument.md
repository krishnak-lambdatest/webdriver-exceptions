# Invalid argument error

The WebDriver error - invalid argument error, arises when invalid arguments are passed to a command.

The InvalidArgument error is somewhat similar to a TypeError in JavaScript, as both errors can occur for various APIs when the input value is not of the expected type, or is distorted in some way. Look at the type and bounds constraints for every WebDriver command.

## Example

For instance, we cannot set the window size to a negative value:

```
from selenium import webdriver
from selenium.common import exceptions

session = webdriver.Firefox()
try:
    session.set_window_size(-100, 0)
except exceptions.InvalidArgumentException as e:
    print(e.message)
```

Output:

	InvalidArgumentException: Expected -100 to be >= 0
