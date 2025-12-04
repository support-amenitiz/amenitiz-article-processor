# 🚀 GitHub Deployment Guide

## Step 1: Create GitHub Repository

### Option A: Via GitHub Website

1. Go to https://github.com/new
2. Fill in:
   - **Repository name**: `amenitiz-article-processor`
   - **Description**: "AI-powered Help Center article processor with 5-language translation"
   - **Visibility**: Public or Private (your choice)
   - **Initialize**: DO NOT add README, .gitignore, or license (we already have them)
3. Click **"Create repository"**

### Option B: Via GitHub CLI

```bash
gh repo create amenitiz-article-processor --public --description "AI-powered Help Center article processor"
```

---

## Step 2: Upload Files to GitHub

### Option A: Using Git Commands

```bash
# Navigate to the repository folder
cd amenitiz-article-processor

# Initialize git repository
git init

# Add all files
git add .

# Create first commit
git commit -m "Initial commit: Article Processor v1.0"

# Add GitHub remote (replace YOUR-USERNAME)
git remote add origin https://github.com/YOUR-USERNAME/amenitiz-article-processor.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Option B: Upload via GitHub Website

1. Go to your new repository on GitHub
2. Click **"uploading an existing file"**
3. Drag and drop all files/folders from `amenitiz-article-processor/`
4. Add commit message: "Initial commit: Article Processor v1.0"
5. Click **"Commit changes"**

---

## Step 3: Enable GitHub Pages (Optional - for HTML form hosting)

1. Go to repository **Settings**
2. Scroll to **Pages** (in left sidebar)
3. Under **Source**, select:
   - Branch: `main`
   - Folder: `/ (root)`
4. Click **Save**
5. Wait 1-2 minutes
6. Your form will be available at:
   ```
   https://YOUR-USERNAME.github.io/amenitiz-article-processor/article-processor.html
   ```

### Update Webhook URL in HTML

After GitHub Pages is live, update `article-processor.html` line 15:

```javascript
// If using GitHub Pages:
const webhookUrl = 'https://YOUR-N8N-INSTANCE/webhook/article-processor';

// If hosting elsewhere:
const webhookUrl = 'https://your-server.com/webhook/article-processor';
```

Commit and push the change:
```bash
git add article-processor.html
git commit -m "Update webhook URL"
git push
```

---

## Step 4: Add Topics/Tags (Recommended)

In your GitHub repository:

1. Click **⚙️ Settings** (top right, next to About)
2. Add topics:
   - `n8n`
   - `openai`
   - `intercom`
   - `automation`
   - `translation`
   - `help-center`
   - `customer-support`

---

## Step 5: Create Releases (Optional)

### Tag Your First Release

```bash
# Create and push a tag
git tag -a v1.0.0 -m "Release v1.0.0: Initial release"
git push origin v1.0.0
```

### Create Release on GitHub

1. Go to **Releases** (right sidebar)
2. Click **"Create a new release"**
3. Fill in:
   - **Tag**: v1.0.0
   - **Release title**: Article Processor v1.0.0
   - **Description**:
     ```
     ## 🎉 Initial Release
     
     - 🌍 5-language translation support (EN, FR, IT, ES, PT)
     - 🎨 Beautiful HTML formatting with callout boxes
     - 🔄 Merge mode (2-5 articles) and Improve mode (1 article)
     - 📝 Custom instructions field
     - ⚡ Ready for batch processing of 262+ articles
     
     ## 📦 What's Included
     - n8n workflow JSON
     - HTML form for submissions
     - Complete documentation
     - Setup guides
     ```
4. Click **"Publish release"**

---

## Step 6: Add Repository Description

On your repository main page, click ✏️ **Edit** next to the repository name:

**Short description:**
```
AI-powered Help Center article processor: Merge/improve articles, translate to 5 languages, format with beautiful HTML
```

**Website (if using GitHub Pages):**
```
https://YOUR-USERNAME.github.io/amenitiz-article-processor/article-processor.html
```

---

## Step 7: Share Your Repository

### Repository URL
```
https://github.com/YOUR-USERNAME/amenitiz-article-processor
```

### Share With Your Team

Send them:
1. **Repository link** for code access
2. **GitHub Pages link** (if enabled) for the form
3. **README.md** for setup instructions

---

## 🎯 Quick Command Summary

```bash
# Clone your repo (after creating it)
git clone https://github.com/YOUR-USERNAME/amenitiz-article-processor.git

# Navigate to folder
cd amenitiz-article-processor

# Make changes, then:
git add .
git commit -m "Your commit message"
git push

# Create new release
git tag -a v1.1.0 -m "Release v1.1.0: Description"
git push origin v1.1.0
```

---

## 🔒 Security Checklist

Before pushing to GitHub, make sure:

- [ ] No API keys in files
- [ ] No Intercom tokens in files
- [ ] No OpenAI API keys in files
- [ ] Webhook URL is placeholder or your actual URL (not sensitive)
- [ ] No internal server URLs exposed

**Note:** Your workflow JSON contains credential IDs but NOT the actual credentials themselves - this is safe to share.

---

## 📱 Optional: Add Social Preview

1. Create an image (1280x640px) showing your tool
2. In repository **Settings → Social Preview**
3. Upload your image

---

## ✅ Done!

Your Article Processor is now live on GitHub! 🎉

**Next steps:**
- Share with your team
- Accept contributions
- Create issues for bugs/features
- Build a community!
