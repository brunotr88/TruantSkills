# Team Workflow

## Team Configuration

Location: `~/.claude/teams/remotion-pro-studio/config.json`

### Agents

| Agent | Role | Specialization |
|-------|------|----------------|
| `team-lead` | Coordinator | Orchestration, code review, architecture decisions, task assignment |
| `animation-architect` | Motion specialist | Springs, easings, entrance/exit helpers, transitions, performance tuning |
| `template-builder` | Composition developer | Templates, layouts, scene system, Root.tsx, Zod schemas |
| `visual-effects` | VFX & polish | Effects (grain, particles, glow), themes, text animations, icons/emoji |

### When to Use the Team

Use `TeamCreate` with team `remotion-pro-studio` for:
- Creating multiple templates simultaneously
- Complex templates needing animation + VFX + layout expertise
- Refactoring the animation or theme system
- Adding new component categories

### Task Distribution Examples

**"Create 3 new reel templates":**
- team-lead: Plan schemas, coordinate, final review
- template-builder: Write component structure, scenes, Root.tsx registration
- animation-architect: Design animation timelines, spring configs
- visual-effects: Apply effects, theme integration, polish

**"Add a new animation preset":**
- animation-architect: Implement in springs.ts/entrance.ts
- visual-effects: Test in a preview composition
- template-builder: Update existing templates if needed

**"Create a custom theme for brand X":**
- visual-effects: Define colors, fonts, spacing
- template-builder: Verify all templates render correctly with new theme
- team-lead: Review WCAG contrast ratios

### Spawning the Team

```
Use TeamCreate with team_name: "remotion-pro-studio"
Then spawn agents with:
  - team_name: "remotion-pro-studio"
  - name: "animation-architect" (or other agent name)
  - subagent_type: "general-purpose"
```

Each agent has:
- model: claude-opus-4-6
- cwd: /mnt/c/PROGETTI/remotion-pro-studio
- Access to remotion-best-practices skill for Remotion rules
- Access to remotion-pro-studio skill for project-specific knowledge
