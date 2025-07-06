# Managing and Delivering Static Assets

Files that are not plain text (such as `.mp4` videos, `.jpg` images, PDFs, fonts, etc.) are often referred to as **static assets** or **objects**. These are binary files that aren't stored in traditional relational databases. Instead, they are typically stored in object storage systems provided by cloud providers, such as:

-- **_You can also use it for frontends also (not for nextjs as it is server side rendering)_**

-- **_You can use it for backends, since every request returns a different response.Caching does not make any sense there_ --- [You can use `edge networks` (deploy your backend in various servers on internet) but data can't be cached in there. ]**

- **Amazon S3 (AWS)**
- **Google Cloud Storage (GCP)**
- **Azure Blob Storage (Azure)**
- **DigitalOcean Spaces**

These storage services are optimized for:

- **Scalability:** Handling millions of files efficiently.
- **High durability:** Ensuring your assets are safe and reliably stored.
- **Efficient content delivery:** Especially when combined with a Content Delivery Network (CDN) for faster global access.

Using object storage and CDNs together ensures your static assets are delivered quickly and reliably to users, regardless of their location.

---

## Storage

**S3 (Amazon Simple Storage Service)**

- S3 is a cloud-based object storage service from AWS.
- Think of it like Google Drive — you can upload files (like images, videos, or documents), and S3 stores them securely.

(i) When you upload a file, you get a link (URL) back.

(ii) But this link is not publicly accessible by default due to AWS security.

(iii) You need to set permissions or access policies to make the file viewable.

---

**Accessing files directly from S3 can be slow for users far from the server (e.g., users in India accessing a file stored in a U.S. region).**

---

## Distribution

**CDN (Content Delivery Network)** : CloudFront (AWS’s CDN service) comes in — it's used to distribute your S3-stored content globally.

A CDN caches your files on servers (called edge locations) closer to the users.

**Example:** If the original file is at `s3.myapp.aws.com/video.mp4` then CloudFront can serve it from `cdn.myapp.aws.com/video.mp4`

When a user in India requests the file:

- If it’s already cached at an India-based edge server, it serves instantly.

- If not, it fetches from the original S3 link, caches it, and then serves it.

---

**_In Simple Terms,_**

- S3 stores your files.
- CloudFront (CDN) brings them closer to your users, making access faster and more reliable.
