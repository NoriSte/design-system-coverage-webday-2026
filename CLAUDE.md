# CLAUDE.md - Presentation Customization Guide

This is a Slidev presentation (Vue 3 + Vite based). Use this guide for quick modifications.

## Quick Commands

```bash
npm run dev      # Start dev server (opens browser)
npm run build    # Build for production
npm run export   # Export to PDF
```

## Key Files for Customization

| What to Change   | File                  | Location in File              |
| ---------------- | --------------------- | ----------------------------- |
| Theme/Colors     | `slides.md`           | Frontmatter `theme:` (line 2) |
| Slide content    | `slides.md`           | Main content (734 lines)      |
| Animation slides | `bitmap-animation.md` | Included via `src:` directive |
| Export filename  | `slides.md`           | Frontmatter `exportFilename:` |
| Title            | `slides.md`           | Frontmatter `title:`          |

## Changing Colors

### Option 1: Switch Theme (Easiest)
In `slides.md` frontmatter, change `theme: seriph` to another installed theme:
- `seriph` (current) - Primary color: `#5d8392`
- `default` - Basic theme
- `apple-basic` - Apple-style
- `light-icons` - Light with icons
- `mint` - Mint green theme

### Option 2: Override Theme Colors
Create `styles/index.css` and override CSS variables:
```css
:root {
  --slidev-theme-primary: #your-color;
}
```

### Text Colors in Slides
Use Tailwind/UnoCSS classes directly in markdown:
- `text-red`, `text-orange`, `text-white`, `text-gray`
- `text-[#hexcolor]` for custom colors
- `bg-[#hexcolor]` for backgrounds

## Changing Fonts

### Option 1: Frontmatter Override
Add to `slides.md` frontmatter:
```yaml
fonts:
  sans: 'Your Font Name'
  serif: 'Your Serif Font'
  mono: 'Your Mono Font'
  weights: '400,700'
```

### Current Fonts (from seriph theme)
- Sans/Serif: PT Serif
- Mono: PT Mono
- Weights: 400, 700

## Changing Slide Dimensions

Add to `slides.md` frontmatter:
```yaml
aspectRatio: '16/9'    # Default, or try '4/3'
canvasWidth: 980       # Base canvas width in pixels
```

## Replacing Images/Screenshots

### Image Locations
```
/public/
├── images/          # Main images (cover, speakers)
├── images2/         # Additional images (diagrams, photos)
├── videos/          # Video files (slowmo1.mov, slowmo2.mov)
└── *.png            # Root level (dashboard, metrics, steps)
```

### How to Replace
1. Drop new image in `/public/` or subdirectory
2. Reference in slides as `/filename.png` or `/images/filename.jpg`
3. For background images: `background: /images/your-image.jpeg`
4. For inline images: `![alt](/images/your-image.png)`

### Current Key Images
- Cover background: `/images/cover_01.jpeg`
- Speaker photos: `/images/ste-1000x1000-progressive.jpg`, `/images/matteo01.jpg`
- QR code: `/qrcode.png`
- Dashboard screenshot: `/dashboard.png`
- Step diagrams: `/step1.png` through `/step6-2.png`

## Slide Layouts Available

Use in slide frontmatter with `layout:`:
- `default` - Standard slide
- `cover` - Full background with centered title
- `intro` - Introduction (full height)
- `statement` - Centered statement
- `center` - Centered content
- `section` - Section divider
- `image-left` - Two columns, image on left
- `image-right` - Two columns, image on right
- `two-cols` - Generic two columns

Example:
```md
---
layout: image-right
image: /images/your-image.jpg
---
# Your Title
Content here
```

## Frontmatter Reference (slides.md)

```yaml
theme: seriph                              # Theme name
transition: none                           # Slide transitions
background: /images/cover_01.jpeg          # Cover background
title: Design System Visual Coverage       # Presentation title
class: text-center                         # CSS class for first slide
exportFilename: design-coverage-jsday-2025 # PDF export name
download: true                             # Show download button
export:
  format: pdf
  dark: true                               # Dark mode export
  withClicks: true                         # Include click steps
```

## Common Modifications

### Change conference branding
1. Update `title:` in frontmatter
2. Replace `/images/cover_01.jpeg` with new cover
3. Update `exportFilename:` for new PDF name
4. Update QR code at `/qrcode.png` if needed

### Adjust text sizing
Use Tailwind classes: `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, `text-3xl`, `text-4xl`, `text-5xl`, `text-6xl`

### Add speaker info
Uses `image-right` or `image-left` layout with `image:` property

## Deployment

Configured for multiple platforms:
- **GitHub Pages**: Push to `main` branch (auto-deploys via `.github/workflows/deploy.yml`)
- **Vercel**: Auto-detects `vercel.json`
- **Netlify**: Auto-detects `netlify.toml`

## Video Embedding

```md
<SlidevVideo autoplay autoreset>
  <source src="/videos/your-video.mov" type="video/mp4" />
</SlidevVideo>
```

## Progressive Reveal (Animations)

Use `v-click` for step-by-step reveals:
```md
<v-click>

This appears on click

</v-click>
```

Or inline: `<span v-click>text</span>`
