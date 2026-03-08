---
name: remotion-pro-studio
description: >
  Intelligent assistant for creating professional social media videos with the Remotion Pro Studio
  project at /mnt/c/PROGETTI/remotion-pro-studio. Use when: creating new video templates (posts/reels),
  adding animations or effects, composing scenes, choosing themes, rendering videos, extending the
  template library, or any work involving the remotion-pro-studio codebase. Triggers on: "video per
  social", "crea un reel", "template post", "animazione remotion", "remotion-pro-studio", "video
  Instagram", "video TikTok", "crea un video", references to post/reel templates, or any Remotion
  work in the remotion-pro-studio project.
---

# Remotion Pro Studio

Professional video template library for social media. Project: `/mnt/c/PROGETTI/remotion-pro-studio`.

## Decision Engine

When the user requests a video, reason through these steps IN ORDER:

### 1. Choose Format

| Request | Format | Size |
|---------|--------|------|
| Post Instagram/Facebook standard | `FORMATS.POST_4_3` | 1080x810 |
| Post Instagram feed tall | `FORMATS.POST_4_5` | 1080x1350 |
| Post square | `FORMATS.POST_1_1` | 1080x1080 |
| Reel / Story / TikTok / Shorts | `FORMATS.REEL_9_16` | 1080x1920 |
| "non so" / generico post | `FORMATS.POST_4_5` | best engagement |
| "non so" / generico reel | `FORMATS.REEL_9_16` | only option |

### 2. Choose or Create Template

**Use existing template when possible:**

| Need | Template | Key Props |
|------|----------|-----------|
| Multi-image showcase | `PostCarousel` | slides[], ctaText |
| Quote / testimonial (post) | `PostQuote` | quote, author, authorRole |
| Product with image + price | `PostProduct` | productImage, productName, price, badge |
| Announcement / event / launch | `PostAnnouncement` | headline, subheadline, date |
| Product showcase reel | `ReelShowcase` | slides[], outroHeadline, ctaText |
| Customer review reel | `ReelTestimonial` | quote, author, rating |
| Tutorial / how-to reel | `ReelTutorial` | title, steps[] |
| Hype / countdown reel | `ReelCountdown` | countFrom, revealText |

**Create new template when:** no existing template matches, or the user wants a unique layout.
See [references/creating-templates.md](references/creating-templates.md) for the creation workflow.

### 3. Choose Theme

| Brand feel | Theme | Colors | Fonts |
|------------|-------|--------|-------|
| Neutral / professional | `default` | Purple accent, light bg | Playfair + Inter |
| Premium / high-end / gold | `luxury` | Gold/charcoal, dark bg | Playfair + Cormorant |
| Tech / corporate / clean | `modern` | Blue/white | Poppins + Inter |
| Bold / energetic / colorful | `vibrant` | Coral/teal/yellow, dark bg | Montserrat + Space Grotesk |
| Clean / B&W / understated | `minimal` | Black/white only | Inter |

**Custom theme needed when:** user provides specific brand colors/fonts. Create in `src/themes/`.

### 4. Apply Constraints

For 9:16 reels, ALWAYS:
- Wrap critical content in `<SafeZone platform="instagram_reel">`
- Use font sizes: titles 60-72px, body 36-44px
- Keep text away from top 200px and bottom 400px

For all formats:
- Min font size: 24px
- Use `translate3d()` + `willChange` for GPU perf
- Max 15-20 simultaneous springs per scene
- Italian text: always correct accents (qualita, piu, perche, E)

## Component Catalog

Quick reference for all available building blocks. For detailed API and examples, see:
- [references/animations.md](references/animations.md) - Springs, easings, entrance/exit/continuous
- [references/components.md](references/components.md) - Text, effects, UI, layout, scenes

### Animations (`src/lib/animations/`)
```
SPRING_PRESETS: hero | text | snappy | slow | cinematic | bouncy | smooth
EASING_PRESETS: softEnter | softExit | smoothContinuous | textReveal | fade | elastic | sharp | standard
Entrance: fadeIn, slideIn, scaleIn, blurIn, clipReveal
Exit: fadeOut, slideOut, scaleOut
Continuous: pulse, float, breathe, kenBurns, glowPulse
```

### Text (`src/lib/text/`)
```
SplitText     - Character stagger, 4 directions (up/down/left/right)
SplitWords    - Word stagger with optional blur + scale
Typewriter    - String slicing with blinking cursor
WordHighlight - Animated highlighter background
CountUp       - Number counter with spring
```

### Effects (`src/lib/effects/`)
```
FilmGrain     - SVG feTurbulence noise overlay
Vignette      - Radial gradient darkening
GlowText      - Pulsing text-shadow glow
GradientBg    - Animated gradient angle rotation
ParticleField - Floating particles with seeded randomness
```

### Transitions (`src/lib/transitions/`)
```
TRANSITION_PRESETS: elegantFade | slideRight | slideLeft | quickWipe
clockRevealTransition(width, height) - Clock wipe factory
FlashOverlay  - White flash between scenes
GradientWipe  - Gradient sweep wipe
```

### UI Components (`src/components/ui/`)
```
Badge         - Tag/label (filled | outlined | ghost)
Divider       - Animated growing line with glow
CallToAction  - CTA button or text with spring entrance
IconWrapper   - Animated icon container (lucide + react-icons)
EmojiAnimated - Emoji with bounce entrance
```

### Layout (`src/components/layout/`)
```
SafeZone       - Platform-aware safe area wrapper
CenterStack    - Centered flex column with gap
FullBleedImage - Full-bleed image + gradient overlay
```

### Scenes (`src/components/scenes/`)
```
IntroScene    - Logo/text entrance with glow + film grain
SlideScene    - Image with Ken Burns + text overlay
TextOnlyScene - Gradient bg + headline + divider + subtext
OutroScene    - Gradient bg + glow headline + CTA
```

## Workflow: Render a Video

```bash
# Preview in Studio
cd /mnt/c/PROGETTI/remotion-pro-studio && npm run dev

# Render still
npx remotion still <CompositionId> --props='{"theme":"luxury"}'

# Render video
npx remotion render <CompositionId> --props='{"theme":"modern","title":"Hello"}'

# Test first 30 frames
npx remotion render <CompositionId> --frames=0-30

# Type check
npx tsc --noEmit
```

Composition IDs follow the pattern: `TemplateName-format` for posts (e.g., `PostCarousel-4-5`) or just `TemplateName` for reels (e.g., `ReelShowcase`).

## Team

4 specialized agents at `~/.claude/teams/remotion-pro-studio/config.json`:
- **team-lead**: Orchestration, code review, architecture
- **animation-architect**: Springs, easings, entrance/exit, transitions
- **template-builder**: Templates, layouts, scene system
- **visual-effects**: Effects, themes, text animations, icons
