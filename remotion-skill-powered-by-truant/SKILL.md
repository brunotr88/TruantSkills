---
name: remotion-best-practices
description: Best practices for Remotion - Video creation in React
metadata:
  tags: remotion, video, react, animation, composition
---

## When to use

Use this skills whenever you are dealing with Remotion code to obtain the domain-specific knowledge.

## Instagram Reels Safe Zones (MANDATORY for 9:16)

On Instagram Reels (1080x1920), the UI overlays username, caption, like/share buttons over the video. **All critical content (text, logos, CTAs) MUST stay within the safe zone** or it will be covered/clipped.

### Margin requirements (from each edge)

| Edge | Minimum margin | Recommended margin | Reason |
|---|---|---|---|
| **Top** | 108px | 150-220px | Status bar, camera notch, story indicators |
| **Bottom** | 320px | 350-450px | Caption, username, like/comment/share buttons |
| **Left** | 35px | 45-60px | Screen crop on various devices |
| **Right** | 35px | 60-120px | Engagement button cluster (like, comment, share, audio) |

### Central safe zone

The safe area for critical content is approximately **1010x1440px**, centered in the 1080x1920 frame:

```
┌──────────────────────────────┐ 0px
│        TOP DANGER ZONE       │
│     (status bar, notch)      │
├──────────────────────────────┤ ~200px
│  ┌──────────────────────┐    │
│  │                      │    │
│  │    SAFE ZONE         │    │ ← Right: engagement
│  │    ~1010 x 1440      │    │   buttons cluster
│  │                      │    │
│  │  Place all critical  │    │
│  │  text, logos, CTAs   │    │
│  │  HERE                │    │
│  │                      │    │
│  └──────────────────────┘    │
├──────────────────────────────┤ ~1560px
│      BOTTOM DANGER ZONE      │
│  (caption, username, CTA UI) │
└──────────────────────────────┘ 1920px
```

### Implementation in Remotion

For reel components, use these constants:

```tsx
const SAFE = {
  top: 200,
  bottom: 400,
  left: 50,
  right: 100,
} as const;

// Safe content wrapper
<div style={{
  position: "absolute",
  top: SAFE.top,
  bottom: SAFE.bottom,
  left: SAFE.left,
  right: SAFE.right,
  display: "flex",
  flexDirection: "column",
  justifyContent: "center",
  alignItems: "center",
}}>
  {/* Critical content here */}
</div>
```

### What CAN go outside safe zones
- Background images (full bleed is fine)
- Decorative gradients and overlays
- Ambient particles/effects
- Non-critical visual elements

### What MUST stay inside safe zones
- All readable text (titles, subtitles, descriptions)
- Logos and branding
- CTA buttons and links
- Prices and product names
- Stats and data

### Feed/Profile preview (4:5 crop)
Instagram also shows reels in feed at 4:5 (1080x1350). The visible area is centered vertically: top ~285px and bottom ~285px are cropped. Keep the most impactful visual in the center 1080x1350 area for thumbnail/feed visibility.

## Social Media Font Size Guidelines

Text on Remotion canvases must be sized for mobile phone viewing. A 1080px canvas is displayed on ~375-430px phone screens (2.5-3x reduction). **Minimum readable size on canvas: 24px.**

### Posts (1080x810 - 4:3)

| Element | Minimum fontSize | Recommended |
|---|---|---|
| Main headline | 56px | 64-80px |
| Collection/category name | 36px | 42-56px |
| Subtitle / description | 28px | 32-38px |
| Body text | 24px | 28-32px |
| Labels / badges | 20px | 22-26px |
| Button text | 20px | 22-26px |
| URL / footer | 22px | 24-28px |
| Big numbers (hero) | 80px+ | 96-200px |

### Reels (1080x1920 - 9:16)

Reference: on a 1080x1920 vertical canvas, body/subtitle text = **36-48px** (equivalent to 40-60px on horizontal 1920x1080). Titles/hooks = at least **50% larger** than body → **60-72px**.

| Element | Minimum fontSize | Recommended |
|---|---|---|
| Title / hook principale | 60px | 64-72px |
| Collection/category name | 48px | 50-60px |
| Subtitle / description | 36px | 40-48px |
| Body text / caption | 36px | 38-44px |
| Labels / badges | 28px | 30-36px |
| Button text | 28px | 30-36px |
| URL / footer | 28px | 30-36px |
| Big numbers (countdown) | 120px+ | keep as-is |

### Scaling rule of thumb
When converting from "desktop thinking" to social media:
- Sizes 8-12px → multiply by ~2.2x (target 18-26px)
- Sizes 13-18px → multiply by ~2x (target 26-36px)
- Sizes 20-30px → multiply by ~1.5x (target 32-48px)
- Sizes 32-44px → multiply by ~1.4x (target 46-64px)
- Sizes 48px+ → keep or increase slightly

### Badge/button padding
Scale padding proportionally with font size (~1.5x). A button with `fontSize: 22` needs at least `padding: "14px 32px"`.

### Logo sizes
- Post: minimum width 180px, recommended 220-280px
- Reel: minimum width 160px, recommended 200-320px

## Italian Text Verification (MANDATORY)

**ALWAYS run a mental spell-check on ALL Italian text before finalizing.** This is a blocking requirement.

### Accented vowels - NEVER omit these

| Wrong | Correct | Meaning |
|---|---|---|
| piu | più | more |
| PIU | PIÙ | MORE |
| e (verb) | è | is |
| E (verb) | È | IS |
| perche | perché | why/because |
| qualita | qualità | quality |
| cioe | cioè | that is |
| sara | sarà | will be |
| verra | verrà | will come |
| gia | già | already |
| cosi | così | so/like this |
| pero | però | but/however |
| meta | metà | half |
| lunedi | lunedì | Monday |
| martedi | martedì | Tuesday |
| mercoledi | mercoledì | Wednesday |
| giovedi | giovedì | Thursday |
| venerdi | venerdì | Friday |
| citta | città | city |
| universita | università | university |

### Apostrophes - NEVER omit these

| Wrong | Correct | Context |
|---|---|---|
| lazienda | l'azienda | the company |
| unamica | un'amica | a (female) friend |
| ce | c'è | there is |
| dove | dov'è | where is |
| cose | cos'è | what is |
| daltra parte | d'altra parte | on the other hand |
| leccellenza | l'eccellenza | the excellence |
| nellindustria | nell'industria | in the industry |

### Uppercase accents
Italian uppercase text MUST keep accents: `QUALITÀ`, `PIÙ`, `PERCHÉ`, `È`, `CITTÀ`.
Do NOT use apostrophe as substitute (E' instead of È is WRONG in professional text).

### Verification checklist
Before committing any Italian text in Remotion:
1. Search all `.tsx` files for common unaccented words: `piu`, `qualita`, `perche`, `cioe`, `gia`, `cosi`, `pero`
2. Search for missing apostrophes in articles: `l[aeiou]` without apostrophe
3. Verify uppercase accented characters render correctly (test with `npx remotion still`)
4. Use UTF-8 encoding (default in modern editors)

## Captions

When dealing with captions or subtitles, load the [./rules/subtitles.md](./rules/subtitles.md) file for more information.

## Using FFmpeg

For some video operations, such as trimming videos or detecting silence, FFmpeg should be used. Load the [./rules/ffmpeg.md](./rules/ffmpeg.md) file for more information.

## Audio visualization

When needing to visualize audio (spectrum bars, waveforms, bass-reactive effects), load the [./rules/audio-visualization.md](./rules/audio-visualization.md) file for more information.

## Sound effects

When needing to use sound effects, load the [./rules/sfx.md](./rules/sfx.md) file for more information.

## How to use

Read individual rule files for detailed explanations and code examples:

- [rules/3d.md](rules/3d.md) - 3D content in Remotion using Three.js and React Three Fiber
- [rules/animations.md](rules/animations.md) - Fundamental animation skills for Remotion
- [rules/assets.md](rules/assets.md) - Importing images, videos, audio, and fonts into Remotion
- [rules/audio.md](rules/audio.md) - Using audio and sound in Remotion - importing, trimming, volume, speed, pitch
- [rules/audio-visualization.md](rules/audio-visualization.md) - Audio visualization patterns (spectrum bars, waveforms, bass-reactive effects)
- [rules/calculate-metadata.md](rules/calculate-metadata.md) - Dynamically set composition duration, dimensions, and props
- [rules/can-decode.md](rules/can-decode.md) - Check if a video can be decoded by the browser using Mediabunny
- [rules/charts.md](rules/charts.md) - Chart and data visualization patterns for Remotion (bar, pie, line, stock charts)
- [rules/compositions.md](rules/compositions.md) - Defining compositions, stills, folders, default props and dynamic metadata
- [rules/extract-frames.md](rules/extract-frames.md) - Extract frames from videos at specific timestamps using Mediabunny
- [rules/ffmpeg.md](rules/ffmpeg.md) - Using FFmpeg for video operations (trimming, silence detection)
- [rules/fonts.md](rules/fonts.md) - Loading Google Fonts and local fonts in Remotion
- [rules/get-audio-duration.md](rules/get-audio-duration.md) - Getting the duration of an audio file in seconds with Mediabunny
- [rules/get-video-dimensions.md](rules/get-video-dimensions.md) - Getting the width and height of a video file with Mediabunny
- [rules/get-video-duration.md](rules/get-video-duration.md) - Getting the duration of a video file in seconds with Mediabunny
- [rules/gifs.md](rules/gifs.md) - Displaying GIFs synchronized with Remotion's timeline
- [rules/images.md](rules/images.md) - Embedding images in Remotion using the Img component
- [rules/light-leaks.md](rules/light-leaks.md) - Light leak overlay effects using @remotion/light-leaks
- [rules/lottie.md](rules/lottie.md) - Embedding Lottie animations in Remotion
- [rules/measuring-dom-nodes.md](rules/measuring-dom-nodes.md) - Measuring DOM element dimensions in Remotion
- [rules/measuring-text.md](rules/measuring-text.md) - Measuring text dimensions, fitting text to containers, and checking overflow
- [rules/sequencing.md](rules/sequencing.md) - Sequencing patterns for Remotion - delay, trim, limit duration of items
- [rules/sfx.md](rules/sfx.md) - Using sound effects in Remotion
- [rules/tailwind.md](rules/tailwind.md) - Using TailwindCSS in Remotion
- [rules/text-animations.md](rules/text-animations.md) - Typography and text animation patterns for Remotion
- [rules/timing.md](rules/timing.md) - Interpolation curves in Remotion - linear, easing, spring animations
- [rules/transitions.md](rules/transitions.md) - Scene transition patterns for Remotion
- [rules/transparent-videos.md](rules/transparent-videos.md) - Rendering out a video with transparency
- [rules/trimming.md](rules/trimming.md) - Trimming patterns for Remotion - cut the beginning or end of animations
- [rules/videos.md](rules/videos.md) - Embedding videos in Remotion - trimming, volume, speed, looping, pitch
- [rules/voiceover.md](rules/voiceover.md) - Adding AI-generated voiceover to Remotion compositions using ElevenLabs TTS
- [rules/parameters.md](rules/parameters.md) - Make a video parametrizable by adding a Zod schema
- [rules/maps.md](rules/maps.md) - Add a map using Mapbox and animate it
