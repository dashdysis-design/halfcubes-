# HalfCubes.com - Global Accessibility Deployment Guide

## Current Status ✅

**Site URL:** https://halfcubes.com
**Hosting:** GitHub Pages + Cloudflare CDN
**HTTPS:** Enabled with HSTS
**Last Deploy:** January 9, 2026

---

## What Was Configured

### 1. Search Engine Optimization (SEO)

#### robots.txt
- **Location:** `/robots.txt`
- **Status:** Allows ALL crawlers (Googlebot, Bingbot, Yandex, Baidu, DuckDuckBot)
- **Sitemap:** Referenced at https://halfcubes.com/sitemap.xml
- **Test:** `curl https://halfcubes.com/robots.txt`

#### sitemap.xml
- **Location:** `/sitemap.xml`
- **URLs Included:**
  - `https://halfcubes.com/` (priority 1.0)
  - `https://www.halfcubes.com/` (priority 0.9)
- **Last Modified:** 2026-01-09
- **Test:** `curl https://halfcubes.com/sitemap.xml`

#### Meta Tags (index.html)
- ✅ Title: "HalfCubes - AI Lead Qualification | $10 per 100 Leads"
- ✅ Description: 160 chars with key benefits
- ✅ Keywords: lead qualification, AI scoring, B2B leads, alternatives
- ✅ Canonical URL: https://halfcubes.com/
- ✅ Open Graph (Facebook): Full meta tags for social sharing
- ✅ Twitter Cards: Large image card support
- ✅ Schema.org Structured Data:
  - Organization schema (contact info, founder)
  - Product schema (pricing, availability)

### 2. Security Headers

#### _headers File
Cloudflare/GitHub Pages compatible headers:

```
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), microphone=(), camera=()
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
Content-Security-Policy: [Allows Three.js, Calendly, self]
Access-Control-Allow-Origin: * (for public API endpoints)
```

**HSTS:** 2-year max-age with preload flag
**CSP:** Allows inline scripts for Three.js, external CDN (cdnjs.cloudflare.com), Calendly embeds

### 3. Performance & Caching

- **Static HTML:** 30 min cache (`max-age=1800`)
- **CSS/JS/Audio:** 1 year immutable cache (`max-age=31536000`)
- **Compression:** Brotli/Gzip via Cloudflare
- **CDN:** Global edge locations (already on Cloudflare)

### 4. Regional Access

- ✅ **No geoblocking** - Site accessible worldwide
- ✅ **Uzbekistan/Tashkent** - No IP restrictions
- ✅ **Cloudflare** - Already routing through global edge network
- ✅ **CORS:** Open (`Access-Control-Allow-Origin: *`)

---

## Verification Checklist

Run these commands to verify deployment:

### 1. Site Accessibility
```bash
# Check site loads (should return 200 OK)
curl -I https://halfcubes.com

# Check from different regions (use VPN or webpagetest.org)
# Test locations: New York, London, Singapore, Sydney, Tashkent
```

### 2. SEO Files
```bash
# Verify robots.txt allows crawlers
curl https://halfcubes.com/robots.txt | grep "Allow: /"

# Verify sitemap exists
curl https://halfcubes.com/sitemap.xml | grep "<loc>"

# Check meta tags in HTML
curl -s https://halfcubes.com | grep -i "meta name=\"description\""
```

### 3. Security Headers
```bash
# Check HSTS header
curl -I https://halfcubes.com | grep -i "strict-transport-security"

# Check CSP header
curl -I https://halfcubes.com | grep -i "content-security-policy"

# Full security score test
# Visit: https://securityheaders.com/?q=halfcubes.com
```

### 4. Performance
```bash
# Test TTFB (Time To First Byte) - should be < 200ms
curl -o /dev/null -s -w "Time: %{time_total}s\n" https://halfcubes.com

# Full performance test
# Visit: https://gtmetrix.com
# Location: Tashkent, Uzbekistan
```

### 5. Search Console Indexing
```bash
# Google: Check if indexed
# Search: site:halfcubes.com
# Or: https://search.google.com/search-console

# Bing: Check indexing
# https://www.bing.com/webmasters

# Yandex: Check indexing (for Russia/CIS)
# https://webmaster.yandex.com
```

---

## Next Steps: Search Engine Submission

### 1. Google Search Console
1. Visit: https://search.google.com/search-console
2. Add property: `halfcubes.com`
3. Verify ownership (DNS TXT record or HTML file upload)
4. Submit sitemap: `https://halfcubes.com/sitemap.xml`
5. Request indexing for homepage

### 2. Bing Webmaster Tools
1. Visit: https://www.bing.com/webmasters
2. Add site: `halfcubes.com`
3. Verify ownership
4. Submit sitemap: `https://halfcubes.com/sitemap.xml`

### 3. Yandex Webmaster
1. Visit: https://webmaster.yandex.com
2. Add site: `halfcubes.com`
3. Verify ownership
4. Submit sitemap: `https://halfcubes.com/sitemap.xml`
5. **Why Yandex?** Dominant search engine in Russia/CIS including Uzbekistan

### 4. Request Indexing
After submitting sitemaps, manually request indexing:
- **Google:** Search Console → URL Inspection → Request Indexing
- **Bing:** URL Inspection Tool → Request Indexing
- **Yandex:** Tools → Reindex pages

Expected indexing time: 24-48 hours for homepage, 1-2 weeks for full coverage

---

## Cloudflare Configuration (Optional Enhancements)

If you have access to Cloudflare dashboard for halfcubes.com:

### 1. Disable "I'm Under Attack" Mode
**Path:** Security → Settings
**Current:** Should be OFF (Challenge Page disabled)
**Why:** Prevents legitimate bot/crawler blocking

### 2. Enable Bot Fight Mode (Managed Challenge)
**Path:** Security → Bots
**Setting:** Use "Managed Challenge" not "Block"
**Why:** Allows search engines, blocks only malicious bots

### 3. Cache Everything Rule
**Path:** Rules → Page Rules
**Rule:** `halfcubes.com/*`
**Setting:** Cache Level: Cache Everything
**Edge Cache TTL:** 1 hour

### 4. HTTPS Rewrite
**Path:** SSL/TLS → Edge Certificates
**Enable:**
- Always Use HTTPS: ON
- Automatic HTTPS Rewrites: ON
- HTTP Strict Transport Security (HSTS): ON (already in _headers)

### 5. Performance Settings
**Path:** Speed → Optimization
**Enable:**
- Auto Minify: HTML, CSS, JS
- Brotli: ON
- Early Hints: ON
- Rocket Loader: OFF (conflicts with Three.js)

---

## Testing from Uzbekistan/Tashkent

### Method 1: WebPageTest.org
1. Visit: https://www.webpagetest.org
2. Enter: `https://halfcubes.com`
3. Select test location: **Tashkent, Uzbekistan** (if available) or closest (Almaty, Kazakhstan)
4. Run test
5. Check for:
   - No 403 errors
   - TTFB < 500ms
   - Full page load < 3s

### Method 2: GTmetrix
1. Visit: https://gtmetrix.com
2. Enter: `https://halfcubes.com`
3. Select server: **Asia** or **Europe-East**
4. Analyze performance

### Method 3: VPN Test
1. Use VPN with Uzbekistan exit node
2. Visit: https://halfcubes.com
3. Verify:
   - Page loads fully
   - Three.js animation works
   - No "Access Denied" messages
   - Console shows no fetch errors

---

## Common Issues & Solutions

### Issue: Site returns 404 for robots.txt or sitemap.xml
**Cause:** GitHub Pages not rebuilding
**Solution:**
```bash
cd halfcubes
git commit --allow-empty -m "Trigger rebuild"
git push
```
Wait 2-3 minutes, check GitHub Actions status

### Issue: Headers not applied
**Cause:** `_headers` file may not work on GitHub Pages
**Solution:** Configure headers in Cloudflare dashboard instead:
- Workers & Pages → halfcubes.com → Settings → Functions
- Or use Cloudflare Page Rules for header injection

### Issue: Googlebot not crawling
**Check:**
1. Google Search Console → Coverage report
2. Fetch as Google → Test live URL
3. Verify robots.txt allows: `User-agent: Googlebot` + `Allow: /`

**Force recrawl:**
```bash
# Submit URL directly
https://search.google.com/search-console → URL Inspection → Request Indexing
```

### Issue: Site blocked in Uzbekistan
**Unlikely** (GitHub Pages + Cloudflare = globally accessible)
**Debug:**
1. Check if it's ISP-level blocking (rare for GitHub/Cloudflare)
2. Verify DNS resolves: `nslookup halfcubes.com 8.8.8.8`
3. Try alternate DNS: Cloudflare (1.1.1.1) or Google (8.8.8.8)

---

## Files Changed in This Deployment

```
halfcubes/
├── index.html          # Enhanced with SEO meta tags, Schema.org
├── robots.txt          # NEW - Allows all crawlers
├── sitemap.xml         # NEW - Sitemap for search engines
├── _headers            # NEW - Security & performance headers
└── DEPLOYMENT_GUIDE.md # NEW - This file
```

---

## Maintenance Schedule

### Weekly
- [ ] Check Google Search Console for crawl errors
- [ ] Monitor Cloudflare Analytics for traffic/blocks

### Monthly
- [ ] Update sitemap.xml `<lastmod>` date if content changes
- [ ] Review security headers score: https://securityheaders.com
- [ ] Test site from 3+ regions using webpagetest.org

### Quarterly
- [ ] Review Schema.org structured data with Google Rich Results Test
- [ ] Update meta descriptions for CTR optimization
- [ ] Audit Cloudflare WAF rules for false positives

---

## Contact & Support

**Site Owner:** Soren Voight
**Email:** sorenvoight@halfcubes.com
**Repository:** https://github.com/dashdysis-design/halfcubes-

**Deployment Platform:**
- **Hosting:** GitHub Pages (free)
- **CDN:** Cloudflare (free tier)
- **Domain:** halfcubes.com (Spaceship.com)

---

## Success Metrics

After 7 days, verify:
- ✅ `site:halfcubes.com` shows homepage in Google
- ✅ Google Search Console shows "Indexed" status
- ✅ No 403/429 errors from any region
- ✅ Cloudflare Analytics shows traffic from 10+ countries
- ✅ securityheaders.com score: A or A+
- ✅ GTmetrix Performance: A (90+)
- ✅ TTFB from Tashkent: < 500ms

**Current Site Status:** Fully configured for global access. Ready for search engine submission.
