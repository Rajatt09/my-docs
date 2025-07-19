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

---

## Hosting a Website on S3 with a Custom Domain (`app.rajat.com`)

You can host a website using S3 and map it to your custom domain in two ways:

- **Option 1: HTTP only (no SSL, no CloudFront)**

- **Option 2: HTTPS (secure, using CloudFront + SSL certificate)**

       [However you can use directly http via cloudfront]

---

#### Note (Read it)

` While using cloudfront you can't directly point app.rajat.com to CName or url of your cloudfront. (These platforms act as fully managed hosting providers.)`

- **_When you add a CNAME like: `app.rajat.com` → `your-app.onrender.com`
  They handle everything else for you :)_**

**CloudFront is not a hosting service. It’s just a CDN/reverse proxy provided by AWS.**
With CloudFront, you’re the sysadmin. AWS gives you raw power — but you must explicitly tell CloudFront:

- What domain to accept

- What SSL cert to use

- How to route traffic

If you don’t configure all this manually, it won’t “just work.”

---

### `(Below things Can vary it is just an overview)`

### - Option 1: Host with **HTTP Only** (No CloudFront)

**Steps**

1. **Enable Static Website Hosting in S3**

   - Open your S3 bucket (must be named `app.rajat.com`)
   - Go to **Properties > Static website hosting**
   - Enable it and set `index.html` as the index document

2. **Make the Bucket Public**

   - Use this bucket policy to allow public access:
     ```json
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Principal": "*",
           "Action": "s3:GetObject",
           "Resource": "arn:aws:s3:::app.rajat.com/*"
         }
       ]
     }
     ```

3. **Add a CNAME in Your DNS Provider (e.g., GoDaddy)**

   - Go to DNS settings for your domain
   - Add a CNAME record:
     ```
     Name: app
     Value: app.rajat.com.s3-website-ap-south-1.amazonaws.com
     ```
     _(Replace `ap-south-1` with your actual AWS region)_

4. Done! Now you can open `http://app.rajat.com` in your browser.

**Note**

- This works only with **HTTP** (not secure).
- Browsers may show "Not Secure" in the address bar.
- Not recommended for login pages, forms, or private data.

---

### - Option 2: Host with **HTTPS** using CloudFront

If you want your site to load securely at `https://app.rajat.com`, follow these steps:

**Steps**

1. **Create an SSL Certificate**

   - Go to [AWS Certificate Manager (ACM)](https://console.aws.amazon.com/acm/home)
   - Choose **us-east-1** region
   - Request a public certificate for `app.rajat.com`
   - Validate ownership via DNS (you’ll get a CNAME to add in GoDaddy)

2. **Create a CloudFront Distribution**

   - Set the **origin** as your S3 bucket
   - In **Alternate Domain Names (CNAMEs)**, enter `app.rajat.com`
   - Attach the SSL certificate you created in ACM
   - Set Viewer Protocol Policy to “Redirect HTTP to HTTPS”

3. **Update DNS in GoDaddy**

   - Go to your domain’s DNS
   - Add a CNAME:
     ```
     Name: app
     Value: <your-cloudfront-id>.cloudfront.net
     ```

4. Done! Now `https://app.rajat.com` will securely load your S3 website.

---
