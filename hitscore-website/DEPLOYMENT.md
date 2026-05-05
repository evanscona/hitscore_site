# HitScore AI — Deployment Guide
# gethitscore.com on Vercel + Squarespace domain

## STEP 1: Deploy to Vercel (Free)

1. Go to vercel.com → Sign up / Log in with GitHub
2. Click "Add New Project"
3. Upload the website folder OR connect a GitHub repo:

   **Option A — Direct Upload:**
   - Install Vercel CLI: `npm install -g vercel`
   - In terminal, navigate to the hitscore-website folder:
     `cd hitscore-website`
   - Run: `vercel deploy`
   - Follow prompts — select "no framework"
   - Vercel gives you a URL like: `hitscore-website.vercel.app`

   **Option B — GitHub:**
   - Create a new GitHub repo
   - Push the hitscore-website folder contents to it
   - In Vercel, Import that repo
   - Auto-deploys on every push

## STEP 2: Add Custom Domain on Vercel

1. In Vercel dashboard → your project → Settings → Domains
2. Add: `gethitscore.com` and `www.gethitscore.com`
3. Vercel gives you DNS records — note them down:
   - Type: A, Name: @, Value: 76.76.21.21
   - Type: CNAME, Name: www, Value: cname.vercel-dns.com

## STEP 3: Point Squarespace Domain to Vercel

1. Log into Squarespace → Domains → gethitscore.com → DNS Settings
2. Delete existing A records and CNAME for www
3. Add new records:
   - A Record: Host = @, Points to = 76.76.21.21
   - CNAME: Host = www, Points to = cname.vercel-dns.com
4. Save — DNS propagates in 1-48 hours
5. Back in Vercel → Domains → it will show "Valid" once live

## STEP 4: 301 Redirect from Carrd

In Carrd (hitscore.carrd.co):
1. Go to your site → Settings → Publishing
2. Add a custom redirect or use Carrd's "Redirect" element
3. If Carrd doesn't support redirects on free plan:
   - Add a meta refresh to your Carrd index page:
   `<meta http-equiv="refresh" content="0; url=https://www.gethitscore.com">`
   - Or use Cloudflare Redirect Rules if your domain is on Cloudflare

## STEP 5: Set Up Custom Email Addresses

Use Cloudflare Email Routing (FREE):

1. Your domain must be on Cloudflare (or add it)
2. Cloudflare Dashboard → Email Routing → Enable
3. Add routing rules:
   - support@gethitscore.com → forward to your personal Gmail
   - legal@gethitscore.com → forward to your personal Gmail
   - privacy@gethitscore.com → forward to your personal Gmail
4. Verify your Gmail address when prompted
5. Done — emails to those addresses land in your Gmail inbox

Alternative (paid): Google Workspace ($6/mo) gives you full send/receive.

## STEP 6: Final Checklist

- [ ] All 4 pages load on gethitscore.com
- [ ] www.gethitscore.com redirects to gethitscore.com
- [ ] hitscore.carrd.co redirects to gethitscore.com
- [ ] All mailto: links work (test each one)
- [ ] Logo shows in browser tab (favicon)
- [ ] App store buttons point to correct App Store URLs
- [ ] All internal page links work (Terms ↔ Privacy ↔ Support)
- [ ] SSL certificate is active (shows 🔒 in browser)

## FILE STRUCTURE

hitscore-website/
├── index.html        ← Home page
├── terms.html        ← Terms of Service
├── privacy.html      ← Privacy Policy
├── support.html      ← Support + FAQ
└── assets/
    ├── logo.png      ← App icon (used in nav + footer)
    ├── image1.png    ← Hero mockup (center, featured)
    ├── image2.png    ← Planner screen
    ├── image3.png    ← Trends screen
    ├── image4.png    ← Tools screen
    ├── apple.png     ← App Store button
    └── google.png    ← Google Play button

## TO ACTIVATE APP STORE BUTTONS

Once your app is live, find your App Store ID:
1. Go to App Store Connect → your app → App Information
2. Copy the Apple ID number (e.g., 1234567890)

Update in index.html — find the store buttons and replace #:
  Apple: href="https://apps.apple.com/app/id1234567890"
  Google: href="https://play.google.com/store/apps/details?id=com.hitscoreai.app"
