# Unknown command error

The WebDriver error - unknown command error, happens when a command or HTTP endpoint is not recognized by the driver.

## Examples

A `404 Not Found` HTTP status code is returned with the unknown command error when an non-existent `/session/{session id}/foo` endpoint is accessed:

```
% curl -i -d '{}' http://localhost:4444/session/foo
HTTP/1.1 404 Not Found
Connection: close
Content-Type: application/json; charset=utf-8
Cache-Control: no-cache
Content-Length: 113
Date: Fri, 30 Mar 2018 15:30:51 GMT

{"value":{"error":"unknown command","message":"POST /session/asd did not match a known command","stacktrace":""}}```
