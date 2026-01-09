# Search Engine Submission Instructions

## Immediate Actions Required

### 1. Google Search Console (Priority: CRITICAL)

**Purpose:** Get halfcubes.com indexed by Google (95% of search traffic)

**Steps:**
1. Visit: https://search.google.com/search-console
2. Sign in with: sorenvoight@gmail.com
3. Click "Add Property"
4. Select "URL prefix" property type
5. Enter: `https://halfcubes.com`

**Verify Ownership (Choose One Method):**

#### Option A: HTML File Upload (Easiest)
1. Download verification file (e.g., `google1234567890abcdef.html`)
2. Add file to halfcubes repository root
3. Commit and push:
   ```bash
   cd halfcubes
   git add google*.html
   git commit -m "Add Google Search Console verification"
   git push
   ```
4. Wait 2 minutes for deployment
5. Click "Verify" in Search Console

#### Option B: DNS TXT Record
1. Get TXT record value from Search Console
2. Log into Spaceship.com (halfcubes.com domain registrar)
3. Add DNS TXT record:
   - Type: TXT
   - Name: @
   - Value: `google-site-verification=XXXXXXX`
4. Wait 5-10 minutes for DNS propagation
5. Click "Verify" in Search Console

**After Verification:**
1. Submit sitemap:
   - Sitemaps → Add a new sitemap
   - Enter: `sitemap.xml`
   - Click "Submit"
2. Request indexing:
   - URL Inspection → Enter: `https://halfcubes.com`
   - Click "Request Indexing"
3. Expected result: "Indexed" status within 24-48 hours

---

### 2. Bing Webmaster Tools (Priority: HIGH)

**Purpose:** Index on Bing + powers DuckDuckGo, Yahoo, Ecosia (5-10% of traffic)

**Steps:**
1. Visit: https://www.bing.com/webmasters
2. Sign in with: sorenvoight@gmail.com (or Microsoft account)
3. Click "Add a site"
4. Enter: `https://halfcubes.com`

**Verify Ownership:**
- **Easy Method:** Import from Google Search Console
  - Click "Import from Google Search Console"
  - Authorize access
  - Site will be auto-verified
- **Manual Method:** Same as Google (HTML file or DNS TXT)

**After Verification:**
1. Submit sitemap:
   - Sitemaps → Submit Sitemap
   - Enter: `https://halfcubes.com/sitemap.xml`
2. Submit URL:
   - URL Submission → Submit URL
   - Enter: `https://halfcubes.com`
3. Expected result: Indexed within 48-72 hours

---

### 3. Yandex Webmaster (Priority: HIGH for Uzbekistan)

**Purpose:** Dominant search engine in Russia, CIS countries, and Uzbekistan

**Steps:**
1. Visit: https://webmaster.yandex.com
2. Sign in or create Yandex account
3. Click "Add site"
4. Enter: `https://halfcubes.com`

**Verify Ownership:**
- **Recommended:** Meta tag method
  1. Copy meta tag: `<meta name="yandex-verification" content="XXXXX" />`
  2. Add to halfcubes/index.html in `<head>` section:
     ```html
     <meta name="yandex-verification" content="XXXXX" />
     ```
  3. Commit and push
  4. Click "Verify" in Yandex Webmaster
- **Alternative:** DNS TXT record (same process as Google)

**After Verification:**
1. Submit sitemap:
   - Indexing → Sitemap files
   - Add: `https://halfcubes.com/sitemap.xml`
2. Reindex pages:
   - Tools → Reindex pages
   - Enter: `https://halfcubes.com`
3. **Enable regional settings:**
   - Settings → Regional settings
   - Select: Uzbekistan (if targeting)
4. Expected result: Indexed within 3-7 days

---

### 4. Baidu Webmaster Tools (Optional - for China)

**Purpose:** If targeting Chinese market (requires Chinese phone number)

**Steps:**
1. Visit: https://ziyuan.baidu.com
2. Register with Chinese phone number
3. Add site: `https://halfcubes.com`
4. Verify ownership (meta tag or file upload)
5. Submit sitemap

**Note:** Baidu requires ICP license for .com domains hosted in China. Since halfcubes.com is on GitHub Pages (US), indexing may be limited.

---

## Automated Indexing Services

### IndexNow (Instant Indexing)

**Purpose:** Submit URLs to Bing, Yandex instantly (no waiting)

**Steps:**
1. Generate API key:
   ```bash
   openssl rand -hex 32
   # Example: a1b2c3d4e5f6...
   ```
2. Create key file:
   ```bash
   cd halfcubes
   echo "YOUR_API_KEY" > a1b2c3d4e5f6.txt
   git add a1b2c3d4e5f6.txt
   git commit -m "Add IndexNow API key"
   git push
   ```
3. Submit URL to IndexNow:
   ```bash
   curl -X POST "https://api.indexnow.org/indexnow" \
     -H "Content-Type: application/json" \
     -d '{
       "host": "halfcubes.com",
       "key": "YOUR_API_KEY",
       "keyLocation": "https://halfcubes.com/YOUR_API_KEY.txt",
       "urlList": [
         "https://halfcubes.com/"
       ]
     }'
   ```

**Result:** Bing and Yandex will crawl within minutes instead of days

---

## Monitoring & Verification

### Week 1 Checklist

**Day 1 (Today):**
- [x] robots.txt deployed ✅
- [x] sitemap.xml deployed ✅
- [x] SEO meta tags live ✅
- [ ] Submit to Google Search Console
- [ ] Submit to Bing Webmaster Tools
- [ ] Submit to Yandex Webmaster

**Day 2:**
- [ ] Check Google Search Console: Coverage report
- [ ] Check Bing: URL Inspection
- [ ] Test IndexNow submission (if implemented)

**Day 3:**
- [ ] Google search: `site:halfcubes.com`
  - Expected: Homepage appears in results
- [ ] Bing search: `site:halfcubes.com`
- [ ] Yandex search: `site:halfcubes.com`

**Day 7:**
- [ ] Google Search Console: Check impressions/clicks
- [ ] Verify indexed pages: Should show 1+ pages
- [ ] Test accessibility from Uzbekistan (VPN or ask contact)

### Month 1 Goals

- **Google:** Homepage indexed, 10+ impressions/day
- **Bing:** Homepage indexed, 2+ impressions/day
- **Yandex:** Homepage indexed (critical for Uzbekistan)
- **No geoblocking:** Accessible from 50+ countries
- **Security score:** A+ on securityheaders.com

---

## Testing Regional Access

### Test from Uzbekistan/Tashkent

#### Method 1: WebPageTest (Free)
1. Visit: https://www.webpagetest.org
2. URL: `https://halfcubes.com`
3. Location: Select "Tashkent" or nearest (Almaty, Kazakhstan)
4. Click "Start Test"
5. **Success Criteria:**
   - HTTP Status: 200 OK
   - TTFB: < 1000ms
   - Page fully loads
   - No 403/429 errors

#### Method 2: GTmetrix (Free)
1. Visit: https://gtmetrix.com
2. URL: `https://halfcubes.com`
3. Server: Select "Asia - Mumbai" (closest to Uzbekistan)
4. Analyze
5. **Success Criteria:**
   - Performance: B or higher
   - Structure: A
   - Load time: < 3s

#### Method 3: VPN Test (Requires VPN)
1. Connect to VPN with Uzbekistan or Kazakhstan exit node
2. Visit: https://halfcubes.com
3. Open browser console (F12)
4. **Success Criteria:**
   - Page loads fully
   - Three.js animation works
   - No "Access Denied" errors
   - No console errors about blocked resources

#### Method 4: Ask Local Contact
Best verification method:
1. Send link to someone in Uzbekistan/Tashkent
2. Ask them to visit: https://halfcubes.com
3. Screenshot confirmation

---

## Quick Verification Commands

Run these in terminal to verify everything is working:

```bash
# 1. Check site is accessible
curl -I https://halfcubes.com | grep "200 OK"

# 2. Verify robots.txt allows crawlers
curl -s https://halfcubes.com/robots.txt | grep "Allow: /"

# 3. Verify sitemap exists
curl -s https://halfcubes.com/sitemap.xml | grep "<loc>https://halfcubes.com</loc>"

# 4. Check HSTS header (security)
curl -I https://halfcubes.com | grep "strict-transport-security"

# 5. Check meta description
curl -s https://halfcubes.com | grep "meta name=\"description\""

# 6. Check Schema.org structured data
curl -s https://halfcubes.com | grep "application/ld+json"

# 7. Test from different DNS resolvers (simulates global access)
nslookup halfcubes.com 8.8.8.8     # Google DNS
nslookup halfcubes.com 1.1.1.1     # Cloudflare DNS
nslookup halfcubes.com 77.88.8.8   # Yandex DNS (Russia/CIS)

# 8. Check Cloudflare is routing
curl -I https://halfcubes.com | grep "cf-cache-status"
```

**Expected Results:** All commands should return data (no errors)

---

## SEO Testing Tools

### Must Use (Free):

1. **Google Rich Results Test**
   - URL: https://search.google.com/test/rich-results
   - Enter: `https://halfcubes.com`
   - Validates Schema.org structured data
   - Expected: Organization + Product schemas detected

2. **Security Headers**
   - URL: https://securityheaders.com
   - Enter: `https://halfcubes.com`
   - Expected score: A or A+

3. **Mobile-Friendly Test**
   - URL: https://search.google.com/test/mobile-friendly
   - Enter: `https://halfcubes.com`
   - Expected: "Page is mobile-friendly"

4. **PageSpeed Insights**
   - URL: https://pagespeed.web.dev
   - Enter: `https://halfcubes.com`
   - Expected: Performance 90+ (desktop), 80+ (mobile)

### Nice to Have:

- **SSL Labs:** https://www.ssllabs.com/ssltest/
- **DNSChecker:** https://dnschecker.org (verify global DNS)
- **Pingdom:** https://tools.pingdom.com (uptime monitoring)

---

## Expected Timeline

| Day | Action | Expected Result |
|-----|--------|-----------------|
| 0 (Today) | Deploy SEO changes | ✅ Complete |
| 1 | Submit to search engines | Verification complete |
| 2-3 | Google starts crawling | URL Inspection shows "Indexed" |
| 3-7 | Bing + Yandex index | `site:halfcubes.com` shows results |
| 7-14 | Organic impressions | Google Search Console shows 10+ daily impressions |
| 14-30 | Full indexing | All pages indexed, ranking for brand name |

**Critical Path:** Google Search Console submission → fastest route to indexing

---

## Troubleshooting

### Issue: robots.txt not updating
```bash
# Force cache clear
curl -H "Cache-Control: no-cache" https://halfcubes.com/robots.txt

# Wait 10 minutes for Cloudflare cache expiry
# Or clear cache in Cloudflare dashboard
```

### Issue: Google says "URL not indexed"
**Check:**
1. Search Console → Coverage → Check errors
2. URL Inspection → See "Why page isn't indexed"
3. Common causes:
   - Crawl not started yet (wait 24-48 hours)
   - robots.txt blocking (verify allows Googlebot)
   - DNS issues (check with `nslookup`)

**Fix:** Request indexing again, submit sitemap again

### Issue: Site blocked in Uzbekistan
**Unlikely** (GitHub + Cloudflare = globally accessible)
**Debug:**
1. Test with VPN
2. Check ISP-level blocking (rare)
3. Verify DNS resolves: `nslookup halfcubes.com`
4. Try alternate DNS: 8.8.8.8 or 1.1.1.1

---

## Contact for Verification

Need someone in Uzbekistan to test?
- Post in freelancer groups
- Use upwork.com ($5 for quick test)
- Or use webpagetest.org with Tashkent location

---

## Summary: Next Steps

**TODAY (30 minutes):**
1. Submit to Google Search Console (10 min)
2. Submit to Bing Webmaster Tools (5 min)
3. Submit to Yandex Webmaster (15 min)

**TOMORROW:**
4. Check Google Search Console for crawl status
5. Run `site:halfcubes.com` in Google/Bing/Yandex

**WEEK 1:**
6. Monitor indexing progress
7. Test from Uzbekistan via webpagetest.org
8. Verify no errors in Search Console

**Status:** Site is fully configured and ready for global access. Just need to submit to search engines!
