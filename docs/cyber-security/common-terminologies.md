# .NET Applications

.NET (pronounced "dot net") is a software development framework by Microsoft that supports building many types of applications:

## Types of Applications Built with .NET

- **Web Applications** – Using ASP.NET
- **Desktop Applications** – Using Windows Forms, WPF
- **Mobile Apps** – Using .NET MAUI or Xamarin
- **Cloud-Based Applications**
- **Games** – Built with Unity
- **IoT Applications**

## Supported Languages

- **C#** (most commonly used)
- **VB.NET**
- **F#**

.NET apps are known for security, structure, and performance.

---

# What is a CMS (Content Management System)?

A CMS is a software tool that helps you create, edit, manage, and publish digital content — usually websites — without writing code.

## Features of a CMS:

- Add or update blog posts
- Upload images and media
- Manage users and permissions
- Change designs via themes/templates
- Extend functionality via plugins (e.g., SEO tools, contact forms)

## Popular CMS Examples:

- WordPress
- Drupal
- Joomla
- Magento (eCommerce)
- Shopify (cloud-based eCommerce CMS)

---

# Web Server vs Application Server

| **Feature**        | **Web Server**                         | **Application Server**                     |
| ------------------ | -------------------------------------- | ------------------------------------------ |
| **Handles**        | Static Content (HTML, CSS, JS, Images) | Dynamic Content (Runs server-side code)    |
| **Executes Code?** | ❌ No                                  | ✅ Yes                                     |
| **Use Case**       | Serves files directly                  | Runs business logic, APIs, database access |
| **Examples**       | Apache, Nginx, IIS                     | Tomcat, JBoss, ASP.NET Core                |

### They Often Work Together:

**Example:**

- Nginx (Web Server) → forwards dynamic requests to → Node.js (Application Server)

---

# Why Use Nginx in Front of Node.js?

| **Reason**              | **Purpose**                                       |
| ----------------------- | ------------------------------------------------- |
| **Reverse Proxy**       | Hides internal details, routes requests           |
| **Load Balancing**      | Distributes traffic to multiple Node.js instances |
| **SSL Termination**     | Handles HTTPS encryption                          |
| **Static File Serving** | More efficient at serving static content          |
| **Security**            | Filters bad requests, rate limits                 |
| **Graceful Restarts**   | Allows restarting Node.js without downtime        |

---

# What is a CDN?

A CDN (Content Delivery Network) is a network of servers around the globe that delivers content to users from the closest server, speeding up load times.

## How It Works:

- **Without CDN** → Content from US → Slow
- **With CDN** → Content from India-based server → Fast

## Delivers:

- Images
- Videos
- JS/CSS files
- Fonts
- Cached HTML pages

## Benefits:

- Faster load times
- Reduced server load
- DDoS protection
- Scalability & availability

## Popular CDN Providers:

- Cloudflare
- Akamai
- Amazon CloudFront
- Google Cloud CDN
- Fastly

---

# Relationship Between Browser, CDN, Web Server & App Server

```
Browser
    ↓
CDN → (serves static content if cached)
    ↓
Web Server → (serves static files or forwards)
    ↓
Application Server → (executes logic, fetches data)
```

---

# Web 1 vs Web 2 vs Web 3

| **Web Generation** | **Key Features**                                 | **Examples**                          |
| ------------------ | ------------------------------------------------ | ------------------------------------- |
| **Web1**           | Static, read-only pages                          | GeoCities, early Yahoo                |
| **Web2**           | Interactive, user-generated content              | Facebook, YouTube, Instagram          |
| **Web3**           | Decentralized, blockchain-based, user-owned data | Crypto wallets, dApps, NFTs (OpenSea) |

### Summary:

- **Web1** = Read-only
- **Web2** = Read + Write (social)
- **Web3** = Decentralized + User ownership

---

# What is AJAX?

AJAX (Asynchronous JavaScript and XML) allows web pages to update data without reloading the entire page.

- Sends background requests to the server.
- Updates only part of a page (like chat messages or form data).
- Used in modern web apps to make them faster and more interactive.

---

# What is XML?

XML (eXtensible Markup Language) is used for storing and transporting data in a structured, readable, and platform-independent format.

## Key Features:

- Self-descriptive
- Hierarchical (tree structure)
- Extensible (custom tags allowed)
- Human-readable
- Cross-platform

### Example:

```xml
<book>
  <title>Learning XML</title>
  <author>John Doe</author>
  <price>29.99</price>
  <availability>In Stock</availability>
</book>
```

---

# XML vs JSON

| **Feature**          | **XML**                 | **JSON**                        |
| -------------------- | ----------------------- | ------------------------------- |
| **Format**           | Tag-based               | Key-value pairs                 |
| **Readability**      | Verbose                 | More concise                    |
| **Custom Tags**      | Allowed                 | Not applicable                  |
| **Attributes**       | Supported               | Not supported (only key-values) |
| **Common Use Cases** | SOAP APIs, Configs, RSS | REST APIs, Data exchange        |

### JSON Version of XML Example:

```json
{
  "book": {
    "title": "Learning XML",
    "author": "John Doe",
    "price": "29.99",
    "availability": "In Stock"
  }
}
```
