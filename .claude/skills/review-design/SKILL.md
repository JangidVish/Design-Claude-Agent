---
name: review-design
description: Apply client feedback to update design_guidelines.md. Run this when a client reviews a post and requests changes to colors, style, tone, or any visual preferences. Updates the brand memory so all future prompts reflect the new direction.
invocation: user
---

# /review-design — Apply Client Feedback

Update the brand guidelines based on client feedback so all future prompts are aligned.

---

## STEP 0 — Verify design_guidelines.md exists

**If missing:**
> "⚠️ No `design_guidelines.md` found. Please run `/start-design` first."

Then STOP.

---

## STEP 1 — Ask for the feedback

Ask:

> "Please paste the client's feedback below. 📝
>
> This can be:
> - Direct client message/WhatsApp/email text
> - Your own notes from a call
> - Specific design change requests
>
> Just paste it as-is — I'll extract what needs to change."

Wait for their input.

---

## STEP 2 — Analyze the feedback

Read the feedback carefully and identify:

**Color changes:**
- Did they mention specific colors? (e.g. "make it more blue", "avoid yellow", "use our brand color #FF5733")
- Did they reject the current palette?

**Style changes:**
- Did they say the design looks too dark/light, too formal/casual, too busy/minimal?
- Did they reference a style they liked? (e.g. "like Apple's website", "more playful like Canva")

**Content/composition changes:**
- Did they want more/less text in images?
- Different layout or composition?

**Tone changes:**
- Did they say it feels off-brand? Too corporate? Too casual?

**Specific elements:**
- Did they mention icons, patterns, gradients, overlays, fonts?
- Any recurring complaints?

**What they liked:**
- Did they mention anything they want to keep?

---

## STEP 3 — Show a summary before applying

Before making any changes, show:

> "Here's what I'm understanding from the feedback:
>
> **Changes to apply:**
> - 🎨 Colors: [what changes]
> - ✏️ Style: [what changes]
> - 📐 Composition: [what changes]
> - 🚫 New Don'ts: [what to avoid going forward]
> - ✅ Keep: [what they liked / keep unchanged]
>
> **Sections in design_guidelines.md I'll update:**
> - [list which sections will be modified]
>
> Should I apply these changes? (Yes / No / Let me adjust)"

Wait for confirmation.

---

## STEP 4 — Apply changes to design_guidelines.md

Once confirmed:

1. Read the current `design_guidelines.md`
2. Make targeted edits to the relevant sections — **do not rewrite the whole file**
3. Specifically:
   - Update color values if colors changed
   - Update "Always Include" / "Avoid" lists in Design Preferences
   - Update Prompt Style Keywords line with new/revised descriptors
   - Update Brand Voice if tone feedback was given
   - Add any new observations under Social Media Style if relevant
4. Add a revision entry at the bottom:

```markdown
- [Today's date]: Updated based on client feedback — [1-line summary of main change]
```

---

## STEP 5 — Confirm and show the diff

After saving, show:

> "✅ `design_guidelines.md` has been updated!
>
> **What changed:**
> - [Bullet list of specific changes made]
>
> **New Prompt Style Keywords:**
> `[Updated keyword string]`
>
> All future prompts from `/generate` will now reflect these changes.
>
> Want to regenerate the prompt for the post the client reviewed?
> Just run `/generate` and tell me the post number."
