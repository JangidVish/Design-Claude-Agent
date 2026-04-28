---
name: start-design
description: Initialize a new client design project. Parses the content sheet, builds tasks.md, collects social/website links, and auto-generates design_guidelines.md. Run this ONCE when a new client project folder is created.
invocation: user
---

# /start-design — Project Initialization

You are starting a new client design project. Follow these steps **in order**, one at a time.

---

## STEP 0 — Check if already initialized

Before anything else:
- Check if `tasks.md` exists in the current directory
- Check if `design_guidelines.md` exists in the current directory

**If BOTH exist:**
> Say: "This project is already initialized! ✅
> - `tasks.md` has your post list
> - `design_guidelines.md` has the brand guidelines
>
> Use `/generate` to create a prompt for a specific post, or `/review-design` to apply client feedback."

Then STOP. Do not continue.

**If either is missing**, continue to Step 1.

---

## STEP 1 — Get the content sheet

Ask the designer:

> "Let's get started! 🚀
>
> Please share the client content sheet. You can give me:
> - A **local file path** (e.g. `C:\Projects\ClientName\content.xlsx` or `~/projects/client/sheet.xlsx`)
> - A **Google Sheets URL** (make sure it's set to 'Anyone with the link can view')
>
> Which do you have?"

Wait for their response.

### If local Excel/CSV file path:
- Use the Read tool to read the file
- Parse all rows and columns
- Auto-detect column names — look for these key columns (case-insensitive, partial match ok):
  - `type` → post type (Post / Carousel / Reel)
  - `topic` or `idea` → the main topic
  - `caption` → post caption text
  - `visual` or `description` → visual description (most important for prompt)
  - `cta` → call to action
  - `date` → scheduled date
  - `pillar` → content pillar
  - `hashtag` → hashtags
  - `suggestion` → extra notes
- Any additional columns → include them as extra metadata
- Skip rows where Type AND Visual Description are both empty (likely empty rows)

### If Google Sheets URL:
- Convert the URL to CSV export format:
  - Take the sheet ID from the URL (between `/d/` and `/edit` or `/view`)
  - Build this URL: `https://docs.google.com/spreadsheets/d/[SHEET_ID]/export?format=csv`
- Use WebFetch to retrieve the CSV content
- Parse exactly the same way as local file above

### Parsing errors:
- If file can't be read → ask them to check the path or sharing settings and try again
- If columns don't match expected names → show them the columns you found and ask them to confirm which is which

---

## STEP 2 — Write tasks.md

Once parsed, create `tasks.md` in the current directory using this exact format:

```
# Client Task List
*Parsed from: [filename or URL]*
*Total posts: [N]*

---

## Post 1 — [Type]
- **Date:** [value or "Not specified"]
- **Pillar:** [value or "Not specified"]
- **Topic/Idea:** [value]
- **Caption:** [value]
- **Visual Description:** [value]
- **Hashtags:** [value or "Not specified"]
- **CTA:** [value or "Not specified"]
- **Suggestions:** [value or "None"]
- **Status:** ⬜ Pending

---

## Post 2 — [Type]
[repeat for each row]
```

After writing, confirm:
> "✅ I've created `tasks.md` with **[N] posts** from the sheet.
>
> Here's a quick summary:
> [list each post as: Post 1 — Carousel: "Topic name"]"

---

## STEP 3 — Collect brand resource links

Ask:

> "Now let's build the brand guidelines. 🎨
>
> Please share the client's links — as many as you have:
> - 🌐 Website URL
> - 📸 Instagram profile URL
> - 👍 Facebook page URL
> - Any other social media or branding resources
>
> Just paste them all, one per line."

Wait for their response.

---

## STEP 4 — Scrape and analyze each link

For each link provided, use WebFetch to visit it and extract:

**From the Website:**
- Brand name and tagline
- Color palette (look for hex codes in CSS, buttons, headers, logo)
- Typography style (serif/sans-serif, modern/classic)
- Overall visual design tone (minimalist, bold, playful, corporate, etc.)
- Any recurring visual elements (patterns, icons, shapes)
- Industry/niche of the business

**From Instagram:**
- Handle name
- Bio text
- Post style observations (product shots, lifestyle, graphics, illustrations, etc.)
- Color themes you see in their grid
- Tone of captions (casual, professional, witty, inspirational, etc.)
- Content pillars (what topics they post about)

**From Facebook:**
- Handle/page name
- About section
- Post style and frequency observations
- Any brand voice notes

**From any other links:**
- Extract whatever brand-relevant information is available

If a link fails to load → note it as "Could not access — [URL]" and move on.

---

## STEP 5 — Generate design_guidelines.md

Using everything scraped, write `design_guidelines.md` in the current directory:

```markdown
# Brand Guidelines — [Brand Name]
*Generated: [today's date]*
*Sources: [list all links provided]*

---

## Brand Identity
- **Brand Name:** [extracted]
- **Industry/Niche:** [extracted]
- **Brand Voice & Tone:** [e.g. "Friendly and professional, uses emojis occasionally"]
- **Target Audience:** [inferred from content/industry]
- **Tagline:** [if found]

---

## Visual Identity
- **Primary Colors:** [e.g. "#1A1A2E (deep navy), #E94560 (accent red)"]
- **Secondary Colors:** [e.g. "#F5F5F5 (off-white), #0F3460 (dark blue)"]
- **Typography Style:** [e.g. "Clean sans-serif, modern and minimal"]
- **Logo Style:** [e.g. "Text-based wordmark, minimal icon"]
- **Overall Aesthetic:** [e.g. "Dark, modern, premium feel with bold accent colors"]

---

## Social Media Style
- **Instagram:** [URL]
  - Post style: [observations]
  - Feed aesthetic: [observations]
  - Caption tone: [observations]
- **Facebook:** [URL]
  - Post style: [observations]
- **Content Pillars:** [list recurring themes]

---

## Website Observations
- **URL:** [url]
- **Design Style:** [observations]
- **Key Brand Elements:** [what stands out]

---

## Design Preferences (for DALL-E prompts)
### Always Include:
- [e.g. "Dark background with navy/deep blue tones"]
- [e.g. "Clean, uncluttered composition"]
- [e.g. "Modern, professional feel"]

### Avoid:
- [e.g. "Bright neon colors"]
- [e.g. "Cluttered or busy layouts"]
- [e.g. "Comic or cartoonish styles"]

### Prompt Style Keywords:
[A ready-to-use string of style descriptors for DALL-E, e.g.:
"dark background, navy blue and red accent palette, modern minimalist design, clean typography, professional aesthetic, high contrast, premium brand feel, studio lighting"]

---

## Revision History
- [Today's date]: Initial guidelines created from [N] sources
```

---

## STEP 6 — Confirm completion

Say:

> "🎉 Project initialized successfully!
>
> Here's what was created:
> - 📋 `tasks.md` — [N] posts ready for production
> - 🎨 `design_guidelines.md` — Brand guidelines built from [N] sources
>
> **Next steps:**
> Type `/generate` whenever you're ready to create a DALL-E prompt for any post.
> Type `/review-design` after client feedback to update the brand guidelines.
>
> Which post would you like to start with?"

If they answer with a post number right away, go ahead and run the `/generate` flow for that post.
