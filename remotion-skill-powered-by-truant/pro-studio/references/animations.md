# Animation System Reference

## Spring Presets (`src/lib/animations/springs.ts`)

```typescript
import { SPRING_PRESETS } from "./lib/animations/springs";

// Usage with Remotion spring()
const progress = spring({ frame, fps, from: 0, to: 1, config: SPRING_PRESETS.hero });
```

| Preset | damping | stiffness | mass | Use Case |
|--------|---------|-----------|------|----------|
| `hero` | 20 | 80 | 1 | Logo reveals, hero elements, main focal points |
| `text` | 18 | 120 | 0.8 | Text animations, word staggers, subtitles |
| `snappy` | 25 | 140 | 0.6 | Quick UI elements, badges, icons, counters |
| `slow` | 30 | 60 | 1.5 | Divider lines, gradual reveals, backgrounds |
| `cinematic` | 15 | 80 | 2 | Dramatic entrances, fade transitions |
| `bouncy` | 8 | 100 | 1 | Playful elements, emojis, notifications |
| `smooth` | 200 | 100 | 1 | Critical damping, no overshoot, progress bars |

### Decision guide:
- Want overshoot? Use `bouncy` (most) > `hero` > `text` (least)
- Want smooth stop? Use `smooth` (no overshoot ever)
- Want dramatic? Use `cinematic` (slow, heavy)
- Want fast? Use `snappy` (quick, light)

## Easing Presets (`src/lib/animations/easings.ts`)

```typescript
import { EASING_PRESETS } from "./lib/animations/easings";

// Usage with Remotion interpolate()
const opacity = interpolate(frame, [0, 30], [0, 1], {
  easing: EASING_PRESETS.softEnter,
  extrapolateRight: "clamp",
});
```

| Preset | Curve | Use Case |
|--------|-------|----------|
| `softEnter` | ease-out | Elements appearing, fading in |
| `softExit` | ease-in | Elements disappearing, fading out |
| `smoothContinuous` | ease-in-out | Looping animations, ken burns, gradients |
| `textReveal` | custom bezier | Text clip reveals, mask animations |
| `fade` | symmetric ease | Cross-fades, opacity transitions |
| `elastic` | overshoot | Bouncy button presses, attention-grabbers |
| `sharp` | material sharp | Precise UI movements |
| `standard` | material standard | Default material motion |

## Entrance Functions (`src/lib/animations/entrance.ts`)

```typescript
// fadeIn(frame, startFrame, duration?) -> opacity: number
const opacity = fadeIn(frame, 10, 15);

// slideIn(frame, fps, startFrame, direction?, distance?, config?) -> { translateX, translateY, opacity }
const { translateX, translateY, opacity } = slideIn(frame, fps, 10, "up", 40, SPRING_PRESETS.text);

// scaleIn(frame, fps, startFrame, config?) -> { scale, opacity }
const { scale, opacity } = scaleIn(frame, fps, 0, SPRING_PRESETS.hero);

// blurIn(frame, startFrame, duration?) -> { blur, opacity }
const { blur, opacity } = blurIn(frame, 0, 15);

// clipReveal(frame, startFrame, duration?, direction?) -> clipPath string
const clipPath = clipReveal(frame, 10, 20, "center"); // "center" | "left" | "right"
```

## Exit Functions (`src/lib/animations/exit.ts`)

```typescript
// fadeOut(frame, startFrame, duration?) -> opacity: number
const opacity = fadeOut(frame, 75, 15);

// slideOut(frame, fps, startFrame, direction?, distance?, config?) -> { translateX, translateY, opacity }
const { translateX, translateY, opacity } = slideOut(frame, fps, 50, "up");

// scaleOut(frame, fps, startFrame, config?) -> { scale, opacity }
const { scale, opacity } = scaleOut(frame, fps, 50);
```

## Continuous Functions (`src/lib/animations/continuous.ts`)

```typescript
// pulse(frame, period?, min?, max?) -> scale: number
const scale = pulse(frame, 60, 0.95, 1.05);

// float(frame, period?, amplitude?) -> translateY: number
const y = float(frame, 90, 8);

// breathe(frame, period?, min?, max?) -> scale: number
const scale = breathe(frame, 120, 0.97, 1.03);

// kenBurns(frame, totalFrames, scaleFrom?, scaleTo?, driftX?, driftY?)
//   -> { scale, translateX, translateY }
const kb = kenBurns(frame, 60, 1, 1.05, -10, 0);

// glowPulse(frame, period?, min?, max?) -> blur radius: number
const glowBlur = glowPulse(frame, 90, 8, 20);
```

## Composition Pattern

Typical scene animation timeline:

```
Frame 0-15:   Entrance animations (fadeIn, slideIn, scaleIn, blurIn)
Frame 10-30:  Text staggers (SplitText, SplitWords start revealing)
Frame 15-∞:   Continuous effects (kenBurns, pulse, breathe on background)
Frame 30-50:  Secondary elements (subtitles, badges, dividers)
Frame 50-60:  Exit animations (fadeOut for scene transitions)
```

Key rules:
- Stagger start frames by 5-10 frames for natural feel
- Use spring for interactive/snappy, easing for smooth/predictable
- Always clamp extrapolation: `extrapolateLeft: "clamp", extrapolateRight: "clamp"`
- Never exceed 15-20 simultaneous springs in one scene
