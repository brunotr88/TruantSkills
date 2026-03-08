# Component Reference

## Text Components (`src/lib/text/`)

### SplitText
Character-by-character stagger animation.

```tsx
<SplitText
  text="HELLO WORLD"         // Text to animate
  frame={frame}              // Current frame (useCurrentFrame)
  startFrame={10}            // When to start (default: 0)
  staggerDelay={2}           // Frames between each char (default: 2)
  springConfig={SPRING_PRESETS.text}  // Spring config (default: text)
  direction="up"             // "up" | "down" | "left" | "right" (default: "up")
  distance={20}              // Pixels to travel (default: 20)
  style={{                   // CSS for the wrapper
    fontFamily: resolveFont(theme.fonts.display),
    fontSize: 64,
    color: theme.colors.text,
  }}
/>
```

Best for: Short text (< 15 chars), dates, labels, brand names.

### SplitWords
Word-by-word stagger with optional blur and scale.

```tsx
<SplitWords
  text="Multiple Words Here"
  frame={frame}
  startFrame={10}
  wordStaggerDelay={4}       // Frames between words (default: 4)
  springConfig={SPRING_PRESETS.text}
  withBlur                   // Add blur-in per word (default: false)
  withScale                  // Add scale-in per word (default: false)
  style={{
    fontFamily: resolveFont(theme.fonts.display),
    fontSize: 52,
    color: theme.colors.white,
  }}
/>
```

Best for: Headlines, titles, longer text. Use `withBlur + withScale` for cinematic feel.

### Typewriter
Progressive text reveal with blinking cursor.

```tsx
<Typewriter
  text="Typing this out..."
  frame={frame}
  startFrame={0}
  framesPerChar={2}          // Speed (default: 2)
  cursorChar="|"             // Cursor character (default: "|")
  showCursor={true}          // Show cursor (default: true)
  cursorBlinkRate={15}       // Blink speed in frames (default: 15)
  style={{ fontSize: 36, color: theme.colors.text }}
/>
```

Best for: Revealing messages, tech/hacker aesthetic, captions.

### WordHighlight
Animated highlighter background effect.

```tsx
<WordHighlight
  text="Highlighted"
  frame={frame}
  startFrame={20}
  duration={20}              // Animation duration (default: 20)
  highlightColor="rgba(108, 92, 231, 0.3)"
  highlightHeight="40%"      // Height of highlight stripe
  style={{ fontSize: 48 }}
/>
```

Best for: Emphasizing key words within sentences.

### CountUp
Animated number counter.

```tsx
<CountUp
  from={0}                   // Start value (default: 0)
  to={1500}                  // End value
  frame={frame}
  startFrame={10}
  springConfig={SPRING_PRESETS.snappy}
  decimals={0}               // Decimal places (default: 0)
  prefix="$"                 // Before number (default: "")
  suffix="+"                 // After number (default: "")
  style={{ fontSize: 96, fontWeight: 800 }}
/>
```

Best for: Stats, prices, metrics, countdown numbers.

## Effect Components (`src/lib/effects/`)

### FilmGrain
```tsx
<FilmGrain opacity={0.4} baseFrequency={0.8} />
```
Place LAST in the component tree (on top of everything). Adds cinematic grain.

### Vignette
```tsx
<Vignette intensity={0.3} innerRadius={30} outerRadius={70} />
```
Darkens edges. Use intensity 0.2-0.4. Place before FilmGrain.

### GlowText
```tsx
<GlowText frame={frame} color="rgba(184,149,107,0.6)" period={90} minBlur={8} maxBlur={20}>
  <span>Glowing headline</span>
</GlowText>
```
Wraps children with pulsing text-shadow. Best on dark backgrounds.

### GradientBg
```tsx
<GradientBg
  frame={frame}
  colors={[theme.colors.primary, theme.colors.primaryDark]}  // 2 or 3 colors
  angleFrom={135}            // Start angle (default: 135)
  angleTo={180}              // End angle (default: 180)
  duration={60}              // Rotation duration (default: 60)
/>
```
Fills AbsoluteFill with animated gradient. Use as first layer in scenes.

### ParticleField
```tsx
<ParticleField
  frame={frame}
  count={30}                 // Number of particles (default: 30)
  color="rgba(255,255,255,0.3)"
  maxSize={4}                // Max particle size (default: 4)
  seed={42}                  // Random seed for determinism (default: 42)
  width={1080}               // Canvas width
  height={1920}              // Canvas height
/>
```
Floating particles. Deterministic via seed. Use 20-40 particles, keep subtle.

## UI Components (`src/components/ui/`)

### Badge
```tsx
<Badge text="NEW" theme={theme} variant="filled" />  // "filled" | "outlined" | "ghost"
```

### Divider
```tsx
<Divider
  frame={frame}
  startFrame={30}
  maxWidth={200}
  color={theme.colors.accent}
  height={1}
  glowColor={`${theme.colors.accent}CC`}  // Optional glow
/>
```

### CallToAction
```tsx
<CallToAction
  text="Shop Now"
  theme={theme}
  frame={frame}
  startFrame={70}
  variant="button"           // "button" | "text"
/>
```

### IconWrapper
```tsx
import { Heart } from "lucide-react";

<IconWrapper size={48} color={theme.colors.accent} frame={frame} startFrame={10} animated>
  <Heart size={48} />
</IconWrapper>
```

### EmojiAnimated
```tsx
<EmojiAnimated emoji="⭐" size={48} frame={frame} startFrame={10} />
```

## Layout Components (`src/components/layout/`)

### SafeZone
```tsx
<SafeZone platform="instagram_reel">  {/* "instagram_reel" | "instagram_post" | "tiktok" | "generic" */}
  {/* Critical content here - text, logos, CTAs */}
</SafeZone>
```

Margins applied:
- instagram_reel: top=200, bottom=400, left=50, right=100
- instagram_post: top=30, bottom=30, left=30, right=30
- tiktok: top=150, bottom=350, left=50, right=50
- generic: top=40, bottom=40, left=40, right=40

### CenterStack
```tsx
<CenterStack gap={20} style={{ position: "absolute", inset: 60 }}>
  <SplitWords ... />
  <Divider ... />
  <CallToAction ... />
</CenterStack>
```

### FullBleedImage
```tsx
<FullBleedImage
  src={staticFile("images/photo.jpg")}
  gradientOverlay="linear-gradient(to top, rgba(0,0,0,0.9) 0%, transparent 70%)"
/>
```

## Scene Components (`src/components/scenes/`)

### IntroScene
```tsx
<IntroScene
  theme={theme}
  logoSrc="logo.png"         // Optional - shows text title if omitted
  tagline="Since 1980"       // Optional tagline below logo
  fadeOutStart={75}
  fadeOutDuration={15}
/>
```

### SlideScene
```tsx
<SlideScene
  theme={theme}
  imageSrc="images/photo.jpg"
  title="Product Name"
  subtitle="Optional subtitle"
  totalFrames={60}
/>
```

### TextOnlyScene
```tsx
<TextOnlyScene
  theme={theme}
  headline="Big Statement"
  subtext="Supporting details"
  showDivider={true}
/>
```

### OutroScene
```tsx
<OutroScene
  theme={theme}
  headline="Our Collection"
  subtitle="Premium Quality"
  ctaText="Shop Now"
/>
```

## Layer Order Convention

Always layer components in this order (bottom to top):

1. `GradientBg` or background color
2. `FullBleedImage` (if using image background)
3. `ParticleField` (ambient particles)
4. Content (SafeZone > CenterStack > text/UI components)
5. `Vignette`
6. `FilmGrain` (always last)
