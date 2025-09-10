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

## Images

1. Create S3 Bucket

<img width="1576" height="734" alt="Image" src="https://github.com/user-attachments/assets/3c7674d1-b8f7-4560-bc2b-03284b14d17a" />

2. Index.html File upload

<img width="1599" height="712" alt="Image" src="https://github.com/user-attachments/assets/310c4e99-3429-43d0-9cd8-f09d7a6164a7" />

3. File uploaded

<img width="1580" height="708" alt="Image" src="https://github.com/user-attachments/assets/bc6df53d-fbc3-4cd8-a13c-b6dbc12d5358" />

4. Enable webhosting

<img width="1580" height="693" alt="Image" src="https://github.com/user-attachments/assets/5f3eb891-7581-48fd-adc1-be2edbe4c53c" />

5. Bucket policy

<img width="1591" height="729" alt="Image" src="https://github.com/user-attachments/assets/d7a3b496-b0b1-4864-bf9e-a71f105e5553" />

6. Bucket End point

<img width="1599" height="618" alt="Image" src="https://github.com/user-attachments/assets/8bf54250-5ad0-400b-acb1-bd0925206dcb" />

7. Output

<img width="1499" height="528" alt="Image" src="https://github.com/user-attachments/assets/fe1efbea-bc68-4602-8688-91b91506ad30" />
👉 Visit the URL to see your website live.

✅ Conclusion

Using AWS S3 Static Website Hosting provides a fast, simple, and cost-effective way to host static websites without managing web servers.

