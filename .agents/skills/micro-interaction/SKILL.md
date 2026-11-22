---
name: micro-interaction
description: >
   Fully specifies a micro-interaction using the Trigger, Rules, Feedback,
   Loops and Modes framework. Use when designing or documenting UI micro-interactions.
metadata:
  author: niamkvn
  version: 1.0.0
---

# Micro-Interaction

Specify a micro-interaction completely using the framework below.

## Framework

### 1. Trigger

What starts it:

- User action (click, hover, swipe)
- System event (notification, completion)
- Conditional (time, threshold)

### 2. Rules

Logic and sequence after the trigger fires, including conditions and branching.

### 3. Feedback

The response the user perceives:

- Visual (color, size, position)
- Motion
- Audio
- Haptic

### 4. Loops and Modes

- Does it repeat or change over time?
- First-time vs repeat behavior
- Progressive disclosure

## Specification Format

Name, trigger, rules (in order), feedback (visual/audio/haptic), duration/easing, loop behavior, accessibility.

## Best Practices

- Give every micro-interaction a clear purpose
- Keep durations short (100-500ms for most cases)
- Give immediate feedback for user actions
- Respect reduced-motion preferences
- Test performance on target devices