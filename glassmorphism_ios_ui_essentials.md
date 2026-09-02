# Glassmorphism & iOS-Style UI Essentials

A practical design reference for building polished interfaces inspired by **glassmorphism** and **modern iOS design**.

---

## 1. Core Design Philosophy

The goal is not to make everything look like glass.

Use glass effects to create:

- Depth
- Layering
- Visual hierarchy
- Spatial separation
- A sense of lightness
- Clear focus on important content

A good glass UI should still work when the blur is removed.

### The basic formula

```text
Background
    ↓
Ambient color / imagery
    ↓
Blurred glass surface
    ↓
Subtle border + highlight
    ↓
Content
    ↓
Shadow / depth
```

---

# 2. Glassmorphism Essentials

## 2.1 Semi-Transparent Surfaces

Glass panels should reveal a small amount of what is behind them.

Typical starting points:

```css
background: rgba(255, 255, 255, 0.15);
```

For dark interfaces:

```css
background: rgba(20, 20, 25, 0.35);
```

Avoid making surfaces completely opaque unless the component needs maximum readability.

### Rule

> The glass should feel translucent, not invisible.

---

## 2.2 Backdrop Blur

The signature effect is background blur.

```css
backdrop-filter: blur(20px);
-webkit-backdrop-filter: blur(20px);
```

Useful ranges:

| Blur | Typical Use |
|---|---|
| `8px` | Subtle surfaces |
| `12px` | Small controls |
| `16px` | Cards |
| `20px` | Navigation / prominent panels |
| `24px` | Modals / floating surfaces |
| `32px+` | Strong atmospheric glass |

More blur is not automatically better.

---

## 2.3 Saturation

A small amount of saturation can make the glass feel richer.

```css
backdrop-filter: blur(20px) saturate(140%);
```

Useful range:

```text
120% → subtle
140% → balanced
160% → vivid
180%+ → dramatic
```

Use stronger saturation when the background contains colorful gradients or imagery.

---

## 2.4 Glass Borders

A glass surface usually needs a very subtle border.

```css
border: 1px solid rgba(255, 255, 255, 0.20);
```

For dark themes:

```css
border: 1px solid rgba(255, 255, 255, 0.10);
```

The border should imply light hitting the edge.

Avoid:

```css
border: 2px solid white;
```

This usually looks too harsh.

---

## 2.5 Inner Highlight

A subtle inner highlight makes glass feel physical.

```css
box-shadow:
  inset 0 1px 0 rgba(255, 255, 255, 0.20);
```

You can combine it with an outer shadow:

```css
box-shadow:
  inset 0 1px 0 rgba(255, 255, 255, 0.20),
  0 12px 40px rgba(0, 0, 0, 0.12);
```

---

# 3. Backgrounds

Glass needs something behind it to reveal the effect.

Good backgrounds include:

- Soft gradients
- Large blurred color fields
- Photos
- Abstract shapes
- Subtle noise
- Atmospheric lighting

Example:

```css
background:
  radial-gradient(circle at 20% 20%, rgba(120, 160, 255, 0.35), transparent 35%),
  radial-gradient(circle at 80% 70%, rgba(255, 120, 200, 0.30), transparent 35%),
  #f4f5f8;
```

### Background rule

Keep the background visually interesting but not so detailed that text becomes difficult to read.

---

# 4. iOS-Style UI Essentials

Modern iOS-inspired UI is more than rounded corners.

The key concepts are:

- Clear hierarchy
- Generous spacing
- Strong typography
- Large touch targets
- Familiar controls
- Layered surfaces
- Soft depth
- Restrained animation
- Context-aware navigation

---

# 5. Typography

For Apple-like interfaces, use a clean system font when available.

### CSS

```css
font-family:
  -apple-system,
  BlinkMacSystemFont,
  "SF Pro Display",
  "SF Pro Text",
  "Segoe UI",
  sans-serif;
```

Do not depend on a proprietary font being available.

### Suggested type hierarchy

```text
Large Title     34px / bold
Title           28px / bold
Headline        22px / semibold
Title 2         20px / semibold
Title 3         17px / semibold
Body            17px / regular
Callout         16px / regular
Subheadline     15px / regular
Footnote        13px / regular
Caption         12px / regular
```

The exact values can change based on platform and screen size.

---

# 6. Spacing

Use a consistent spacing system.

A simple scale:

```text
4px
8px
12px
16px
20px
24px
32px
40px
48px
64px
```

Common patterns:

```text
Screen padding:     16–24px
Card padding:       16–24px
Between sections:   24–40px
Icon/text gap:      8–12px
Button height:      44–52px
```

### iOS-style principle

> Give important content room to breathe.

Do not cram every element into the smallest possible space.

---

# 7. Corner Radius

Rounded surfaces are important, but the radius should match the component.

Suggested starting points:

| Component | Radius |
|---|---:|
| Small control | 10–12px |
| Button | 12–16px |
| Card | 18–24px |
| Large panel | 24–32px |
| Floating sheet | 28–36px |
| Pill | `9999px` |

Use fewer radius values across the system to keep the design coherent.

---

# 8. Buttons

A modern iOS-style button should be:

- Easy to recognize
- Large enough to tap
- Visually simple
- Clearly separated from secondary actions

Example:

```css
.button {
  min-height: 48px;
  padding: 0 20px;
  border-radius: 14px;
  font-weight: 600;
}
```

### Primary button

Use a strong solid or glass-filled surface.

### Secondary button

Use:

- translucent glass
- outline
- low-contrast fill

### Tertiary action

Use simple text or iconography.

Do not give every button the same visual weight.

---

# 9. Navigation

Modern iOS-inspired navigation tends to use:

- Large titles
- Simple icons
- Bottom tab bars
- Floating controls
- Clear active states

A bottom navigation bar can use glass:

```css
.tab-bar {
  background: rgba(255, 255, 255, 0.18);
  backdrop-filter: blur(24px) saturate(140%);
  -webkit-backdrop-filter: blur(24px) saturate(140%);
  border: 1px solid rgba(255, 255, 255, 0.18);
}
```

Keep navigation visually quieter than the main content.

---

# 10. Cards

A good glass card generally needs:

```css
.card {
  background: rgba(255, 255, 255, 0.16);
  backdrop-filter: blur(20px) saturate(140%);
  -webkit-backdrop-filter: blur(20px) saturate(140%);
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 22px;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.18),
    0 12px 40px rgba(0, 0, 0, 0.10);
}
```

### Do not stack excessive cards

If everything is a card, nothing feels important.

Use surfaces to define hierarchy.

---

# 11. Sheets and Modals

Floating sheets work especially well with glass.

Recommended structure:

```text
Background
      ↓
Dim / blur layer
      ↓
Floating sheet
      ↓
Handle
      ↓
Title
      ↓
Content
      ↓
Actions
```

Example:

```css
.sheet {
  border-radius: 30px 30px 0 0;
  background: rgba(255, 255, 255, 0.22);
  backdrop-filter: blur(30px) saturate(150%);
  -webkit-backdrop-filter: blur(30px) saturate(150%);
}
```

Use a small drag handle:

```css
.handle {
  width: 36px;
  height: 5px;
  border-radius: 999px;
  background: rgba(0, 0, 0, 0.18);
}
```

---

# 12. Inputs and Forms

Inputs should remain highly readable.

Example:

```css
.input {
  background: rgba(255, 255, 255, 0.18);
  border: 1px solid rgba(255, 255, 255, 0.16);
  border-radius: 14px;
  min-height: 48px;
  padding: 0 16px;
  backdrop-filter: blur(12px);
}
```

### Focus state

Use a clear focus ring.

```css
.input:focus {
  outline: 2px solid rgba(0, 122, 255, 0.55);
  outline-offset: 2px;
}
```

Never rely on glass alone to communicate focus.

---

# 13. Colors

A simple iOS-inspired palette often starts with:

```text
Background
Surface
Elevated Surface
Primary Text
Secondary Text
Tertiary Text
Accent
Destructive
Success
Warning
```

Example CSS variables:

```css
:root {
  --background: #f5f5f7;
  --surface: rgba(255, 255, 255, 0.55);

  --text-primary: rgba(0, 0, 0, 0.90);
  --text-secondary: rgba(0, 0, 0, 0.60);
  --text-tertiary: rgba(0, 0, 0, 0.40);

  --accent: #007aff;
  --destructive: #ff3b30;
  --success: #34c759;
  --warning: #ff9500;
}
```

For a dark theme:

```css
:root {
  --background: #0b0b0f;
  --surface: rgba(30, 30, 35, 0.55);

  --text-primary: rgba(255, 255, 255, 0.95);
  --text-secondary: rgba(255, 255, 255, 0.65);
  --text-tertiary: rgba(255, 255, 255, 0.45);
}
```

---

# 14. Shadows and Depth

Glass usually needs softer shadows than traditional material-style UI.

Avoid overly dark shadows:

```css
/* Too heavy */
box-shadow: 0 20px 50px rgba(0, 0, 0, 0.35);
```

Prefer:

```css
box-shadow:
  0 10px 30px rgba(0, 0, 0, 0.10);
```

For stronger floating elements:

```css
box-shadow:
  0 20px 60px rgba(0, 0, 0, 0.15);
```

Use depth sparingly.

---

# 15. Iconography

Use simple, consistent icons.

Good icon characteristics:

- Simple shapes
- Consistent stroke weight
- Optical balance
- Clear active/inactive states
- Adequate tap area

For an iOS-inspired style, familiar symbols often work better than decorative icons.

### Important

The icon itself can be small, but its interactive area should be larger.

Example:

```css
.icon-button {
  width: 44px;
  height: 44px;
  display: grid;
  place-items: center;
}
```

---

# 16. Animation

Animation should explain state changes.

Use:

- Fade
- Scale
- Slide
- Spring-like easing
- Blur transitions
- Opacity transitions

Example:

```css
transition:
  transform 180ms ease,
  opacity 180ms ease,
  background 180ms ease;
```

For a subtle interaction:

```css
.button:active {
  transform: scale(0.97);
}
```

### Avoid

```text
Huge bounce
Constant motion
Long transitions
Decorative animation everywhere
```

The interface should feel responsive, not theatrical.

---

# 17. Microinteractions

Useful microinteractions include:

### Button press

```text
Normal → slightly smaller → return
```

### Toggle

```text
Off → thumb slides → background changes
```

### Modal

```text
Fade background
+
Sheet moves upward
+
Slight blur transition
```

### Navigation

```text
Selected icon becomes emphasized
+
Label becomes clearer
```

Keep motion under user control where possible.

---

# 18. Accessibility

Beautiful glass UI is useless if users cannot read it.

## Contrast

Check text against the **actual rendered background**, not only the base page color.

Potential problems:

- White text over bright images
- Thin gray text
- Low-opacity labels
- Transparent buttons over busy backgrounds

### Add a fallback

```css
background:
  rgba(255, 255, 255, 0.65);
```

Instead of relying entirely on:

```css
background:
  rgba(255, 255, 255, 0.10);
```

---

## Reduced Motion

Respect user preferences:

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

---

# 19. Fallback for Backdrop Blur

`backdrop-filter` is not always available or equally performant.

Provide a readable fallback:

```css
.glass {
  background: rgba(255, 255, 255, 0.65);
}

@supports (backdrop-filter: blur(20px)) {
  .glass {
    background: rgba(255, 255, 255, 0.18);
    backdrop-filter: blur(20px) saturate(140%);
    -webkit-backdrop-filter: blur(20px) saturate(140%);
  }
}
```

---

# 20. Performance

Blur can be expensive, especially across large surfaces.

### Prefer

```text
Small glass panels
Moderate blur
Limited layered surfaces
Static backgrounds
```

### Avoid

```text
Huge full-screen blur layers
Many overlapping blurred elements
Very high blur values everywhere
Animating large blurred regions
```

A practical rule:

> Use blur where it communicates depth. Do not use blur just because it looks cool.

---

# 21. Common Mistakes

## Mistake 1: Too Much Glass

If every component is translucent, hierarchy disappears.

### Better

Use glass for:

- Navigation
- Floating controls
- Cards
- Sheets
- Modals
- Important grouped content

---

## Mistake 2: Weak Contrast

Transparent text can become unreadable.

### Better

Increase:

- Surface opacity
- Text contrast
- Background separation

---

## Mistake 3: Excessive Blur

Huge blur values can make the UI muddy.

### Better

Start around:

```text
12–24px
```

Then increase only when needed.

---

## Mistake 4: Random Corner Radii

Using 11px, 17px, 23px, 31px, and 37px everywhere makes the design feel inconsistent.

### Better

Create a radius system:

```text
Small: 12px
Medium: 16px
Large: 24px
XL: 32px
Pill: 9999px
```

---

## Mistake 5: Everything Floats

If every object has shadows, the interface loses a clear visual hierarchy.

### Better

Use three depth levels:

```text
Level 0 → background
Level 1 → normal surfaces
Level 2 → floating surfaces / controls
```

---

# 22. Recommended Design Tokens

A practical starting token system:

```css
:root {
  /* Spacing */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 20px;
  --space-6: 24px;
  --space-7: 32px;
  --space-8: 40px;
  --space-9: 48px;

  /* Radius */
  --radius-sm: 12px;
  --radius-md: 16px;
  --radius-lg: 24px;
  --radius-xl: 32px;
  --radius-pill: 9999px;

  /* Glass */
  --glass-bg: rgba(255, 255, 255, 0.16);
  --glass-border: rgba(255, 255, 255, 0.18);
  --glass-blur: 20px;
  --glass-saturation: 140%;

  /* Shadows */
  --shadow-soft:
    0 10px 30px rgba(0, 0, 0, 0.10);

  --shadow-floating:
    0 20px 60px rgba(0, 0, 0, 0.15);
}
```

---

# 23. Reusable Glass Component

```css
.glass {
  background: rgba(255, 255, 255, 0.16);

  border: 1px solid rgba(255, 255, 255, 0.18);

  border-radius: 24px;

  backdrop-filter:
    blur(20px)
    saturate(140%);

  -webkit-backdrop-filter:
    blur(20px)
    saturate(140%);

  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.18),
    0 10px 30px rgba(0, 0, 0, 0.10);
}
```

---

# 24. A Better Glass Hierarchy

Do not use one glass style for everything.

Create several levels.

## Glass 1 — Subtle

```css
background: rgba(255, 255, 255, 0.10);
backdrop-filter: blur(12px);
```

Use for:

- Toolbars
- Secondary controls
- Background navigation

## Glass 2 — Standard

```css
background: rgba(255, 255, 255, 0.16);
backdrop-filter: blur(20px);
```

Use for:

- Cards
- Panels
- General surfaces

## Glass 3 — Elevated

```css
background: rgba(255, 255, 255, 0.22);
backdrop-filter: blur(28px);
```

Use for:

- Modals
- Sheets
- Floating action panels

---

# 25. iOS-Like Layout Pattern

A clean application layout can follow:

```text
┌─────────────────────────────┐
│ Status / top safe area      │
│                             │
│ Large Title                 │
│ Supporting information      │
│                             │
│ ┌─────────────────────────┐ │
│ │ Glass Card              │ │
│ │                         │ │
│ │ Main content            │ │
│ └─────────────────────────┘ │
│                             │
│ Section                     │
│                             │
│ ┌───────────┐ ┌───────────┐ │
│ │ Card      │ │ Card      │ │
│ └───────────┘ └───────────┘ │
│                             │
│                             │
│    ┌─────────────────────┐  │
│    │  Glass Navigation   │  │
│    └─────────────────────┘  │
└─────────────────────────────┘
```

Think in **layers and hierarchy**, not individual decorations.

---

# 26. Design Checklist

Before shipping a glassmorphism / iOS-inspired interface, check:

### Visual

- [ ] Glass is translucent rather than fully transparent
- [ ] Blur is visible but not excessive
- [ ] Borders are subtle
- [ ] Shadows are soft
- [ ] Background provides enough visual material
- [ ] Corner radii are consistent
- [ ] Depth levels are obvious

### Typography

- [ ] Primary text has strong contrast
- [ ] Secondary text is still readable
- [ ] Heading hierarchy is obvious
- [ ] Font sizes are consistent
- [ ] Line height is comfortable

### Interaction

- [ ] Buttons are easy to tap
- [ ] Interactive elements have clear states
- [ ] Focus states are visible
- [ ] Press states feel responsive
- [ ] Animation is restrained
- [ ] Reduced-motion preference is respected

### Accessibility

- [ ] Text remains readable over changing backgrounds
- [ ] Important information does not depend on transparency
- [ ] Color is not the only way to communicate state
- [ ] Keyboard focus is visible
- [ ] Blur has a readable fallback

### Performance

- [ ] Large blur regions are limited
- [ ] Multiple glass layers do not overlap unnecessarily
- [ ] Animations do not constantly animate large blurred surfaces
- [ ] Mobile performance has been tested

---

# 27. The Golden Rules

```text
1. Hierarchy before decoration.
2. Glass creates depth, not content.
3. Keep transparency controlled.
4. Use blur with purpose.
5. Protect text contrast.
6. Keep spacing generous.
7. Use consistent radii.
8. Limit the number of floating layers.
9. Make interactions obvious.
10. Design for accessibility first.
```

## Final Mental Model

Think of the interface as **physical layers of frosted material floating above an ambient environment**.

```text
Background
   ↓
Atmosphere
   ↓
Glass
   ↓
Content
   ↓
Interaction
   ↓
Depth
```

The best glass UI does not scream:

> "Look, I used backdrop-filter!"

It quietly communicates:

> "This element sits here, above everything else."

