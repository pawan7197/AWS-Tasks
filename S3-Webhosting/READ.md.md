# ✅ AWS S3 Static Website Hosting Lab

This document explains step-by-step how to host a static website using AWS S3.

---

## 🚀 1️⃣ Create an S3 Bucket

1. Go to the **AWS S3 Console**.
2. Click **Create bucket**.
3. Enter a **unique bucket name** (example: `ajas3bucket2025web`).
4. Choose the appropriate **region**.
5. **Important:**  
   Uncheck **Block all public access** to allow public access to your website.
6. Click **Create bucket**.

---

## 💾 2️⃣ Upload Website Files

1. Open your newly created bucket.
2. Click **Upload** → **Add files** (e.g., `index.html`, `style.css`, etc.).
3. Click **Upload** to store your website files in the bucket.

---

## ⚙️ 3️⃣ Enable Static Website Hosting

1. Go to the bucket **Properties** tab.
2. Scroll to **Static website hosting**.
3. Click **Edit**.
4. Select **Enable**.
5. Enter the following:
   - **Index document:** `index.html`
   - **Error document:** `error.html` (optional)
6. Click **Save changes**.

---

## 🔓 4️⃣ Make Files Public

### Option 1 – Manually:
- Click each file → **Permissions** → **Make public**.

### Option 2 – Set Bucket Policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::ajas3bucket2025web/*"
    }
  ]
}
```

🌐 5️⃣ Access Your Website

After enabling static hosting, the Endpoint URL will appear in the bucket settings, for example:

http://ajas3bucket2025web.s3-website-us-east-1.amazonaws.com


👉 Visit the URL to see your website live.

✅ Conclusion

Using AWS S3 Static Website Hosting provides a fast, simple, and cost-effective way to host static websites without managing web servers.

