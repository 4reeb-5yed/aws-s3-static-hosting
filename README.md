# AWS S3 Static Website Hosting

A simple static webpage hosted on Amazon S3 using its static website hosting feature — no servers, no backend, no database. Built as a hands-on introduction to core AWS concepts: object storage, public access policies, and static content delivery.

**Live URL:** `[paste your S3 website endpoint here after deployment]`

---

## Architecture

The browser sends an HTTP GET request to the S3 static website endpoint. Inside the bucket, a bucket policy checks that the request is a public read, then S3 returns the requested object — `index.html` on success, or `error.html` if the page doesn't exist.

```
Browser --GET request--> S3 Bucket [Bucket Policy: public GetObject]
                              |
                    ┌─────────┴─────────┐
                index.html          error.html
              (200 OK, found)     (404, not found)
                              |
Browser <---- returns page ---┘
```

**Components used:**
- **S3 bucket** — object storage for the site files
- **Static website hosting** — S3 feature that serves `index.html`/`error.html` directly, no server needed
- **Bucket policy** — grants public *read-only* access (`s3:GetObject`), nothing is publicly writable

**Cost:** $0 — entirely within the AWS Free Tier.

---

## Steps taken

1. Created an S3 bucket with a globally unique name, in region `[your region]`
2. Uploaded `index.html` and `error.html` to the bucket
3. Enabled **Static website hosting** under the bucket's Properties tab, set `index.html` as the index document and `error.html` as the error document
4. Added a bucket policy allowing public `s3:GetObject` access, scoped only to this bucket
5. Verified the site loads at the generated website endpoint
6. Verified error handling by visiting a non-existent path and confirming `error.html` renders

---

## Screenshots

| Step | Screenshot |
|---|---|
| Bucket created | ![Bucket created](screenshots/01-bucket-created.png) |
| Static hosting enabled | ![Static hosting enabled](screenshots/02-static-hosting-enabled.png) |
| Bucket policy | ![Bucket policy](screenshots/03-bucket-policy.png) |
| Website endpoint | ![Website endpoint](screenshots/04-website-endpoint.png) |
| Live site | ![Live site](screenshots/05-live-site.png) |

*(AWS Account ID and any billing details are cropped out of all screenshots for privacy.)*

---

## What I learned

- How S3's static website hosting differs from just storing files in a bucket
- How bucket policies work, and how to scope permissions to exactly what's needed (public read, nothing else)
- How to verify a deployment properly, not just assume it works — including testing the error path

---

## Repo structure

```
aws-s3-static-hosting/
├── site/
│   ├── index.html
│   └── error.html
├── screenshots/
└── README.md
```

---

## Contact

- GitHub: [4reeb-5yed](https://github.com/4reeb-5yed)
- LinkedIn: [areeb-syed](https://www.linkedin.com/in/areeb-syed-b19491245)
- Email: 4reeb.5yed@gmail.com
