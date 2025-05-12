# XSS (Cross-Site Scripting)

XSS (Cross-Site Scripting) is a client-side attack where attackers inject malicious code, typically JavaScript, into a trusted website. This malicious code is then executed in the victim's browser, leading to various security risks.

## Purpose of XSS

- Steal cookies or session IDs
- Hijack user accounts
- Modify web page content
- Redirect users to malicious websites

## Types of XSS

### Reflected XSS (Non-persistent, Immediate Execution)

- The malicious input (like a script) is not saved on the server.
- It is sent via a URL parameter or form input.
- The server immediately reflects this input back in the HTTP response (e.g., inside HTML, JS, or error messages).
- The script executes in the victim's browser once they click that URL or submit that form.

### Example

Consider the following URL:

```
http://vulnerable-site.com/search.php?q=<script>alert("XSS")</script>
```

If the server-side code is:

```php
<p>Search result for: <?php echo $_GET['q']; ?></p>
```

The JavaScript `<script>alert("XSS")</script>` is rendered as part of the HTML, and it executes in the victim's browser. This happens because the input is not sanitized or escaped before being included in the response.

Note :In many modern web apps use separate APIs, especially with React, Angular, etc. But in classic PHP (or any server-rendered site), the URL itself acts as the request to the server.

### Stored XSS (Persistent)

- The attacker submits a script to the server (e.g., in a form, comment box).
- The script gets stored in the database.
- Every time a user loads that page, the script runs automatically.

### Example

An attacker submits the following input in a comment box or name field:

```html
<script>
  alert("Stored XSS");
</script>
```

#### Behavior

1. The malicious script is stored in the database.
2. When the page is loaded by any user, the script is injected into the page.
3. The script executes in the browser of every visitor, causing widespread impact.

#### Key Points

- Stored XSS is more dangerous than reflected XSS because it affects multiple users.
- Proper input validation and output encoding are essential to prevent this type of attack.
- Use Content Security Policy (CSP) to mitigate the impact of XSS vulnerabilities.

### DOM-based XSS (Client-Side Only)

- No server involvement.
- JavaScript in the page reads from the URL, DOM, or cookies, and injects that into the page without sanitizing.
- The attacker manipulates the DOM directly.

### Example

Consider the following URL:

```
http://vulnerable-site.com/page.php#<script>alert('DOM XSS')</script>
```

If the page contains the following JavaScript:

```javascript
document.getElementById("msg").innerHTML = window.location.hash;
```

When a user visits the URL:

```
http://vulnerable-site.com/page.php#<script>alert('DOM XSS')</script>
```

The script `<script>alert('DOM XSS')</script>` is executed in the browser because the `window.location.hash` value is directly injected into the DOM without sanitization.

### Mitigation Strategies

- Avoid directly injecting untrusted data into the DOM.
- Use libraries like DOMPurify to sanitize user input.
- Validate and encode data before rendering it in the DOM.
- Implement a strict Content Security Policy (CSP) to block inline scripts.
- Regularly review and test your code for XSS vulnerabilities.

## Notes

- **Sanitizing Input :** Cleaning up user input to remove or neutralize anything dangerous before using it in your app. It’s like filtering or validating the input the user gives to ensure it doesn’t contain harmful stuff like:

- **Escaping Output :** When you're displaying user data on a page, convert any dangerous characters so the browser does NOT treat them as code.

## Common Sanitization Methods (PHP)

| **Function**         | **What it does**                                   |
| -------------------- | -------------------------------------------------- |
| `strip_tags()`       | Removes all HTML tags                              |
| `htmlspecialchars()` | Converts HTML characters to safe text              |
| `preg_replace()`     | Replaces dangerous patterns                        |
| Input validation     | Only allow expected formats (e.g., names, numbers) |

### Preventions

- **Filter input on arrival.** At the point where user input is received, filter as strictly as possible
  based on what is expected or valid input.

- **Encode data on output.** At the point where user-controllable data is output in HTTP
  responses, encode the output to prevent it from being interpreted as active content. Depending
  on the output context, this might require applying combinations of HTML, URL, JavaScript,
  and CSS encoding.

- **Use appropriate response headers.** To prevent XSS in HTTP responses that aren't intended to
  contain any HTML or JavaScript,

- **Content Security Policy.** As a last line of defense, you can use Content Security Policy (CSP)
  to reduce the severity of any XSS vulnerabilities that still occur.
