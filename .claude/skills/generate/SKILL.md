---
name: generate
description: Generate a DALL-E optimized image prompt for a specific post. Reads the post details from tasks.md and applies brand guidelines from design_guidelines.md. Use after /start-design has been run.
invocation: user
---

# /generate — DALL-E Prompt Generator

Generate a professional, detailed DALL-E image prompt for a specific post.

---

## STEP 0 — Verify project is initialized

Check if both files exist:
- `tasks.md`
- `design_guidelines.md`

**If either is missing:**
> "⚠️ This project hasn't been initialized yet.
> Please run `/start-design` first to set up the client project."

Then STOP.

---

## STEP 1 — Ask which post

Ask:

> "Which post would you like to generate a prompt for?
>
> Example: 'Post 3', 'Carousel 1', 'Reel 2'
> (Or just type the number)"

Wait for their response.

---

## STEP 2 — Read the post from tasks.md

Open and read `tasks.md`. Find the matching post by:
- Post number (e.g. "Post 3" → find "## Post 3")
- Or by type + number (e.g. "Carousel 1" → find first Carousel in the list)

Extract all fields for that post:
- Type, Topic/Idea, Caption, Visual Description, CTA, Suggestions, any extras

**If post number not found:**
> "I couldn't find Post [N] in tasks.md. The sheet has [total] posts (Post 1 to Post [total]).
> Which post number did you mean?"

---

## STEP 3 — Read design_guidelines.md

Open and read `design_guidelines.md`. Extract:
- Primary and secondary colors
- Overall aesthetic
- Do's and Don'ts
- The "Prompt Style Keywords" line (this is your base style string)
- Any other visual preferences

---

## STEP 4 — Build the DALL-E prompt

Construct a detailed, structured DALL-E prompt using this formula:

```
[Subject/Scene from Visual Description],
[Composition and layout notes based on post type],
[Brand color palette applied to the scene],
[Lighting and mood that matches brand aesthetic],
[Style keywords from brand guidelines],
[Technical quality descriptors]
```

### Post-type specific rules:

**For a POST (single image):**
- One strong focal point
- Clean composition, breathing room around subject
- Brand colors as background or accent
- "social media post format, square composition, 1:1 ratio"

**For a CAROUSEL:**
- Describe the visual style for slide 1 (the hook/cover slide)
- Consistent visual language across slides
- "carousel slide design, bold header area, clean content sections"
- Add: "consistent visual theme suitable for multiple slides"

**For a REEL (thumbnail/cover):**
- High energy, eye-catching
- Strong central element
- "video thumbnail style, vertical format 9:16, bold and attention-grabbing"
- Movement or dynamic feel even in static image

### Always end the prompt with:
`high quality, professional photography/digital art, 4K, sharp details, marketing material`

### Full prompt format:
```
[Complete scene description]. [Composition]. [Color palette: primary hex - secondary hex]. 
[Mood and lighting]. [Style: brand aesthetic keywords]. 
[Post type specific]. High quality, professional, 4K, sharp, suitable for social media marketing.
```

---

## STEP 5 — Present the output

Show the result in this format:

---

> ### 📸 Post [N] — [Type]: "[Topic]"
>
> **Post Details:**
> - Type: [Post/Carousel/Reel]
> - Topic: [topic]
> - Caption summary: [first 100 chars of caption...]
> - Visual Description: [from sheet]
>
> **Brand Elements Applied:**
> - Colors: [primary] + [secondary]
> - Aesthetic: [from guidelines]
> - Style: [keywords used]
>
> ---
>
> **🎯 DALL-E Prompt:**
>
> ```
> [THE FULL PROMPT HERE — ready to copy-paste]
> ```
>
> ---
>
> **💡 Tips for this prompt:**
> - [Any specific advice, e.g. "If DALL-E adds unwanted text, add 'no text, no words' to the prompt"]
> - [Any variations to try if first result isn't perfect]
>
> ---
>
> **Delivered! ✅** Update the status in `tasks.md` for Post [N] to 🔄 In Progress once you start generating.
>
> Ready for the next post? Just tell me which one!

---

## STEP 6 — Update tasks.md status

After showing the prompt, update `tasks.md`:
- Find the post entry
- Change `**Status:** ⬜ Pending` to `**Status:** 🔄 In Progress`

Save the file silently (don't make a big deal of it, just do it).
