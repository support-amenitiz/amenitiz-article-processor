# Changelog

All notable changes to the Amenitiz Article Processor will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Collection/folder support for organizing articles
- Bulk upload via CSV
- Article scheduling
- Preview mode before submission

---

## [1.0.0] - 2024-12-04

### Added
- 🌍 **5-language translation support**
  - English (British, main language)
  - French (formal *vous*)
  - Italian (informal *tu*)
  - Spanish (informal *tú*)
  - Portuguese (formal *você*, European)
- 🎨 **Beautiful HTML formatting**
  - Colored callout boxes (Tips, Warnings, Notes, Important, Examples)
  - Professional structure with proper spacing
  - SEO descriptions
  - Consistent section headers
- 🤖 **AI-powered processing with GPT-4o**
  - Merge mode: Combine 2-5 articles into one cohesive piece
  - Improve mode: Enhance single article structure and clarity
- 📝 **Custom instructions field**
  - Add specific requirements per submission
  - Up to 500 characters
- ⚡ **Batch processing ready**
  - Designed to handle 262+ articles efficiently
  - Processing time: 90-150 seconds per article
- 📊 **Complete documentation**
  - Setup guide
  - OpenAI node configuration
  - System specifications
  - Troubleshooting guide
- 🔄 **n8n workflow automation**
  - Webhook trigger
  - Conditional routing (Merge/Improve)
  - Translation parsing
  - Intercom API integration
- 🎯 **HTML form interface**
  - Clean, user-friendly design
  - Dynamic article fields (1-5 articles)
  - Real-time character counters
  - Loading states and error handling
  - Success message with Intercom link

### Technical Details
- OpenAI model: GPT-4o
- Max tokens: 16,000
- Temperature: 0.3
- Cost per article: ~$0.15-0.35
- Supported Intercom API version: 2.11
- Article state: Draft (all languages)

### Workflow Nodes
1. Webhook Trigger
2. Check if Merge (IF node)
3. Message a model (Merge)
4. Message a model1 (Improve)
5. Message a model2 (Translate + HTML Format)
6. Parse Translations
7. Prepare Intercom Body
8. Create in Intercom
9. Respond to Webhook

### Known Limitations
- Maximum 5 articles per merge
- Custom instructions limited to 500 characters
- Articles created as drafts only (not published)
- No support for article attachments/images
- No collection/folder assignment

### Dependencies
- n8n (self-hosted or cloud)
- OpenAI API (GPT-4o access)
- Intercom workspace with API access

---

## Version History

### Pre-release Development

#### 2024-12-04 - Session 3: HTML Formatting Fix
- Fixed Intercom API 400 error (empty English body)
- Implemented beautiful HTML formatting with styled callout boxes
- Updated translation node to output HTML instead of markdown
- Fixed Parse Translations code to properly extract English content
- Added validation for English content extraction
- Updated Prepare Intercom Body to include author_id
- Added comprehensive HTML formatting specifications

#### 2024-12-04 - Session 2: OpenAI Migration
- Migrated from Notion integration to webhook-based system
- Switched to OpenAI GPT-4o for processing
- Added support for up to 5 articles (previously 2)
- Added custom instructions field
- Created standalone HTML form
- Simplified workflow architecture

#### 2024-12-04 - Session 1: Initial Build
- Built complete Notion integration for 262 articles
- Implemented Intercom article creation
- Established translation workflow
- Created initial documentation

---

## Release Notes Template

```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- New features

### Changed
- Changes to existing functionality

### Deprecated
- Features that will be removed

### Removed
- Removed features

### Fixed
- Bug fixes

### Security
- Security improvements
```

---

[Unreleased]: https://github.com/YOUR-USERNAME/amenitiz-article-processor/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/YOUR-USERNAME/amenitiz-article-processor/releases/tag/v1.0.0
