# ⚡ Quick Reference Guide

One-page cheat sheet for the Amenitiz Article Processor.

---

## 🚀 5-Minute Setup

1. **Import workflow** → n8n → Import from File → `workflows/Article_Processor_Workflow.json`
2. **Add OpenAI credential** → API key → Save
3. **Add Intercom credential** → Access token → Save
4. **Update author_id** → "Prepare Intercom Body" node → Your admin ID
5. **Update webhook URL** → `article-processor.html` → Your n8n URL
6. **Deploy form** → Upload HTML or open locally
7. **Test!** → Submit an article

---

## 📋 Quick Commands

### Find Your Intercom Admin ID
```bash
# In n8n, create temp HTTP Request node:
GET https://api.intercom.io/me
Header: Intercom-Version: 2.11
Auth: Your Intercom credential
# Copy the "id" from response
```

### Test Webhook Locally
```bash
curl -X POST https://YOUR-N8N/webhook/article-processor \
  -H "Content-Type: application/json" \
  -d '{"mode":"improve","article1_title":"Test","article1_body":"Test body"}'
```

### Check n8n Logs
```bash
# In n8n UI:
Executions → Click failed execution → View detailed logs
```

---

## 🎯 Form Fields

| Field | Type | Required | Max Length | Notes |
|-------|------|----------|------------|-------|
| Mode | Select | ✅ | - | Improve or Merge |
| Article Count | Number | ✅ (Merge) | 2-5 | Only in Merge mode |
| Title | Text | ✅ | 255 | Article title |
| Category | Text | ✅ | 100 | e.g., "Booking Engine" |
| Subcategory | Text | ✅ | 100 | e.g., "Payments" |
| Custom Instructions | Textarea | ❌ | 500 | Optional guidance |
| Article Title | Text | ✅ | 255 | For each article |
| Article Body | Textarea | ✅ | - | For each article |

---

## 🌍 Language Output

| Language | Code | Formality | You/Tu/Vous |
|----------|------|-----------|-------------|
| English | en | British | - |
| French | fr | Formal | vous |
| Italian | it | Informal | tu |
| Spanish | es | Informal | tú |
| Portuguese | pt | Formal (EU) | você |

---

## 🎨 HTML Elements Generated

### Structure
```html
<p><strong>SEO description</strong></p>
<p>&nbsp;</p>                    <!-- Spacing -->
<h2>Section Heading</h2>
<p>Paragraph content</p>
<ul><li>List item</li></ul>
<ol><li>Numbered item</li></ol>
<a href="#">Link</a>
```

### Callout Boxes
```html
<!-- Tip (green) -->
<div style="background-color: #e8f5e9; padding: 15px; border-radius: 5px; margin: 15px 0;">
  <p>💡 <strong>Tip</strong></p>
  <p>Content here</p>
</div>

<!-- Warning (red) -->
<div style="background-color: #ffebee; ...">⚠️ <strong>Warning</strong></div>

<!-- Note (yellow) -->
<div style="background-color: #fff9c4; ..."><strong>Note</strong></div>

<!-- Important (blue) -->
<div style="background-color: #e3f2fd; ..."><strong>Important</strong></div>

<!-- Example (gray) -->
<div style="background-color: #f5f5f5; ..."><strong>Example</strong></div>
```

---

## 📊 Processing Times & Costs

| Task | Time | Tokens | Cost |
|------|------|--------|------|
| Improve 1 article | 60-90s | 5k-10k | $0.15-0.20 |
| Merge 2 articles | 90-120s | 8k-15k | $0.20-0.30 |
| Merge 5 articles | 120-150s | 15k-20k | $0.30-0.35 |

**Total for 262 articles**: ~$40-90

---

## 🔧 Workflow Node IDs

| Node | ID (for debugging) |
|------|-------------------|
| Webhook | webhook-trigger-1 |
| Check if Merge | if-mode-check |
| Merge GPT | message-model-merge |
| Improve GPT | message-model1-improve |
| Translate GPT | message-model2-translate |
| Parse | parse-translations |
| Prepare Body | prepare-intercom-body |
| Create Article | create-intercom |
| Respond | respond-webhook |

---

## ⚠️ Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `Bad request - author_id` | Wrong/missing ID | Update author_id in code node |
| `JSON parameter needs...` | Body format wrong | Use "Using JSON" mode |
| `Empty body_en` | GPT not outputting | Check translation prompt |
| `Timeout` | Processing too long | Check OpenAI API status |
| `Unauthorized` | Wrong credentials | Re-add API keys |

---

## 🎯 Testing Checklist

- [ ] Workflow imported and active
- [ ] OpenAI credential added
- [ ] Intercom credential added
- [ ] Author ID updated
- [ ] Webhook URL updated in HTML
- [ ] Test: Improve 1 article
- [ ] Test: Merge 2 articles
- [ ] Check all 5 languages created
- [ ] Verify HTML formatting in Intercom
- [ ] Confirm callout boxes render

---

## 📞 Quick Support

**Issue**: Article not created
**Check**: n8n execution logs → Error message

**Issue**: Wrong language
**Check**: Parse Translations output → Verify all 5 bodies

**Issue**: No HTML formatting
**Check**: GPT output → Should be HTML, not markdown

**Issue**: Slow processing
**Check**: Article length → Split if >5000 words

---

## 🔗 Key URLs

| Resource | URL |
|----------|-----|
| n8n Docs | https://docs.n8n.io |
| OpenAI API | https://platform.openai.com/docs |
| Intercom API | https://developers.intercom.com/docs/build-an-integration/learn-more/rest-apis/api-versions |
| This Repo | https://github.com/YOUR-USERNAME/amenitiz-article-processor |

---

## 📝 Credentials Format

### OpenAI (in n8n)
```
Type: OpenAI API
API Key: sk-proj-...your-key...
```

### Intercom (in n8n)
```
Type: Intercom API  
Access Token: dG9rOmNmY...your-token...
```

---

## 🎨 Customization Quick Hacks

**Change callout colors**: Edit Translation node prompt → Update `background-color: #HEX`

**Add new section**: Edit Translation node prompt → Add to structure

**Change formality**: Edit Translation node prompt → Update vous/tu/tú/você

**Disable callouts**: Edit Translation node prompt → Remove callout examples

**Add 6th language**: 
1. Update Translation prompt
2. Update Parse Translations code
3. Update Prepare Body code

---

## ✅ Pre-Push Checklist

- [ ] No API keys in files
- [ ] No tokens in files
- [ ] Webhook URL is placeholder
- [ ] Author ID is placeholder
- [ ] .gitignore present
- [ ] README updated
- [ ] CHANGELOG updated

---

## 🚀 Deployment Steps

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR-USERNAME/amenitiz-article-processor.git
git push -u origin main
```

---

**Pro tip**: Bookmark this page for quick reference! 🔖
