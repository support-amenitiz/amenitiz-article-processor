# 🚀 SIMPLE ARTICLE PROCESSOR - SETUP GUIDE

## 📋 Overview

This is a MUCH simpler system than the Notion-based version. You get:

1. **Web form** (React artifact) - paste articles, choose merge/improve
2. **n8n webhook workflow** - processes everything automatically
3. **Creates in Intercom** - English + 4 translations (FR, IT, ES, PT)

**Processing time:** ~60-90 seconds per article

---

## 🎯 PART 1: Set Up n8n Workflow

### Step 1: Open Your Workflow

1. Go to n8n
2. Find workflow: **"Article Processor - Simple Webhook"**
3. Workflow ID: `O18duWx02JWGK5g1`

### Step 2: Add Credentials

You need to add credentials to 4 nodes:

#### **Node 1: OpenAI: Merge Articles**
- Click on the node
- Click "Credential to connect with"
- Add your OpenAI API key
- Get it from: https://platform.openai.com/api-keys

#### **Node 2: OpenAI: Improve Article**
- Same as above - add OpenAI API key

#### **Node 3: OpenAI: Translate**
- Same as above - add OpenAI API key

#### **Node 4: Create in Intercom**
- Click on the node
- Click "Credential to connect with"
- Add your Intercom API token
- Get it from: Intercom → Settings → Developer Hub → Developer Access Token
- Required scopes: `articles:read`, `articles:write`

### Step 3: Activate the Workflow

1. Click the **"Active"** toggle in the top right
2. The workflow turns blue when active

### Step 4: Get Your Webhook URL

1. Click on the **"Webhook Trigger"** node
2. Look for "Production URL" or "Test URL"
3. Copy the URL - it looks like:
   ```
   https://your-n8n-instance.com/webhook/article-processor
   ```
4. **SAVE THIS URL** - you need it for the web form!

---

## 🎨 PART 2: Set Up Web Form

### Option A: Use in Claude Artifacts (Easiest)

1. The React form is already created as an artifact
2. Just update the webhook URL:
   - Find this line: `const WEBHOOK_URL = 'https://your-n8n-instance.com/webhook/article-processor';`
   - Replace with your actual webhook URL from Part 1, Step 4
3. Done! Use the form directly in this conversation

### Option B: Host It Yourself

1. Copy the React code from `/mnt/user-data/outputs/article-submission-form.jsx`
2. Update the webhook URL (same as above)
3. Deploy to:
   - **Vercel** (free, easiest)
   - **Netlify** (free)
   - **GitHub Pages** (free)
   - Or run locally with `npx create-react-app`

---

## 🧪 PART 3: Test It!

### Test with a Simple Article

1. Open the web form
2. Select **"Improve Article"**
3. Fill in:
   - **Title:** "How to reset your password"
   - **Category:** "Account Settings"
   - **Subcategory:** "Security"
   - **Article Content:** Paste a short article (200-500 words)
4. Click **"Improve & Translate"**
5. Wait 60-90 seconds
6. You should see: "Article processed successfully!"
7. Click the Intercom link to view your article

### What to Check in Intercom

Go to Intercom → Articles → Your new article

**Verify:**
- ✅ English version is there (DRAFT status)
- ✅ Click the language dropdown - you should see FR, IT, ES, PT
- ✅ All translations are complete
- ✅ All translations are in DRAFT status
- ✅ Article structure follows the template

---

## 📝 PART 4: How to Use

### For Single Articles (Improve)

1. Go to Intercom
2. Copy the article content you want to improve
3. Open the web form
4. Select **"Improve Article"**
5. Paste the content
6. Fill in title, category, subcategory
7. Submit
8. Wait for the result
9. Review in Intercom

### For Merging 2 Articles

1. Go to Intercom
2. Copy BOTH articles you want to merge
3. Open the web form
4. Select **"Merge Articles"**
5. Paste Article 1 in the first box
6. Paste Article 2 in the second box
7. Fill in the NEW title for the merged article
8. Submit
9. Wait for the result
10. Review in Intercom

---

## 🔧 Workflow Details

### The Flow

```
📥 Webhook receives form data
    ↓
🔀 Check: Merge or Improve?
    ↓
🤖 OpenAI: Merge (if merge) OR Improve (if single)
    ↓
🌍 OpenAI: Translate to FR, IT, ES, PT
    ↓
📊 Parse all 5 versions (EN + 4 translations)
    ↓
📤 Create article in Intercom with all languages
    ↓
✅ Send success response back to form
```

### Processing Time

- **Improve:** ~60 seconds
- **Merge:** ~90 seconds
- *Depends on article length and OpenAI API speed*

### What Gets Created in Intercom

Every submission creates **1 article with 5 language versions:**

1. **English** (main, DRAFT)
2. **French** (linked, DRAFT, formal "vous")
3. **Italian** (linked, DRAFT, informal "tu")
4. **Spanish** (linked, DRAFT, informal "tú")
5. **Portuguese** (linked, DRAFT, formal "você")

All are created as **DRAFTS** so you can review before publishing.

---

## ⚠️ Troubleshooting

### "Error: Failed to fetch"
- Check that n8n workflow is **ACTIVE** (blue toggle)
- Verify webhook URL is correct in the form
- Check your n8n instance is reachable

### "Article created but missing translations"
- Check OpenAI API key is valid
- Check you have GPT-4o access
- Look at the workflow execution in n8n to see where it failed

### "Intercom API error"
- Check Intercom token is valid
- Verify token has `articles:write` permission
- Check the Intercom-Version header is `2.11`

### Translations are in the wrong language
- The prompts enforce the correct formality
- If wrong, check the OpenAI: Translate node prompt
- Make sure you're using `gpt-4o` model (not 3.5)

### Form shows "Processing..." forever
- Check n8n workflow execution logs
- Look for errors in the OpenAI nodes
- Verify all credentials are set

---

## 💰 Cost Estimates

**OpenAI API Costs (GPT-4o):**
- Improve article: ~$0.05-0.10 per article
- Merge articles: ~$0.08-0.15 per merge
- Translation: ~$0.05-0.10 per set
- **Total per article: ~$0.10-0.25**

For 262 articles: **~$26-65 total**

*Much cheaper than your previous estimate because we're not using Claude!*

---

## 🎯 What's Different from the Notion Version?

### ✅ SIMPLER
- No Notion database setup
- No complex "Related Article database" relations
- No status tracking
- Just paste & go!

### ✅ FASTER
- No fetching from Notion
- No updating status back to Notion
- Direct webhook → process → Intercom

### ✅ CHEAPER
- Using OpenAI GPT-4o instead of Claude
- ~60% cheaper per article

### ❌ What You Lose
- No batch processing (do one at a time)
- No automatic Notion tracking
- Manual copy/paste from Intercom

---

## 📚 Article Template

All articles follow this structure:

```
SEO Description (max 255 chars)

## Overview
[What the article covers]

## Before you start
[Prerequisites, or "No prerequisites required."]

## Step-by-step instructions
1. [Action verb first]
2. [Next step]
3. [Continue...]

## Troubleshooting / FAQs
- **[Issue]** — [Solution]
- **[Edge case]** — [Resolution]

## Related articles
- [Related article 1]
- [Related article 2]
```

### Style Rules
- ✅ British English (colour, organise, analyse)
- ✅ Professional but approachable
- ✅ Clear navigation paths (Settings → Pricing → Rates)
- ❌ NO EMOJIS EVER
- ❌ No marketing language
- ❌ No vague instructions ("simply", "just", "easily")

### Terminology
- **Guest** (not customer)
- **Property** (not hotel)
- **→** for navigation
- **Booking Engine** (Amenitiz's system)

---

## 🚀 Ready to Go!

1. ✅ Add credentials to n8n workflow
2. ✅ Activate the workflow
3. ✅ Copy the webhook URL
4. ✅ Update the web form with webhook URL
5. ✅ Test with one article
6. ✅ Process your 262 articles!

**Estimated time for 262 articles:**
- If processing one at a time: ~3-4 hours
- You can run multiple browser tabs in parallel to speed up!

---

## 📞 Need Help?

Check the n8n execution logs:
1. Go to n8n → Executions
2. Click on the latest execution
3. See exactly where it failed
4. Each node shows input/output data

**Common fixes:**
- Node shows red X → credential issue
- Stuck on OpenAI node → API key issue or rate limit
- Stuck on Intercom node → API token issue

---

## 🎉 You're Done!

This system is MUCH simpler than the Notion version. Just paste articles, click submit, and get back perfect multilingual Help Center content!

**Files Created:**
- `/mnt/user-data/outputs/article-submission-form.jsx` - React form
- n8n workflow: "Article Processor - Simple Webhook" (ID: O18duWx02JWGK5g1)

**Next Steps:**
1. Configure credentials in n8n
2. Get webhook URL
3. Update form
4. Start processing! 🚀
