# Web Hosting & DNS Records

## DNS Records Explained

1. **A Record (Address)**

```mermaid
flowchart LR
    A[example.com] -->|A Record| B[192.168.1.10]
```

- Points domain to IP address
- Direct connection
- Fast resolution
- Example: `example.com → 192.168.1.10`

2. **CNAME (Canonical Name)**

```mermaid
flowchart LR
    A[www.example.com] -->|CNAME| B[example.com]
    B -->|A Record| C[192.168.1.10]
```

- Points domain to another domain
- Like an alias
- Flexible but slower
- Example: `www.example.com → example.com`

3. **MX Record (Mail Exchange)**

```mermaid
flowchart LR
    A[example.com] -->|MX Record| B[mail.example.com]
    B -->|Priority 10| C[mail1.example.com]
    B -->|Priority 20| D[mail2.example.com]
```

- Email routing
- Multiple servers
- Priority based
- Example: `example.com → mail1.example.com (10)`

4. **TXT Record (Text)**

- SPF records
- DKIM verification
- Domain verification
- Example: `v=spf1 include:_spf.google.com ~all`

## Real-World Example: Website Setup

```mermaid
flowchart TD
    A[Buy Domain] --> B[Get Hosting]
    B --> C[Configure DNS]
    C --> D[A Record Setup]
    C --> E[CNAME Setup]
    C --> F[MX Setup]
    D --> G[Point to Host IP]
    E --> H[Setup www]
    F --> I[Setup Email]
```

## Common Configurations

1. **Basic Website**

```
example.com       A     192.168.1.10
www.example.com   CNAME example.com
```

2. **Email Setup**

```
example.com       MX    mail.example.com (10)
mail.example.com  A     192.168.1.20
```

3. **Subdomain Setup**

```
blog.example.com  A     192.168.1.30
shop.example.com  A     192.168.1.40
```

## Best Practices

- Use A records for apex domain
- Use CNAME for subdomains
- Set appropriate TTL
- Regular DNS audits
- Backup DNS records

---

## Types of Hosting

```mermaid
flowchart TD
    subgraph "Shared Hosting"
        SH[Server]
        SH --> W1[Website 1]
        SH --> W2[Website 2]
        SH --> W3[Website 3]
    end

    subgraph "VPS Hosting"
        VPS[Physical Server]
        VPS --> V1[Virtual Server 1]
        VPS --> V2[Virtual Server 2]
        V1 --> VW1[Website 1]
        V2 --> VW2[Website 2]
    end

    subgraph "Dedicated Hosting"
        DH[Physical Server]
        DH --> DW1[Single Website]
    end

    subgraph "Cloud Hosting"
        CH[Cloud Infrastructure]
        CH --> S1[Server 1]
        CH --> S2[Server 2]
        CH --> S3[Server 3]
        S1 --> CW1[Website]
        S2 --> CW1
        S3 --> CW1
    end
```
