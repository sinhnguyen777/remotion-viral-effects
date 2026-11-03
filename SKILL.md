---
name: video-effects
description: |
  Build short 9:16 motion graphics videos (Reels/TikTok) for spa businesses and tool-tutorial content using Remotion.
  Use when the user wants to: create text/caption effects, before-after comparisons, simulated UI overlays, CTAs, result hooks, or any transparent-layer overlay on a main video track.
  Do not use when: editing static images only, rendering non-9:16 video, or working outside the Remotion stack.
---

# Video Effects

Build motion graphics from user-supplied assets (photos, clips, logo, voiceover, music). Never generate synthetic footage of real people.

## Step 0 — Gather Inputs (once, concisely)

- **Goal**: introduce a service / treatment results / promotion / client testimonial / teach a tool
- **Assets**: before-after photos, footage, logo, voiceover file, background music, tool screenshots
- **Maintrack**: the primary clip (or at least 1 frame) to determine the subject's face position; a subject matte is required for effects #2, #15, #22, #28, #30, #31, #32, or #33
- **Effects**: which effects to use (by code below) — if the user does not specify, suggest 5–7 effects that fit the goal
- **Brand colors + fonts**. Two built-in presets if none provided:
  - **Warm Spa**: cream `#F5EFE6`, earth brown `#8B6F5A`, champagne gold `#D4B483`
  - **Moss Luxe**: moss-green background `#2F4A3A` (opacity 0.9, border-radius 16px), cream text `#F3EEE3`, gold label `#C9A86A` uppercase letter-spaced, active item: cream background with moss text
- **Duration**: default 15–30 seconds (tutorial videos may run 60–90 seconds)

If any asset is missing, use a clearly labelled placeholder so the user can swap it in later.

## Default Specs

> [!IMPORTANT]
> Apply to **every** effect. Do not override unless the user explicitly requests it.

- 1080×1920, 30 fps; text must stay within the safe zone (≥250 px from the top edge, ≥400 px from the bottom edge)
- Each scene: 2–4 seconds; the hook must appear within the first 0.5 seconds
- Every effect is a self-contained component accepting props (text, image, color, timing) for reusability
- Vietnamese font: install via npm (e.g. `@fontsource/be-vietnam-pro`, import `vietnamese-700.css` / `-800.css`) so diacritics render correctly

## Layer Rules (apply to ALL effects)

- Every effect is a **transparent overlay layer** placed on top of the maintrack. Never fill the entire frame with a solid background; if a background is needed for legibility, use a semi-transparent strip/block (rgba opacity 0.3–0.5 + blur) so the maintrack remains visible behind it.
- Export each layer with an alpha channel so the user can composite it onto the maintrack in CapCut/Premiere: ProRes 4444 (`--codec=prores --prores-profile=4444 --image-format=png --pixel-format=yuva444p10le`) or WebM VP9 with alpha. Only export a pre-composited MP4 when the user supplies a maintrack and explicitly requests it.
- **Never cover the subject's face.** Check (or inspect a maintrack frame for) the face position and empty areas; all cards, text, and overlays go in empty zones or below chest level.
- Effects that appear **behind the subject** (#2, #22, #28, #30, #31, #32, #33, and the rear pass of #15) require a **subject matte** (alpha-channel video created by CapCut's background-removal, Runway, etc.). Layer order: maintrack → behind effect → matted subject → front effect. Without a matte, place the effect in an empty zone — never overlap the subject.
- Speech-synced effects (#3, #20, #29) require **timestamped transcription**: generate it from the voiceover file using **@skill:remotion-captions**, or have the user supply timestamps.

---

## Effect Catalog

### A. Text & Captions

1. **hook-text**: semi-transparent dark banner (rgba ~0.3 opacity + 5 px backdrop blur) spanning the frame at the lower third, maintrack visible behind; text animates in line-by-line or word-by-word with fade + 20 px upward slide, staggered 4–6 frames, soft spring; keywords switch to the accent color.

2. **falling-text**: each character falls from above, hits the "floor" and bounces 1–2 times (low spring damping, mass 1), staggered 2 frames. **Position: upper third, left of frame**, max 2 lines. Place **behind the subject** (below the matte layer) so the subject always stands in front; without a matte, move text into empty space — never overlap the face.

3. **big-caption**: bold subtitle at 72–96 px, 2–4 words at a time, with stroke/shadow for readability on any background; the word currently being spoken scales to 1.1 and switches color. Generate from the voiceover file using **@skill:remotion-captions**.

4. **count-up**: number animates from 0 to the target value in 1 second, easing out.

5. **title-card**: chapter title card — small uppercase label ("PART 2") + large title; a colored block slides in and then the text fades up; holds for 1.5–2 seconds.

28. **neon-text-behind**: one or two emotionally charged words as a **flickering neon sign placed behind the subject**. Layer order: maintrack → semi-transparent dark overlay (rgba black ~0.75–0.8, covering the full frame) → neon text → matted subject (preserve brightness, optionally add a very subtle white edge glow) → front captions. Result: **only the subject and the neon text are bright**, everything else goes dark. Neon text: very bold, large enough to span nearly the full width (character height ~20% of frame width), positioned **above the top of the subject's head** so the head only clips the bottom of the letters while the full word remains readable; near-white letterform core, accent glow (default hot pink `#FF4D6D`), multi-layered text-shadow (white core + 3–4 progressively wider glow layers in the accent color). Flickering: buzzes on 2–3 times over ~6 frames, holds bright, randomly blinks off for 1 frame. Use for emotional/climactic moments, maximum 1–2 times per video.

30. **result-hook**: opens with **the final result** (finished product, results screen, or approved after-treatment photo) before narrating the process.
   - Result frame (video/screenshot, large border-radius ~3%, drop shadow) placed in the **upper third**, width ~92%, **behind the subject**: layer order maintrack → result frame → matted subject (same as #28). The subject's head may only cover the **bottom edge** of the frame; the key content must remain visible. Shift/scale the subject layer down if needed.
   - **Title line sits in front of the subject** (topmost layer), at chin-to-chest height, never covering eyes or mouth: rounded square icon box (user's icon or logo) + bold 2-line text block, light gold text on a semi-transparent accent background, dashed border.
   - Animation: result frame drops slightly + scales 0.9→1 (spring) → icon box pops and rotates slightly → text block slides in from the right, staggered ~4 frames. All within the first 0.7 seconds of the video.
   - The result must be genuine (the actual outcome the video teaches), never fabricated.

31. **layered-caption**: hook with two text layers sandwiching the subject. **Large headline** (1–2 words per line, max 2 lines, all-caps heavy white, character height ~20% of frame width, positioned ~27–50% down the frame) sits **behind the subject**; **sub-caption** smaller (~7% of frame width, pale gold `#FFF0B8`, with shadow) sits **in front of the subject** at waist-to-hip level. The headline must still be readable even when the subject covers its center: choose recognizable words, large enough that the portions visible on either side are still legible. Animation: headline scales 1.35→1 + fades; ~4 frames later the sub-caption slides up. Use for hooks only.

---

### B. Before–After & Color

6. **before-after-slide**: a vertical divider splits the frame — **left side is the original, right side is the corrected version**; the divider sweeps left and right (interpolate + clipPath), labelled "Before" left / "After" right. For **film color grading**: left stays desaturated (grayscale), right shows the graded version (boosted saturation, gentle contrast). For treatment before-after photos: use both real photos as-is — no beauty filters.

7. **split-screen**: two images slide in from opposite sides simultaneously, with treatment timeline labels.

8. **color-slider**: animated slider (temperature, brightness, saturation…) with a moving handle; the preview frame updates with a matching CSS filter in real time.

9. **cinematic-grade**: film grade — increased contrast, slight saturation pull, warm highlights; add black bars on two sides (letterbox 2.35:1), subtle film grain, and vignette.

10. **ken-burns**: scale 1→1.12 with a gentle pan throughout the scene.

---

### C. Spa Atmosphere

11. **sparkle**: 20–40 light particles at fixed-seed random positions, opacity twinkling; glow via drop-shadow.

12. **light-leak**: warm radial gradient, opacity 0.2–0.4, `mixBlendMode: screen`, drifting slowly.

13. **soft-transition**: `@remotion/transitions` (fade, slide), blur sweeps 8 px→0 across the cut.

---

### D. Simulated UI (for tool-tutorial videos)

Draw minimal custom UI — never include any app's real logo or wordmark.

14. **prompt-frame**: **Claude-style chat interface**: ivory background `#FAF9F5`, border `#E5E1D6`, large border-radius, italic serif placeholder text ("How can I help you today?"), "+" and tool buttons at the bottom-left, **square rounded send button in Claude orange `#D97757`** at the bottom-right (dimmed when empty, bright when text is present). Text types character by character with a cursor; the send button presses down; then orange typing dots appear ("Thinking…"). Place in the lower half, clear of the face. Do not draw the Claude logo, star, or the word "Claude" — if an exact replica is needed, use the user's own screen recording.

15. **storyboard**: 6–8 images arranged in an **elliptical orbit around the subject**, rotating continuously (~12 seconds/revolution) so front-pass images move **left to right**. Images in the rear half of the orbit sit **behind the subject** (below the matte), smaller and dimmer; images in the front half sit in front of the subject. **The image currently at the front center: glowing border (accent glow), scales ~1.12 and rises slightly** above the rest. Scene number badge at the corner of each image.

16. **cross-icon**: an icon appears, then a red diagonal line draws itself across it (`strokeDashoffset`), and the icon fades — for "common mistake" / "don't do this" moments.

17. **drag-drop**: a mouse cursor drags a file icon along a curved path into a "drop zone" box; the box highlights with a border, then a checkmark appears.

18. **edit-timeline**: a multi-track timeline UI (video, text, music tracks); clips slide into position and a playhead sweeps across.

19. **delete-app**: a grid of app icons jiggles, an × badge appears, one icon shrinks and disappears, and the grid closes in.

---

### E. Navigation & Lists

20. **chapter-list**: a floating semi-transparent panel in the **empty space beside the subject — never covering the face** (narrow panel ~40–45% of frame width): "IN THIS VIDEO" label + "01 / N" counter, list with checkboxes. **Each item gets ticked exactly when the voiceover mentions that topic** (use timestamps from the transcript): the active item highlights with a bright background + ✓ check; past items keep their ✓ and dim.

21. **video-list**: rows of videos (thumbnail + title + duration) slide in one after another.

22. **video-frame**: use when a video/illustration frame needs to appear in a spot currently blocked by the subject. Sequence (~0.5 s, simultaneous):
   - Create a subject overlay layer **precisely aligned** with the maintrack (using the subject matte) so there is no jump-cut at the start.
   - The maintrack below **blurs out** (blur 0→12 px, slight darkening, slight scale ~1.05).
   - The matted subject layer **slides downward** (~35–45% of frame height) so the face lands around 55–75% of the frame, still sharp and speaking.
   - Simultaneously in the upper half, elements appear staggered (4–5 frames apart, slide up + fade): small lead-in line → **large title** (bright accent color) → **rounded-corner video frame** ~84% wide, 16:9–16:10 ratio, drop shadow → small transition line → **large emphasis text** (secondary accent color). Layout guide: small text ~8% from top, title ~13%, video frame ~20–48%, lower caption ~50–60%.
   - Exit: reverse (caption and frame fade, subject slides back to original position, maintrack deblurs) — or hard-cut to the next scene.
   - Without a subject matte this effect is not possible; ask the user or fall back to placing the video frame in an empty zone.
   - **Layer rule exception**: because the maintrack itself must be blurred, this segment requires the maintrack clip as input and exports a pre-composited clip for that time range (the user places it over the matching section on their timeline).

23. **process-steps**: steps 1→2→3 appear in sequence with connecting lines drawing in progressively.

29. **link-diagram**: a node-link diagram connecting multiple entities. **Use when the voiceover discusses**: relationships, org charts, logical skincare steps, interdependent factors, agent teams and workflows, or the components needed to build a video.
   - Background: semi-transparent dark overlay (~0.65 opacity) + strong blur (12–14 px) over the maintrack, subject faintly visible.
   - Small lead-in line at the top (~12% down). **Central node**: circle with accent border, icon, small label below, plus an **angled label tag** (light background, bold text) that pops out to the side. **Dashed connector lines** draw from **below the central node's label** to each **child node** (frosted-glass rounded card: icon in a white box + name); lines must not cut through any text.
   - Sequence: lead-in → central node springs in → label tag → dashes draw → child nodes spring in one by one, staggered 4–5 frames. Each child node appears **in sync with the voiceover mentioning** that entity.
   - Layout by node count: 2 child nodes — one on each side; 3–4 nodes — split into rows; sequential flow — stack vertically or zigzag with arrows; max ~6 nodes for mobile readability.
   - Draw simple custom icons. Never draw brand logos (OpenAI, Anthropic, etc.); if the user wants real logos, use logo files they supply and have rights to use.

---

### F. Call to Action

24. **offer-countdown**: a promotional card pops up alongside a decorative countdown timer.

25. **comment-cta**: a line inviting viewers to comment a keyword (e.g. "Comment SPA to get…"); the keyword is enclosed in a flashing box with a downward arrow.

26. **comment-box**: a simulated comment field where text types out character by character, then resolves into a comment bubble. The content is the phrase viewers are invited to type — not a fabricated comment attributed to a real person.

---

### G. Old → New

27. **katana-text**: the OLD phrase (small label "OLD WAY", light gray) appears for 0.5–1 s → a glowing sword slash (white bar with accent glow) cuts diagonally at ~−13° across the text in ~7 frames, 1-frame white flash → the text splits along the cut line (polygon clipPath), both halves fly apart in opposite directions with a slight rotation and fade over ~0.6 s → the NEW phrase (label "NEW WAY", accent color) slides up and holds. Background: semi-transparent dark layer + light blur, subject still visible.
   - **Use only when there is an old→new pair**: something outdated or wrong being replaced by something new. Examples: "Claude burns tokens" → "7 steps to save"; "Skin detox" → "Nourish from within". Do not use to introduce a standalone headline with nothing being replaced.
   - Maximum once per video; place at the hook or a key pivot point.
   - Both phrases are required; if the user provides only one, ask for the other.

---

Logo at start/end: use **title-card** + glow, or scale 0.8→1 for a logo reveal.

---

## Suggested Templates

- **Spa 20 s**: hook-text or result-hook (2 s) → ken-burns/clip (4 s) → process-steps (5 s) → before-after-slide (5 s) → offer-countdown or comment-cta (2 s) → logo (2 s)
- **Tool tutorial 60 s**: result-hook + chapter-list in the opening scene → each chapter opens with title-card, illustrated by Group D effects or link-diagram → big-caption throughout → comment-cta + comment-box at the end

---

## How to Build

1. Read **@skill:remotion-best-practices** (required). If no project exists yet, also read **@skill:remotion-create**.
2. Write each effect as a component; compose them with `<Sequence>` / `<Series>`.
3. Preview a few frames with `remotion still` on a real maintrack frame. Verify: text is legible on mobile, rear text/frames are not hidden by the subject, the subject's face is never covered. If Remotion cannot load its bundled Chrome, pass `--browser-executable` pointing to an installed Chrome.
4. Render with `remotion-render`: default to per-effect alpha layers (ProRes 4444 / WebM VP9); only export a pre-composited MP4 when the maintrack is provided and explicitly requested. Deliver files to the user.

## Definition of Done

- [ ] Each Remotion component compiles without errors.
- [ ] At least 1 frame previewed with `remotion still`; text/frames behind the subject are not clipped, face is not covered.
- [ ] Output format is correct: alpha layer or pre-composited MP4 per requirements.
- [ ] Files delivered to the user with placement instructions for CapCut / Premiere.

---

## Hard Rules

- Do not smooth skin, alter body shape, change skin tone, or swap faces on result photos or clips. Before-after images are used as-is; only crop and apply equal brightness adjustment to both sides. Color effects (#8, #9, the color pass in #6) apply to atmospheric footage only — never to treatment result images.
- Client testimonials must use the client's exact words; do not write copy and attribute it to a real person.
- Do not use copyrighted music; use music the user supplies or leave the audio track empty with a note.
- Avoid absolute-outcome language ("100% gone", "permanent results").
- **katana-text** slashes a method or belief — never a competitor's brand name, product, or specific person.
