---
name: anti-slop-design
description: >
   Prevents generic, "AI-made" frontend design. Use when building or restyling
   UI to get a distinctive look with deliberate typography, color, motion, and layout.
metadata:
  author: niamkvn
  version: 1.0.0
---

# Anti Slop Design

Prevent frontend design that feels "AI-made".

## AI Slop Signs (forbidden)

- Default fonts: Inter/Roboto/Arial/system fonts, also Space Grotesk
- Purple gradients on a white background
- Uniform rounded corners
- Center-aligned layouts only
- Clichéd hero section + 3-column feature grid
- Identical shadows on every card
- Illustrations with no character

## Workflow

### 1. Concept

- Purpose and users: what problem is being solved, and for whom?
- Tone (pick one, commit to it): brutalism, minimal, maximalist, retrofuturism, organic, luxury, playful, editorial, art deco, industrial, soft pastel, 80s neon, Japanese minimalism
- Differentiator: one element the user will remember
- Technical constraints: framework, performance, accessibility

### 2. Build

Production-ready code: HTML/CSS/JS, Svelte, Vue, React, etc.

- **Typography:** characterful fonts (Google Fonts); pair a display font with a body font
- **Color:** CSS variables; one dominant color + a sharp accent; an uncommon palette
- **Motion:** staggered reveal on load; unexpected hover/scroll effects; CSS for HTML, Motion library for Svelte
- **Space:** asymmetry, overlap, diagonal flow, elements breaking out of the grid; whitespace that is either generous or dense, by intention
- **Background:** never a default solid color; use gradient mesh, noise, geometric patterns, layered transparency, dramatic shadows, decorative borders
- **Code complexity:** match the vision; maximalism needs elaborate code, minimalism needs precise spacing and typography

### 3. Verify

Check visual hierarchy, interactions, animations, and accessibility. Make sure there are asymmetric elements and no AI Slop signs remain.