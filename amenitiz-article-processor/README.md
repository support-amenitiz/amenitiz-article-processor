# 📚 Amenitiz Article Processor

> AI-powered Help Center article creation with automatic translation to 5 languages and beautiful HTML formatting

Automate your Amenitiz Help Center article creation with GPT-4o. Submit 1-5 articles for merging/improvement, get back professionally formatted articles in **English, French, Italian, Spanish, and Portuguese** - all created as drafts in Intercom.

[![n8n](https://img.shields.io/badge/n8n-workflow-orange)](https://n8n.io)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-blue)](https://openai.com)
[![Intercom](https://img.shields.io/badge/Intercom-API-brightgreen)](https://intercom.com)

---

## ✨ Features

- 🤖 **AI-Powered Processing**: Merge up to 5 articles or improve a single article using GPT-4o
- 🌍 **5 Languages**: Automatic translation to French (formal), Italian (informal), Spanish (informal), Portuguese (formal)
- 🎨 **Beautiful HTML**: Professional formatting with colored callout boxes (Tips, Warnings, Notes, Important)
- 📝 **Custom Instructions**: Add specific requirements for each submission
- ⚡ **Batch Processing**: Ready to handle 262+ articles efficiently
- 💰 **Cost Effective**: ~$0.15-0.35 per article

---

## 🎯 What It Does

### Input
- **Mode**: Choose "Improve" (1 article) or "Merge" (2-5 articles)
- **Articles**: Paste your article content with title and body
- **Custom Instructions**: Optional specific requirements (e.g., "Add troubleshooting section", "Focus on mobile users")

### Output
Creates **1 Intercom article** with **5 language versions** as DRAFTS:
- 🇬🇧 English (main, British spelling)
- 🇫🇷 French (formal *vous*)
- 🇮🇹 Italian (informal *tu*)
- 🇪🇸 Spanish (informal *tú*)
- 🇵🇹 Portuguese (formal *você*, European)

All with:
- Professional HTML structure
- Colored callout boxes (gray, green, yellow, red, blue)
- Proper spacing and formatting
- SEO descriptions
- Consistent section structure

---

## 📋 Prerequisites

### Required Accounts
1. **n8n instance** (self-hosted or cloud)
2. **OpenAI API key** (GPT-4o access)
3. **Intercom workspace** with API access
4. **Intercom admin account** (for author_id)

### Costs
- **OpenAI**: ~$0.15-0.35 per article (depends on length)
- **n8n**: Free (self-hosted) or cloud pricing
- **Intercom**: Your existing plan

---

## 🚀 Quick Start

### 1. Import n8n Workflow

```bash
# In n8n:
1. Go to Workflows → Import from File
2. Select: workflows/Article_Processor_Workflow.json
3. Activate the workflow
```

### 2. Configure Credentials

**OpenAI Credential:**
```
Name: OpenAI account
Type: OpenAI API
API Key: sk-...your-key...
```

**Intercom Credential:**
```
Name: Intercom account
Type: Intercom API
Access Token: Your Intercom API token
```

### 3. Update Author ID

In the **"Prepare Intercom Body"** code node, update line 8:
```javascript
author_id: '50046499',  // ← Replace with YOUR Intercom admin ID
```

**How to find your ID:**
1. Go to n8n workflow
2. Add HTTP Request node temporarily
3. GET: `https://api.intercom.io/me`
4. Auth: Your Intercom credential
5. Header: `Intercom-Version: 2.11`
6. Execute and copy your `id`

### 4. Update Webhook URL

In `article-processor.html`, update line 15:
```javascript
const webhookUrl = 'https://YOUR-N8N-INSTANCE/webhook/article-processor';
```

### 5. Deploy HTML Form

**Option A: Host on your server**
```bash
# Upload article-processor.html to your web server
# Access via: https://yoursite.com/article-processor.html
```

**Option B: Use GitHub Pages**
```bash
# Push to GitHub
# Enable GitHub Pages in repo settings
# Access via: https://yourusername.github.io/amenitiz-article-processor/article-processor.html
```

**Option C: Local use**
```bash
# Just open the HTML file in your browser
open article-processor.html
```

---

## 📖 Usage Guide

### Step 1: Choose Mode

**Improve Mode** (1 article)
- Enhances structure, clarity, formatting
- Adds missing sections
- Improves readability

**Merge Mode** (2-5 articles)
- Combines multiple articles into one cohesive piece
- Removes duplicates
- Creates logical flow

### Step 2: Fill In Details

**Required:**
- Title (max 255 chars)
- Category (e.g., "Booking Engine")
- Subcategory (e.g., "Payments")
- Article content (title + body for each)

**Optional:**
- Custom Instructions (max 500 chars)

### Step 3: Submit

- Processing time: **90-150 seconds**
- Status messages will appear
- Success shows Intercom article link

### Step 4: Review in Intercom

1. Click the article link
2. Review all 5 language versions
3. Make any final edits
4. Publish when ready

---

## 🎨 HTML Formatting

All articles include:

### Structure
```html
<p><strong>SEO Description</strong></p>
<p>&nbsp;</p>
<h2>Section Heading</h2>
<p>Content here...</p>
<p>&nbsp;</p>
```

### Colored Callout Boxes

**💡 Tip** (green) - Best practices, shortcuts
```html
<div style="background-color: #e8f5e9; padding: 15px; border-radius: 5px; margin: 15px 0;">
<p>💡 <strong>Tip</strong></p>
<p>Tip content here</p>
</div>
```

**⚠️ Warning** (red) - Destructive actions
```html
<div style="background-color: #ffebee; padding: 15px; border-radius: 5px; margin: 15px 0;">
<p>⚠️ <strong>Warning</strong></p>
<p>Warning content here</p>
</div>
```

**📝 Note** (yellow) - Additional context
**ℹ️ Important** (blue) - Prerequisites
**📋 Example** (gray) - Real-world samples

---

## 🔧 Workflow Architecture

```
┌─────────────────┐
│ Webhook Trigger │
└────────┬────────┘
         │
         ▼
    ┌────────┐
    │ IF: Mode│
    └─┬────┬─┘
      │    │
  Merge  Improve
      │    │
      ▼    ▼
    ┌──────────────┐
    │ GPT-4o       │
    │ Processing   │
    └──────┬───────┘
           │
           ▼
    ┌──────────────┐
    │ GPT-4o       │
    │ Translate    │
    │ + HTML Format│
    └──────┬───────┘
           │
           ▼
    ┌──────────────┐
    │ Parse        │
    │ Translations │
    └──────┬───────┘
           │
           ▼
    ┌──────────────┐
    │ Prepare      │
    │ Intercom Body│
    └──────┬───────┘
           │
           ▼
    ┌──────────────┐
    │ Create in    │
    │ Intercom API │
    └──────┬───────┘
           │
           ▼
    ┌──────────────┐
    │ Respond to   │
    │ Webhook      │
    └──────────────┘
```

### Node Details

| Node | Type | Purpose |
|------|------|---------|
| Webhook | Trigger | Receives form submissions |
| Check if Merge | IF | Routes to Merge or Improve |
| Message a model (Merge) | OpenAI | Merges 2-5 articles |
| Message a model1 (Improve) | OpenAI | Improves single article |
| Message a model2 (Translate) | OpenAI | Translates + formats HTML |
| Parse Translations | Code | Extracts language sections |
| Prepare Intercom Body | Code | Builds API request |
| Create in Intercom | HTTP | POST to Intercom API |
| Respond to Webhook | Webhook Response | Returns result to form |

---

## 🌍 Language Specifications

| Language | Formality | Tone | Example |
|----------|-----------|------|---------|
| 🇬🇧 English | British | Professional | "organise", "colour" |
| 🇫🇷 French | Formal (vous) | Professional | "Vous pouvez configurer..." |
| 🇮🇹 Italian | Informal (tu) | Friendly | "Puoi configurare..." |
| 🇪🇸 Spanish | Informal (tú) | Friendly | "Puedes configurar..." |
| 🇵🇹 Portuguese | Formal (você) | Professional | "Você pode configurar..." |

### Standard Section Headers

| English | French | Italian | Spanish | Portuguese |
|---------|--------|---------|---------|------------|
| Overview | Aperçu | Panoramica | Descripción general | Visão geral |
| Before you start | Avant de commencer | Prima di iniziare | Antes de empezar | Antes de começar |
| Step-by-step instructions | Instructions étape par étape | Istruzioni passo passo | Instrucciones paso a paso | Instruções passo a passo |
| Troubleshooting / FAQs | Dépannage / FAQ | Risoluzione problemi / FAQ | Solución de problemas / FAQ | Resolução de problemas / FAQ |
| Related articles | Articles connexes | Articoli correlati | Artículos relacionados | Artigos relacionados |

---

## 🔍 Troubleshooting

### "Bad request - please check your parameters"

**Solution:** Update your `author_id` in the "Prepare Intercom Body" node.

### "JSON parameter needs to be valid JSON"

**Solution:** Make sure the "Create in Intercom" node is using:
- Specify Body: **Using JSON**
- JSON field: `={{ $json.requestBody }}`

### Translations not appearing

**Solution:** Check Parse Translations output for all 5 languages (body_en, body_fr, body_it, body_es, body_pt).

### Processing takes too long (>3 min)

**Possible causes:**
- OpenAI API rate limits
- Very long articles (>5000 words)
- Network issues

**Solution:** Check n8n execution logs.

### HTML not rendering properly

**Check:**
1. GPT output has proper HTML tags (not markdown)
2. No ```html markers in output
3. Intercom isn't stripping inline styles

---

## 📊 Performance

### Processing Times
- **1 article improve**: 60-90 seconds
- **2-5 articles merge**: 90-150 seconds

### Token Usage (GPT-4o)
- **Merge**: ~8,000-15,000 tokens
- **Improve**: ~5,000-10,000 tokens
- **Translate**: ~10,000-20,000 tokens

### Costs Per Article
- **Small** (< 500 words): $0.15-0.20
- **Medium** (500-1500 words): $0.20-0.30
- **Large** (> 1500 words): $0.30-0.35

---

## 🛠️ Customization

### Add New Language

1. Update Translation node prompt
2. Add new parsing in Parse Translations code
3. Add new language to Intercom body

### Change Callout Colors

Update the `style=""` attributes in the Translation node prompt:
```html
background-color: #YOUR-HEX-COLOR;
```

### Modify Article Structure

Edit the Translation node prompt to change:
- Section order
- Required sections
- Formatting rules

---

## 📁 Repository Structure

```
amenitiz-article-processor/
├── README.md                          # This file
├── article-processor.html             # HTML form
├── workflows/
│   └── Article_Processor_Workflow.json # n8n workflow export
├── docs/
│   ├── SETUP-GUIDE.md                 # Detailed setup
│   ├── OPENAI-NODE-CONFIG.md          # GPT-4o config
│   └── FINAL-SYSTEM-SUMMARY.md        # Complete specs
└── LICENSE                            # MIT License
```

---

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📄 License

MIT License - feel free to use and modify for your needs.

---

## 🆘 Support

**Issues?** Open a GitHub issue with:
- Description of the problem
- n8n execution logs
- GPT response (if applicable)
- Intercom API error (if applicable)

---

## 🎉 Success Story

**Amenitiz Help Center**: 262 articles processed and translated in record time, now serving customers across 9 markets in their native languages.

---

## 🔗 Related Projects

- [n8n](https://n8n.io) - Workflow automation
- [OpenAI GPT-4o](https://openai.com) - AI language model
- [Intercom](https://intercom.com) - Customer messaging platform

---

## 📝 Changelog

### v1.0.0 (2024-12-04)
- ✨ Initial release
- 🌍 5-language translation support
- 🎨 HTML formatting with callout boxes
- 🔄 Merge/Improve modes
- 📝 Custom instructions field

---

**Made with ❤️ for the Amenitiz Support Team**

*Transforming customer support, one article at a time.*
