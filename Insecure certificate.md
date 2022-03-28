# Insecure certificate error
The WebDriver error - insecure certificate error, arises when the browser controlled remotely faces a certificate warning. This error is generally the consequence of visiting a website with an expired or invalid TLS certificate. These invalid certificates could either be self-signed, revoked, or cryptographically insecure certificates.

Web browsers do not send information to domains with broken certificates because communication with the server will be compromised. It is highly recommended that instead of disabling certificate checks in test environments, administrators fix the certificate situation. This is recommended even for test deployments.

The WebDriver offers an acceptInsecureCerts capability for disabling certificate checks for the current session's duration. Its use, however, should be avoided.

## Example

This error will occur when connecting to a domain that has a self-signed TLS certificate using the following Python code:


	from selenium import webdriver
	from selenium.common import exceptions

	session = webdriver.Firefox()
	try:
	    session.get("https://self-signed.badssl.com/")
	except exceptions.InsecureCertificateException as e:
	    print("Hit insecure cert on {}".format(session.current_url)

Output:

	Hit an insecure cert on https://self-signed.badssl.com/
