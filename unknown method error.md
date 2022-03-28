# Unknown method error

The WebDriver error - unknown method error happens when the HTTP request method for an endpoint is not recognized by the driver.

A mostly REST-ish API is provided by the WebDriver and the `GET`, `POST`, and `DELETE` methods are are not supported for all endpoints. This error might happen when an endpoint with an unsupported HTTP requested method is called. 

## Examples

For example, the New Session command has a `POST` request and a `DELETE` request endpoint:

```
% curl -d '{}' http://localhost:4444/session
{"sessionId":"d4605710-5a4e-4d64-a52a-778bb0c31e00","value":{"XULappId":"{ec8030f7-c20a-464f-9b0e-13a3a9e97384}","acceptSslCerts":false,"appBuildId":"20160913030425","browserName":"firefox","browserVersion":"51.0a1","command_id":1,"platform":"LINUX","platformName":"linux","platformVersion":"4.9.0-1-amd64","processId":17474,"proxy":{},"raisesAccessibilityExceptions":false,"rotatable":false,"specificationLevel":0,"takesElementScreenshot":true,"takesScreenshot":true,"version":"51.0a1"}}
```

```
% curl -X DELETE http://localhost:4444/session/d4605710-5a4e-4d64-a52a-778bb0c31e00
{}
```

However, it does not contain a `GET` method and this will throw an unknown method error:
```
% curl http://localhost:4444/session/650f9df3-740e-314c-958d-307e41752fae
{"value":{"error":"unknown command","message":"GET /session/650f9df3-740e-314c-958d-307e41752fae did not match a known command","stacktrace":""}}%
```
