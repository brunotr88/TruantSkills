# Creating New Templates

## Step-by-Step Workflow

### 1. Define the Zod Schema

Every template starts with a Zod schema. Include sensible defaults for every field so the composition renders without props.

```tsx
import { z } from "zod";

export const myTemplateSchema = z.object({
  theme: z.enum(["default", "luxury", "modern", "vibrant", "minimal"]).default("default"),
  title: z.string().default("Default Title"),
  subtitle: z.string().optional(),
  // ... other props with defaults
});

type MyTemplateProps = z.infer<typeof myTemplateSchema>;
```

### 2. Create the Component File

Location:
- Posts: `src/templates/posts/PostName.tsx`
- Reels: `src/templates/reels/ReelName.tsx`

Template structure:

```tsx
import React from "react";
import { AbsoluteFill, Sequence, useCurrentFrame } from "remotion";
import { z } from "zod";
// Import all 5 themes
import { defaultTheme } from "../../themes/default";
import { luxuryTheme } from "../../themes/luxury";
import { modernTheme } from "../../themes/modern";
import { vibrantTheme } from "../../themes/vibrant";
import { minimalTheme } from "../../themes/minimal";
import type { Theme } from "../../themes/types";
import { resolveFont } from "../../fonts";
// Import needed components
import "../../fonts";  // MUST import to trigger font loading

const THEMES: Record<string, Theme> = {
  default: defaultTheme, luxury: luxuryTheme, modern: modernTheme,
  vibrant: vibrantTheme, minimal: minimalTheme,
};

export const myTemplateSchema = z.object({
  theme: z.enum(["default", "luxury", "modern", "vibrant", "minimal"]).default("default"),
  title: z.string().default("Title"),
});

export const MyTemplate: React.FC<z.infer<typeof myTemplateSchema>> = ({ theme: themeKey, title }) => {
  const frame = useCurrentFrame();
  const theme = THEMES[themeKey] ?? defaultTheme;

  return (
    <AbsoluteFill style={{ backgroundColor: theme.colors.background }}>
      {/* Scenes via Sequence */}
    </AbsoluteFill>
  );
};
```

### 3. Register in Root.tsx

For posts (add to POST_TEMPLATES array):
```tsx
import { MyTemplate, myTemplateSchema } from "./templates/posts/MyTemplate";

// Add to POST_TEMPLATES:
{ id: "MyTemplate", component: MyTemplate, schema: myTemplateSchema, duration: 150 },
```
This automatically creates compositions in all 3 post formats (4:3, 4:5, 1:1).

For reels (add Composition directly):
```tsx
import { MyReel, myReelSchema } from "./templates/reels/MyReel";

// Add inside <Folder name="Templates/Reels-9-16">:
<Composition
  id="MyReel"
  component={MyReel}
  schema={myReelSchema}
  defaultProps={myReelSchema.parse({})}
  durationInFrames={450}
  fps={DEFAULTS.fps}
  width={FORMATS.REEL_9_16.width}
  height={FORMATS.REEL_9_16.height}
/>
```

### 4. Scene Composition Patterns

**Multi-scene with Sequence:**
```tsx
<AbsoluteFill>
  <Sequence durationInFrames={90}>
    <IntroScene theme={theme} tagline={title} />
  </Sequence>
  <Sequence from={90} durationInFrames={180}>
    {/* Main content */}
  </Sequence>
  <Sequence from={270} durationInFrames={120}>
    <OutroScene theme={theme} headline="Discover" ctaText="Learn More" />
  </Sequence>
</AbsoluteFill>
```

**Multi-slide with TransitionSeries:**
```tsx
import { TransitionSeries, springTiming } from "@remotion/transitions";
import { slide } from "@remotion/transitions/slide";

<TransitionSeries>
  {slides.map((s, i) => (
    <React.Fragment key={i}>
      <TransitionSeries.Sequence durationInFrames={60}>
        <SlideScene theme={theme} imageSrc={s.image} title={s.title} />
      </TransitionSeries.Sequence>
      {i < slides.length - 1 && (
        <TransitionSeries.Transition
          presentation={slide({ direction: "from-right" })}
          timing={springTiming({ config: SPRING_PRESETS.text })}
        />
      )}
    </React.Fragment>
  ))}
</TransitionSeries>
```

### 5. Duration Calculation

```
Total = Intro + (Slides * SlideDuration) + Outro

Typical durations:
- Post (no slides): 150 frames (5 sec)
- Post carousel: 60 + (N * 60) + 90
- Reel showcase: 90 + (N * 60) + 150
- Reel tutorial: 60 + (N * 90)
- Reel countdown: (N * 30) + 120
```

### 6. Checklist Before Committing

- [ ] Zod schema has defaults for ALL fields
- [ ] `import "../../fonts"` present
- [ ] No unused imports (tsc --noEmit passes)
- [ ] For reels: SafeZone wraps all critical content
- [ ] Font sizes meet minimums (24px post, 36px reel body)
- [ ] Italian text has correct accents
- [ ] Registered in Root.tsx
- [ ] `npx remotion still` renders without errors
