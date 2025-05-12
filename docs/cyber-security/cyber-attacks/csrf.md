# Cross-Site Request Forgery (CSRF)

## What is CSRF?

Cross-Site Request Forgery (CSRF) is an attack where a hacker tricks a logged-in user’s browser into making an unwanted request to a website without their knowledge.

It exploits the trust that a website has in the user's browser, using the user's identity and session to perform actions they never intended — such as changing passwords, transferring money, or deleting accounts.

---

## Real-life Example

Imagine the following scenario:

1. You are logged in to your bank's website (`yourbank.com`).
2. Meanwhile, a hacker tricks you into clicking a malicious link or loading a page in the background.
3. That page secretly sends a request like this:

   ```http
   POST yourbank.com/transfer?to=Hacker&amount=10000
   ```

- Your browser sends the request along with your cookies/session, and the bank processes it as if you initiated the action.

**Result:** The hacker successfully transfers money from your account without your knowledge.

---

## How to Prevent CSRF

To mitigate CSRF attacks, websites can implement the following measures:

- **CSRF Tokens:** Include unique, unpredictable tokens in forms and verify them on the server.
- **SameSite Cookies:** Use the `SameSite` attribute in cookies to restrict cross-origin requests.
- **User Authentication:** Require re-authentication for sensitive actions.
- **CORS Policies:** Restrict cross-origin requests to trusted domains.

### Additional Details on Prevention Techniques

#### 1. CSRF Tokens

Generate a random, secret token when the form loads. Add it as a hidden field in the form and validate it on the server when the form is submitted.

Example:

```html
<form action="submit.php" method="POST">
  <input type="hidden" name="csrf_token" value="a1b2c3d4" />
</form>
```

On the server, ensure the `csrf_token` is valid for the session before processing the request.

#### 2. SameSite Cookies

Use the `SameSite` attribute in cookies to prevent them from being sent with cross-site requests.

Example:

```http
Set-Cookie: sessionid=abc123; SameSite=Strict;
```

This ensures cookies are only sent with requests originating from the same site.

#### 3. Referer Header Validation

Validate the `Referer` header on the server to ensure the request originated from your domain. If the `Referer` is missing or from an untrusted source, block the request.

By implementing these strategies, websites can significantly reduce the risk of CSRF attacks.
