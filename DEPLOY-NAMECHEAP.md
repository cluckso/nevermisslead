# Deploy Website to Namecheap Domain (nevermisslead-ai.com)

This guide walks you through deploying your website to your Namecheap domain.

## Prerequisites

- ✅ Domain purchased on Namecheap: `nevermisslead-ai.com`
- ✅ Website files ready (`index.html`, `styles.css`, `script.js`)
- ✅ Namecheap account access

## Deployment Options

### Option 1: Namecheap Hosting (Easiest - Recommended)

If you purchased hosting with your domain:

#### Step 1: Access cPanel

1. Log into [Namecheap](https://www.namecheap.com)
2. Go to **Account** → **Domain List**
3. Find `nevermisslead-ai.com`
4. Click **Manage** next to hosting (if you have hosting)
5. Click **cPanel** button
6. Log into cPanel

#### Step 2: Upload Files via File Manager

1. In cPanel, find **Files** section
2. Click **File Manager**
3. Navigate to `public_html` folder (this is your website root)
4. Delete default files (if any): `index.html`, `cgi-bin`, etc.
5. Click **Upload** button
6. Upload all your website files:
   - `index.html`
   - `styles.css`
   - `script.js`
7. Make sure `index.html` is in the root of `public_html`

#### Step 3: Verify

1. Visit `http://nevermisslead-ai.com` (or `https://` if SSL is enabled)
2. Your website should be live!

---

### Option 2: Free Hosting (Netlify/Vercel) + Namecheap DNS

**Best for**: Free hosting with easy updates

#### Step 1: Deploy to Netlify

1. **Create Netlify Account**
   - Go to [netlify.com](https://netlify.com)
   - Sign up (free)

2. **Deploy Site**
   - Drag and drop your `website` folder onto Netlify dashboard
   - OR connect GitHub repository
   - Netlify will give you a URL like: `https://random-name.netlify.app`

3. **Test the Netlify URL**
   - Make sure your site works on the Netlify URL

#### Step 2: Configure Namecheap DNS

1. **Log into Namecheap**
   - Go to [namecheap.com](https://www.namecheap.com)
   - Account → Domain List
   - Click **Manage** next to `nevermisslead-ai.com`

2. **Go to Advanced DNS**
   - Click **Advanced DNS** tab

3. **Add DNS Records**
   - Delete any existing A records for `@` (root domain)
   - Add new A record:
     - **Type**: A Record
     - **Host**: `@`
     - **Value**: `75.2.60.5` (Netlify's IP - check Netlify docs for current IP)
     - **TTL**: Automatic
   
   - Add CNAME record for `www`:
     - **Type**: CNAME Record
     - **Host**: `www`
     - **Value**: `random-name.netlify.app` (your Netlify site URL)
     - **TTL**: Automatic

4. **Configure Netlify Custom Domain**
   - In Netlify dashboard → Site settings → Domain management
   - Add custom domain: `nevermisslead-ai.com`
   - Add `www.nevermisslead-ai.com`
   - Netlify will provide DNS instructions (use these instead of above if different)

5. **Wait for DNS Propagation**
   - Can take 24-48 hours (usually 1-2 hours)
   - Check with: [whatsmydns.net](https://www.whatsmydns.net)

#### Step 3: Enable SSL (Automatic with Netlify)

- Netlify automatically provides free SSL certificates
- Your site will be available at `https://nevermisslead-ai.com`

---

### Option 3: GitHub Pages + Namecheap DNS

**Best for**: Free hosting with version control

#### Step 1: Create GitHub Repository

1. Create new repository on GitHub
2. Upload your website files
3. Go to repository **Settings** → **Pages**
4. Select source branch (usually `main`)
5. GitHub will give you URL: `https://username.github.io/repo-name`

#### Step 2: Configure Namecheap DNS

1. **Log into Namecheap**
   - Domain List → Manage → Advanced DNS

2. **Add CNAME Record**
   - **Type**: CNAME Record
   - **Host**: `@` (or `www`)
   - **Value**: `username.github.io` (your GitHub Pages URL)
   - **TTL**: Automatic

3. **Configure GitHub Pages Custom Domain**
   - In repository Settings → Pages
   - Add custom domain: `nevermisslead-ai.com`
   - GitHub will verify DNS

#### Step 3: Enable SSL

- GitHub Pages provides free SSL
- Enable in repository Settings → Pages → Enforce HTTPS

---

### Option 4: VPS/Cloud Hosting (DigitalOcean, AWS, etc.)

**Best for**: Full control, custom backend

#### Step 1: Set Up Server

1. Create VPS instance (DigitalOcean, AWS, etc.)
2. Install web server (Nginx or Apache)
3. Upload website files to `/var/www/html` (or similar)

#### Step 2: Configure Namecheap DNS

1. **Get Server IP**
   - Note your VPS IP address

2. **Configure DNS in Namecheap**
   - Add A Record:
     - **Host**: `@`
     - **Value**: Your VPS IP address
     - **TTL**: Automatic
   - Add A Record for `www`:
     - **Host**: `www`
     - **Value**: Your VPS IP address
     - **TTL**: Automatic

#### Step 3: Set Up SSL (Let's Encrypt)

```bash
# Install Certbot
sudo apt install certbot python3-certbot-nginx

# Get SSL certificate
sudo certbot --nginx -d nevermisslead-ai.com -d www.nevermisslead-ai.com
```

---

## Recommended: Netlify Deployment (Easiest)

**Why Netlify?**
- ✅ Free hosting
- ✅ Free SSL
- ✅ Easy updates (drag & drop or Git)
- ✅ Fast CDN
- ✅ Automatic deployments

### Quick Netlify Setup:

1. **Go to [netlify.com](https://netlify.com)** and sign up
2. **Drag your `website` folder** onto Netlify dashboard
3. **Get your Netlify URL** (e.g., `https://amazing-site-123.netlify.app`)
4. **In Netlify Dashboard:**
   - Site settings → Domain management
   - Add custom domain: `nevermisslead-ai.com`
   - Follow Netlify's DNS instructions

5. **In Namecheap:**
   - Advanced DNS tab
   - Add the DNS records Netlify provides
   - Usually:
     - A Record: `@` → Netlify IP
     - CNAME: `www` → Netlify site URL

6. **Wait 1-2 hours** for DNS propagation
7. **Visit `https://nevermisslead-ai.com`** - Your site is live!

---

## DNS Configuration Details

### Namecheap Advanced DNS Settings

When you go to Advanced DNS, you'll see records like:

```
Type    Host    Value                    TTL
A       @       192.0.2.1               Automatic
CNAME   www     example.com             Automatic
```

**For Netlify:**
```
Type    Host    Value                              TTL
A       @       75.2.60.5                         Automatic
CNAME   www     your-site.netlify.app             Automatic
```

**For GitHub Pages:**
```
Type    Host    Value                    TTL
CNAME   @       username.github.io      Automatic
```

**For VPS:**
```
Type    Host    Value              TTL
A       @       YOUR_VPS_IP       Automatic
A       www     YOUR_VPS_IP       Automatic
```

---

## SSL Certificate Setup

### With Netlify/Vercel
- ✅ Automatic - they provide free SSL
- ✅ Just add custom domain and wait

### With Namecheap Hosting
1. In cPanel → **SSL/TLS Status**
2. Install free SSL (Let's Encrypt)
3. Enable **Force HTTPS Redirect**

### With VPS
- Use Let's Encrypt (free) - see Option 4 above

---

## Testing Your Deployment

1. **Check DNS Propagation**
   - Visit [whatsmydns.net](https://www.whatsmydns.net)
   - Enter `nevermisslead-ai.com`
   - Check if DNS records are propagated globally

2. **Test Website**
   - Visit `http://nevermisslead-ai.com`
   - Visit `https://nevermisslead-ai.com` (if SSL enabled)
   - Test all pages and features

3. **Check Mobile Responsiveness**
   - Test on phone
   - Use browser dev tools (F12 → Mobile view)

---

## Troubleshooting

### Website Not Loading

1. **Check DNS Propagation**
   - Wait 24-48 hours for full propagation
   - Use [whatsmydns.net](https://www.whatsmydns.net) to check

2. **Verify DNS Records**
   - Make sure A/CNAME records are correct
   - Check TTL values

3. **Check File Upload**
   - Verify `index.html` is in root directory
   - Check file permissions (should be 644)

### SSL Not Working

1. **Wait for SSL Certificate**
   - Can take a few hours to provision

2. **Check SSL Status**
   - In hosting panel, check SSL/TLS status
   - Enable "Force HTTPS Redirect"

### 404 Errors

1. **Check File Names**
   - Make sure `index.html` is lowercase
   - Verify all file paths are correct

2. **Check .htaccess** (if using Apache)
   - May need to configure rewrite rules

---

## Next Steps After Deployment

1. ✅ **Test Contact Form**
   - Set up form backend (Formspree, Netlify Forms, or custom API)

2. ✅ **Set Up Analytics**
   - Add Google Analytics
   - Or use Netlify Analytics (paid)

3. ✅ **Set Up Email**
   - Configure email forwarding in Namecheap
   - Or use email service (Google Workspace, etc.)

4. ✅ **SEO Optimization**
   - Submit sitemap to Google Search Console
   - Add meta tags (already in HTML)

5. ✅ **Monitor Performance**
   - Use Google PageSpeed Insights
   - Optimize images if needed

---

## Quick Reference

| Service | Cost | Difficulty | Best For |
|---------|------|------------|----------|
| Namecheap Hosting | $1-5/month | Easy | Simple sites |
| Netlify | Free | Very Easy | Static sites |
| GitHub Pages | Free | Easy | Developers |
| VPS | $5-20/month | Hard | Full control |

**Recommendation**: Start with **Netlify** (free, easy, fast)

---

**Your website will be live at `https://nevermisslead-ai.com` once DNS propagates!** 🚀
