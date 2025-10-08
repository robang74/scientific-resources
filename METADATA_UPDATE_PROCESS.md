# 📋 Metadata Update Process Guide

## 🎯 Purpose
This document provides a step-by-step guide for updating all metadata files and documentation after new paper reviews are added to the repository. Follow this process after each batch of new reviews to maintain consistency across all files.

## 📅 When to Use This Guide
- After new review DOCX files are added to `split-reviews-docx/`
- When the total review count increases (e.g., from 520 to 526+)
- Monthly or periodic repository updates
- After pulling changes that include new reviews

## 🔍 Pre-Update Assessment

### Step 1: Identify New Reviews
```bash
# Navigate to the reviews directory
cd scientific-resources/mike-paper-reviews-500/split-reviews-docx

# Check current highest review number
ls Review_*.docx | tail -5

# Count total reviews
ls Review_*.docx | wc -l
```

### Step 2: Determine Update Scope
Check which files need updating by examining current counts:
- `metadata_22_09_2025/all_paper_titles.txt` (header shows total count)
- `metadata_22_09_2025/reviews_from_208_titles.txt` (last entry number)
- `README.md` (collection statistics)
- `mike-paper-reviews-500/readme.md` (total reviews count)

## 📝 Metadata Files Update Process

### Step 3: Update `reviews_from_208_titles.txt`

**Location:** `metadata_22_09_2025/reviews_from_208_titles.txt`

1. **Extract titles from new reviews:**
```python
# Use Python with docx library to extract titles
import docx
import re

def extract_english_title(file_path):
    doc = docx.Document(file_path)
    # Look for English titles in document content
    # (See detailed extraction code in previous session)

# Extract for each new review: Review_XXX.docx
```

2. **Add new entries:**
- Format: `XXX. [Paper Title]`
- Continue numbering from last entry
- Update header metadata count

### Step 4: Update `all_paper_titles.txt`

**Location:** `metadata_22_09_2025/all_paper_titles.txt`

1. **Update header:**
```markdown
# 📚 Complete Paper Titles from All Mike's Reviews (1-XXX)
# Total: XXX paper titles
```

2. **Add new entries:**
- Format: `XXX. [Paper Title]`
- Sequential numbering from last entry

### Step 5: Update `clean_titles_for_search.txt`

**Location:** `metadata_22_09_2025/clean_titles_for_search.txt`

1. **Clean new titles:**
- Remove special characters (colons, hyphens)
- Normalize spaces
- Format: `XXX. [Cleaned Title]`

### Step 6: Update `paper_with_links.csv`

**Location:** `metadata_22_09_2025/paper_with_links.csv`

1. **Extract ArXiv links:**
```python
# Extract links from DOCX files
def extract_arxiv_link(file_path):
    # Look for patterns: https://arxiv.org/abs/XXXX.XXXXX
    # (See detailed extraction code in previous session)
```

2. **Add CSV entries:**
```csv
Review_XXX,Title,https://arxiv.org/abs/XXXX.XXXXX
```

## 📚 Documentation Updates

### Step 7: Update Main README

**Location:** `README.md`

**Key sections to update:**
```markdown
- **Total Paper Reviews**: XXX comprehensive analyses ✅ (UPDATED)
- **XXX Individual Files**: Complete unified collection (Reviews 1-XXX)
- **Daily Reviews**: Reviews 209-XXX in chronological order (May 2024 - [Current Month] 2025)
- **Professional Naming**: `Review_001.docx` through `Review_XXX.docx`
- **Daily Reviews**: XXX DOCX files (May 2024 - [Current Month] 2025)
- **Organization**: Sequential Review_001 to Review_XXX naming
```

### Step 8: Update Collection README

**Location:** `mike-paper-reviews-500/readme.md`

**Key sections to update:**
```markdown
**Total Reviews**: XXX individual DOCX files (Review_001 to Review_XXX)
**Coverage Period**: From early reviews to [Current Date]
**Last Updated**: [Current Date]

### `all-reviews/` - Unified Review Collection (XXX files)
#### **Reviews 208-XXX**: Daily Reviews (XXX files)
- **Date Range**: May 30, 2024 to [Current Date]

## 📊 Statistics
- **Total Individual Files**: XXX reviews
- **Daily Reviews**: XXX files (Reviews 208-XXX)
- **Date Coverage**: ~XX months of daily reviews (May 2024 - [Current Month] 2025)
```

## 🔧 Automation Scripts

### Title Extraction Script
```python
#!/usr/bin/env python3
"""
Extract titles from new review DOCX files
Usage: python extract_new_titles.py START_REVIEW END_REVIEW
"""

import docx
import sys
import re

def extract_title_from_review(file_path):
    try:
        doc = docx.Document(file_path)
        # Implementation details from previous session
        pass
    except Exception as e:
        return f"Error: {e}"

if __name__ == "__main__":
    start_review = int(sys.argv[1])
    end_review = int(sys.argv[2])
    
    for i in range(start_review, end_review + 1):
        file_path = f"split-reviews-docx/Review_{i:03d}.docx"
        title = extract_title_from_review(file_path)
        print(f"{i}. {title}")
```

### Link Extraction Script
```python
#!/usr/bin/env python3
"""
Extract ArXiv links from new review DOCX files
Usage: python extract_new_links.py START_REVIEW END_REVIEW
"""

import docx
import re
import sys

def extract_arxiv_link(file_path):
    # Implementation from previous session
    pass

# Similar structure to title extraction
```

## ✅ Verification Checklist

### File Consistency Check
- [ ] All metadata files have same total count
- [ ] Sequential numbering with no gaps
- [ ] All new reviews have corresponding entries
- [ ] ArXiv links are working and properly formatted
- [ ] README files reflect updated counts and dates

### Quality Assurance
```bash
# Verify file counts match
wc -l metadata_22_09_2025/*.txt metadata_22_09_2025/*.csv

# Check for sequential numbering
tail -10 metadata_22_09_2025/all_paper_titles.txt

# Verify no duplicate entries
sort metadata_22_09_2025/all_paper_titles.txt | uniq -d
```

## 🚀 Git Operations

### Commit and Push Changes
```bash
# Stage all changes
git add .

# Commit with descriptive message
git commit -m "Update metadata and documentation for Reviews XXX-YYY

- Add X new paper reviews (XXX-YYY) to all metadata files
- Update all_paper_titles.txt: OLD → NEW total reviews
- Update clean_titles_for_search.txt: Add cleaned titles
- Update paper_with_links.csv: Add ArXiv links
- Update reviews_from_208_titles.txt: Add entries XXX-YYY
- Update README files: Reflect NEW total reviews, [Month] 2025 coverage

New papers added:
- Review XXX: [Title]
- Review YYY: [Title]
[... list all new papers ...]"

# Push to remote
git push origin main
```

## 📊 Example Update Session

### Recent Update (October 8, 2025)
**Reviews Added:** 515-520 (6 new reviews)
**Previous Count:** 514 → **New Count:** 520

**Files Updated:**
1. `all_paper_titles.txt`: Added entries 515-520, updated header
2. `clean_titles_for_search.txt`: Added cleaned titles 515-520
3. `paper_with_links.csv`: Added CSV rows with ArXiv links
4. `reviews_from_208_titles.txt`: Added entries 307-312
5. `README.md`: Updated all counts from 514 to 520
6. `mike-paper-reviews-500/readme.md`: Updated collection stats

**Time Required:** ~30 minutes for 6 reviews
**Success Rate:** 100% (all titles and links extracted successfully)

## 🔄 Monthly Update Workflow

1. **Pull latest changes** from repository
2. **Identify new reviews** (count files in split-reviews-docx/)
3. **Extract titles and links** using Python scripts
4. **Update all metadata files** following this guide
5. **Update documentation** (README files)
6. **Verify consistency** using checklist
7. **Commit and push** changes
8. **Update this guide** if process changes

## 📝 Notes and Tips

### Common Issues
- **Hebrew vs English titles:** Always extract English titles for metadata
- **Missing ArXiv links:** Some papers may use different link formats
- **Duplicate handling:** Check for existing entries before adding
- **Date formatting:** Use consistent date format (Month DD, YYYY)

### Best Practices
- **Backup before changes:** Create branch or backup before major updates
- **Test extraction scripts:** Verify on small sample before batch processing
- **Double-check counts:** Ensure all files have consistent totals
- **Descriptive commits:** Use detailed commit messages for tracking

---

**Last Updated:** October 8, 2025  
**Next Scheduled Update:** November 2025  
**Maintainer:** AI Assistant + Mike  
**Repository:** https://github.com/merlihson/scientific-resources
