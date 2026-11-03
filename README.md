# 🎬 Video Effects for Remotion (9:16 Shorts / Reels / TikTok)

[![Remotion](https://img.shields.io/badge/Powered%20by-Remotion-blue?style=flat-square&logo=react)](https://www.remotion.dev/)
[![Format](https://img.shields.io/badge/Format-9%3A16%20(1080x1920)-purple?style=flat-square)](https://www.tiktok.com/)
[![License](https://img.shields.io/badge/License-MIT%2FApache--2.0-green?style=flat-square)](#license)

A modular library and AI Agent Skill specification for crafting high-converting, transparent motion graphics layers and short-form video effects (9:16 vertical) with **[Remotion](https://www.remotion.dev/)**. 

Designed specifically for **spa/aesthetic wellness clinics** and **software/AI tool tutorials**, these effects are built as transparent overlay layers with alpha channels (ProRes 4444 / WebM VP9) ready to drop into CapCut, Premiere Pro, or DaVinci Resolve.

---

## ✨ Key Features

- **Alpha Channel by Default**: Designed to overlay seamlessly on user maintracks without covering faces or background scenes.
- **Subject Matte Depth**: Sandwich effects behind or around the subject using video matting / rotoscoping.
- **Two Curated Niches**:
  - 🌿 **Spa & Aesthetic Wellness**: Warm luxury palettes, before-after split comparisons, particle sparkles, and soft cinematic transitions.
  - 💻 **Tool & Software Demos**: Minimal Claude-style chat UIs, interactive node-link diagrams, code/edit timelines, and drag-and-drop animations.
- **AI Agent Skill Ready**: Includes a structured [`SKILL.md`](SKILL.md) for direct consumption by AI coding assistants (Antigravity, Cursor, Claude Code, Copilot).

---

## 📐 Default Specifications

| Parameter | Default Value | Notes |
| :--- | :--- | :--- |
| **Resolution** | `1080 × 1920` (9:16 Vertical) | Standard for TikTok, IG Reels, YouTube Shorts |
| **Frame Rate** | `30 fps` | Smooth motion graphics |
| **Safe Margins** | Top: `≥250px` \| Bottom: `≥400px` | Avoids platform UI buttons and caption overlays |
| **Scene Length** | `2–4 seconds` per shot | Hook within the first `0.5s` |
| **Output Codecs** | ProRes 4444 / WebM VP9 (with Alpha) | Pre-composited MP4 only when requested |

---

## 🎨 Color Presets

- **Warm Spa**:
  - Cream: `#F5EFE6`
  - Earth Brown: `#8B6F5A`
  - Champagne Gold: `#D4B483`
- **Moss Luxe**:
  - Moss Green: `#2F4A3A` (Opacity 0.9, radius 16px)
  - Cream Text: `#F3EEE3`
  - Accent Gold: `#C9A86A` (Uppercase letter-spaced)

---

## 📚 Effect Catalog

The library includes 20+ purpose-built motion graphic components organized by category:

### A. Text & Typography
- **`hook-text`**: Semi-transparent backdrop blur banner with staggered spring text animation.
- **`falling-text`**: Playful letter-drop with physics-based bounce (placed behind matted subject).
- **`big-caption`**: High-contrast, dynamic subtitles with karaoke-style active word highlighting (72–96px).
- **`count-up`**: Smooth numeric increment counter with easing.
- **`title-card`**: Chapter milestone card with sliding badge and fade-in title.
- **`neon-text-behind`**: Electric neon sign positioned behind the subject with organic flicker and multi-layered glow.
- **`result-hook`**: Upper-third outcome showcase frame sliding behind subject, paired with front-facing headline.
- **`layered-caption`**: Text-sandwich hook (massive headline behind head, crisp subtitle in front at waist level).

### B. Before & After / Grading
- **`before-after-slide`**: Interactive vertical wipe comparing raw footage vs. graded/treated results.
- **`split-screen`**: Parallel split sliding from opposite edges with duration indicators.
- **`color-slider`**: Simulated grading slider with live CSS filter adjustments.
- **`cinematic-grade`**: Film look simulation with warm highlights, letterbox (2.35:1), and subtle grain.
- **`ken-burns`**: Subtle 1.0→1.12 scale and pan across static images.

### C. Atmosphere & Mood
- **`sparkle`**: Procedural twinkling light particles with drop-shadow glow.
- **`light-leak`**: Drifting warm radial gradients using screen blend mode.
- **`soft-transition`**: Seamless blur-to-clear transitions across cuts.

### D. Simulated App & Tool UI
- **`prompt-frame`**: Minimalist Claude-style prompt bar with typing cursor and warm orange action button.
- **`storyboard`**: 3D elliptical carousel of preview frames orbiting around the presenter.
- **`cross-icon`**: Self-drawing red strike-through indicator for "don'ts" and common mistakes.
- **`drag-drop`**: Animated cursor dragging assets into an active target drop zone.
- **`edit-timeline`**: Multi-track video/audio editing timeline with animated playhead.
- **`delete-app`**: iOS-style jiggling icon grid with removal animation.

### E. Navigation & Frameworks
- **`chapter-list`**: Side-docked agenda panel ticking off items in sync with voiceover timestamps.
- **`video-list`**: Sequential card slide-in for video recommendations or playlists.
- **`video-frame`**: Camera-down subject slide revealing a 16:9 featured media frame above.
- **`process-steps`**: Animated 1→2→3 workflow with progressive vector connection paths.
- **`link-diagram`**: Node-link architecture graph dynamically connecting agents, teams, or routine steps.

### F. Call to Action & Comparisons
- **`offer-countdown`**: Flash deal badge with decorative urgency countdown.
- **`comment-cta`**: Pulsing keyword invitation with animated directional arrows.
- **`comment-box`**: Typewriter text resolving into a native comment bubble.
- **`katana-text`**: Slicing light-blade cutting through outdated methods ("OLD WAY") to reveal modern solutions ("NEW WAY").

---

## 🛠️ Usage with Remotion

### 1. Installation

```bash
npm install remotion @remotion/cli @remotion/transitions
npm install @fontsource/be-vietnam-pro # Optional: Vietnamese typography support
```

### 2. Example: Rendering an Alpha Layer (ProRes 4444)

```bash
# Render a transparent overlay component to ProRes 4444
npx remotion render src/index.ts HookText out/hook-text.mov \
  --codec=prores \
  --prores-profile=4444 \
  --image-format=png \
  --pixel-format=yuva444p10le
```

### 3. Example: Rendering WebM with Alpha (Lightweight Alternative)

```bash
npx remotion render src/index.ts NeonTextBehind out/neon-text.webm \
  --codec=vp9
```

### 4. Single-Frame Preview Check

```bash
npx remotion still src/index.ts VideoFrame preview.png --frame=45
```

---

## 🤖 Install via skills.sh

This repository follows the open **[Agent Skills](https://skills.sh)** specification. You can install and use it directly across all supported AI coding agents (Claude Code, Cursor, Antigravity, Codex, OpenCode, and others) via the `skills` CLI.

### 1. Install into your current project

```bash
npx skills add sinhnguyen777/video-effects-viral
```
> *(The CLI will prompt you to choose the target agent environment in your project).*

Or install directly for a specific agent:

```bash
# For Claude Code
npx skills add sinhnguyen777/video-effects-viral -a claude-code

# For Cursor
npx skills add sinhnguyen777/video-effects-viral -a cursor
```

### 2. Install globally (available in all workspaces)

```bash
npx skills add sinhnguyen777/video-effects-viral -g
```

### 3. Use temporarily without installing

```bash
npx skills use sinhnguyen777/video-effects-viral --agent claude-code
```

### 4. How the Agent Uses It

Once installed, your AI agent automatically references [`SKILL.md`](SKILL.md). You can prompt naturally:

> *"Create a 20-second Reel introducing our skin peel treatment using a split-screen before-after and a warm spa theme."*

> *"Build a 60-second Claude-style tutorial video with chapter-list, link-diagram, and big-caption subtitle overlays."*

The agent will follow the layer rules, timing, typography presets, and export specifications out of the box.

---

## ⚖️ Ethics & Quality Guidelines

- **Authenticity First**: Never use beautification filters, skin-smoothing plugins, or fake results on medical/spa before-and-after footage.
- **Attribution**: Only use authentic, verified client testimonials.
- **Safe Commercial Use**: Always ensure audio tracks and icons used are cleared for commercial distribution.

---

## 👤 Author

Crafted with ❤️ by **Sinh Nguyen** ([@sinhnguyen777](https://github.com/sinhnguyen777))

---

## 📄 License

Distributed under the **MIT License** or **Apache-2.0**. Feel free to use and adapt these components in your client and commercial projects!

