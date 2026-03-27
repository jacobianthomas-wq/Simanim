# Simanim — Setup Guide

## Project Structure

```
simanim/
├── index.html              ← Homepage
├── book.html               ← Dynamic book page (reads from content/)
├── netlify.toml            ← Netlify config
├── admin/
│   ├── index.html          ← Decap CMS admin panel
│   └── config.yml          ← CMS content model
├── content/
│   └── books/
│       └── yehoshua.md     ← One .md file per sefer
└── static/
    └── uploads/            ← Images, PDFs uploaded via CMS
```

---

## Step 1 — Push to GitHub

1. Create a new repo at https://github.com/new
   - Name it `simanim` (or whatever you like)
   - Set it to **Public** (required for free Netlify)

2. In your terminal:
```bash
cd path/to/simanim
git init
git add .
git commit -m "Initial Simanim site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/simanim.git
git push -u origin main
```

---

## Step 2 — Deploy on Netlify

1. Go to https://netlify.com and sign in (use your GitHub account)
2. Click **"Add new site" → "Import an existing project"**
3. Choose **GitHub** and select your `simanim` repo
4. Build settings:
   - Build command: *(leave blank)*
   - Publish directory: `.`
5. Click **Deploy site**

Your site will be live at a URL like `https://random-name-123.netlify.app`

**Custom domain:** In Netlify → Domain settings → Add custom domain → type `simanim.com` (or whatever you own) and follow the DNS instructions.

---

## Step 3 — Enable the CMS (Decap CMS)

### 3a. Enable Netlify Identity
1. In Netlify dashboard → **Identity** tab → Click **"Enable Identity"**
2. Under **Registration** → set to **"Invite only"** (so only you can log in)
3. Under **External providers** → Enable **GitHub** login (optional but easy)

### 3b. Enable Git Gateway
1. In Netlify → Identity → **Services** → Click **"Enable Git Gateway"**
   - This lets the CMS commit to your GitHub repo when you save content

### 3c. Invite yourself as admin
1. In Netlify → Identity → **Invite users**
2. Enter your email → Send invite
3. Check your email and accept the invite — set a password

---

## Step 4 — Log into the Admin Panel

1. Go to `https://your-site.netlify.app/admin`
2. Log in with the email/password you set
3. You'll see the **Simanim CMS** — a UI to manage all book content

---

## Step 5 — Add a Book

In the CMS admin panel:
1. Click **"📚 Books"** → **"New Book"**
2. Fill in:
   - English title (e.g. `Shoftim`)
   - Hebrew title
   - Section (Nevi'im Rishonim / Acharonim / Kesuvim)
   - Order number
   - Number of perakim
   - Description
   - Hebrew watermark letter
   - Video URL (YouTube/Vimeo)
   - Siman image (upload)
   - Memory story (rich text editor)
   - PDFs (upload)
   - Quiz questions
   - Toggle **Published** to ON
3. Click **Save** → Netlify auto-deploys in ~30 seconds

---

## Step 6 — Link books from Homepage

In `index.html`, book tags link like this:
```html
<a href="book.html?book=yehoshua" class="book-tag">Yehoshua</a>
<a href="book.html?book=shoftim" class="book-tag">Shoftim</a>
```

The slug must match the filename in `content/books/` (e.g. `shoftim.md`).

---

## Adding More Books

Just add a new `.md` file to `content/books/` — either via the CMS or directly in GitHub.
The `book.html` page will load any book by its slug in the URL: `book.html?book=SLUG`

---

## Giving Others Admin Access

In Netlify → Identity → Invite users → enter their email.
They'll get an invite link and can log into `/admin` to add/edit content.
