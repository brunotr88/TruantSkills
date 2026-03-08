# Remotion Best Practices - Skill for Claude Code

A comprehensive Claude Code skill with **37 specialized rules** for [Remotion](https://remotion.dev) - the framework for creating videos programmatically in React.

## What This Skill Does

When activated, Claude Code gains deep knowledge of Remotion's APIs, patterns, and best practices, including:

- **Instagram Reels safe zones** - mandatory margins for 9:16 content so text/logos aren't covered by UI overlays
- **Social media font sizing** - minimum readable sizes for posts (1080x810) and reels (1080x1920)
- **Italian text verification** - automatic spell-check for accented vowels and apostrophes (mandatory for Italian content)
- **37 topic-specific rules** covering animations, audio, video, captions, transitions, 3D, charts, maps, and more
- **3 ready-to-use component examples** (bar chart, typewriter effect, word highlight)

## Remotion Packages Referenced

This skill covers the following Remotion ecosystem packages:

```
remotion                        # Core framework
@remotion/cli                   # CLI tools (studio, render)
@remotion/media                 # Video and Audio components
@remotion/google-fonts          # Google Fonts integration
@remotion/fonts                 # Local font loading
@remotion/transitions           # Fade, slide, wipe, flip, clock-wipe
@remotion/captions              # TikTok-style captions and subtitles
@remotion/media-utils           # Audio visualization, waveforms
@remotion/layout-utils          # Text measurement, fit text
@remotion/three                 # Three.js / React Three Fiber
@remotion/lottie                # Lottie animations
@remotion/gif                   # GIF / APNG / AVIF / WebP support
@remotion/paths                 # SVG path animation (line charts)
@remotion/light-leaks           # WebGL light leak effects
@remotion/install-whisper-cpp   # Audio transcription (Whisper)
@remotion/zod-types             # Zod parameter types (color picker)
@remotion/sfx                   # Sound effects
```

Third-party packages also covered: `mediabunny`, `mapbox-gl`, `@turf/turf`

## Installation

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and configured
- A Remotion project (or intent to create one)

### Windows + WSL Setup (if needed)

If you're on Windows with WSL (recommended for Remotion development):

1. **Install WSL** (if not already):
   ```powershell
   wsl --install
   ```

2. **Install Node.js in WSL**:
   ```bash
   curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```

3. **Install Claude Code globally**:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

### Install the Skill

1. **Clone this repository** (or download the skill folder):
   ```bash
   git clone https://github.com/brunotr88/TruantSkills.git
   ```

2. **Copy the skill to your Claude Code skills directory**:
   ```bash
   mkdir -p ~/.agents/skills
   cp -r TruantSkills/remotion-skill-powered-by-truant ~/.agents/skills/remotion-best-practices
   ```

3. **Verify installation** - the skill should appear when you run Claude Code in a Remotion project.

### Create a New Remotion Project

If you don't have a Remotion project yet:

```bash
# Using npm
npx create-video@latest my-video

# Using bun
bunx create-video@latest my-video

# Navigate and start
cd my-video
npm start  # or bun start
```

## Usage

Once installed, the skill activates automatically when Claude Code detects Remotion code. You can also invoke it directly:

### Example Prompts

```
Create a 9:16 Instagram Reel with animated text that respects safe zones

Build a bar chart animation that reveals bars with spring physics

Add TikTok-style captions to my video with word highlighting

Create a map animation showing a route from Rome to Milan using Mapbox

Add a typewriter effect with a blinking cursor and pause between sentences

Generate audio visualization bars that react to the music beat

Create a transition sequence with fade and light leak effects
```

## File Structure

```
remotion-skill-powered-by-truant/
├── README.md              # This file
├── SKILL.md               # Skill entry point (loaded by Claude Code)
└── rules/
    ├── 3d.md              # Three.js and React Three Fiber
    ├── animations.md      # Fundamental animation patterns
    ├── assets.md          # Importing images, videos, audio, fonts
    ├── audio.md           # Audio: trim, volume, speed, pitch, loop
    ├── audio-visualization.md  # Spectrum bars, waveforms, bass-reactive
    ├── calculate-metadata.md   # Dynamic duration, dimensions, props
    ├── can-decode.md      # Video decode validation (Mediabunny)
    ├── charts.md          # Bar, pie, line, stock charts
    ├── compositions.md    # Compositions, stills, folders, props
    ├── display-captions.md     # TikTok-style caption display
    ├── extract-frames.md  # Frame extraction from videos
    ├── ffmpeg.md          # FFmpeg/FFprobe operations
    ├── fonts.md           # Google Fonts and local fonts
    ├── get-audio-duration.md   # Audio duration (Mediabunny)
    ├── get-video-dimensions.md # Video dimensions (Mediabunny)
    ├── get-video-duration.md   # Video duration (Mediabunny)
    ├── gifs.md            # GIF, APNG, AVIF, WebP display
    ├── images.md          # Image embedding with <Img>
    ├── import-srt-captions.md  # SRT subtitle import
    ├── light-leaks.md     # WebGL light leak overlays
    ├── lottie.md          # Lottie animations
    ├── maps.md            # Mapbox map animations
    ├── measuring-dom-nodes.md  # DOM element measurement
    ├── measuring-text.md  # Text measurement and fitting
    ├── parameters.md      # Zod schema parameters
    ├── sequencing.md      # Sequence and Series patterns
    ├── sfx.md             # Sound effects
    ├── subtitles.md       # Caption/subtitle system overview
    ├── tailwind.md        # TailwindCSS in Remotion
    ├── text-animations.md # Typewriter, word highlight
    ├── timing.md          # Interpolation, spring, easing
    ├── transcribe-captions.md  # Whisper.cpp transcription
    ├── transitions.md     # TransitionSeries, overlays
    ├── transparent-videos.md   # ProRes/WebM transparency
    ├── trimming.md        # Trim beginning/end of animations
    ├── videos.md          # Video: trim, volume, speed, loop
    ├── voiceover.md       # ElevenLabs TTS voiceover
    └── assets/
        ├── charts-bar-chart.tsx            # Bar chart component
        ├── text-animations-typewriter.tsx   # Typewriter effect
        └── text-animations-word-highlight.tsx  # Word highlight effect
```

## License

[MIT](../LICENSE)

---

*Skill created by [Bruno Truant](https://isipc.com) - Part of the [TruantSkills](https://github.com/brunotr88/TruantSkills) collection.*
