# PRD Addendum: Engagement and Character System

## Purpose

This addendum defines the emotional, motivational, and character-driven behavior layer for Maltese Quest V1. It expands the PRD with the engagement engine, mascot states, reward balancing rules, and the hero/rival narrative model.

## System overview

The product shall map learner behaviors to emotional states and reward outputs. Core inputs include correct pronunciation, streak maintenance, session completion, retry after error, help request, and return after absence. The system shall consider learner age band, current challenge level, session length, and feedback density before selecting a response.

## Design goals

- Protect confidence and reduce speaking anxiety.
- Keep children engaged without over-rewarding every action.
- Make the experience feel warm, playful, and story-driven.
- Shift from visible celebration to quieter progress signals when fatigue risk rises.
- Support children aged 7–9 first, while allowing age-based tuning later.

## Behavior-to-reward mapping

| Behavior | Emotional state | Mascot reaction | Reward output |
|---|---|---|---|
| Correct pronunciation | Celebratory | Quick proud animation, bright praise line | XP, combo progress, occasional story unlock |
| Streak maintenance | Encouraging | Nodding, soft wag, effort-focused comment | Small XP, consistency badge segment |
| Session completion | Celebratory | Short hop, calm success pose | Chapter progress, milestone reveal |
| Retry after error | Empathetic | Soft eyes, low-motion hint pose | Minimal XP, scaffolded retry path |
| Help request | Encouraging | Crouch-to-eye-level help pose | Hint quality increase, no badge |
| Return after absence | Empathetic | Warm welcome-back pose | Comeback bonus, no streak shame |

## Age-band balancing

The reward system shall vary by age band:

- Ages 5–7: higher reward visibility, larger animations, simpler praise.
- Ages 8–10: balanced rewards, clear map progress, moderate animation.
- Ages 11–13: lower celebration frequency, more autonomy, subtler praise.

V1 targets ages 7–9, so the default behavior should sit in the middle of this range: visible but not excessive, warm but not childish, and always confidence-preserving.

## Mascot states

### Encouraging
Used for routine effort, help-seeking, and streak maintenance. The mascot should appear friendly, calm, and supportive.

### Celebratory
Used for mastery, completion, and meaningful breakthroughs. The mascot should show a brief burst of energy, then return to rest.

### Empathetic
Used after errors, pauses, or returns after absence. The mascot should reduce motion, lower visual intensity, and avoid disappointment cues.

## Reward fatigue guardrails

- No major animation burst inside 25 seconds.
- No badge award for help requests or first recovery attempts.
- Rewards should shift from XP bursts to progress meters when feedback density rises.
- No shame-based responses after errors or missed sessions.
- Narrative unlocks should be preferred over constant prize feedback.

## Character system

### Benni
Benni is the primary hero character. Benni should feel empathetic, optimistic, and dependable. Benni is the child’s guide, coach, and confidence-builder.

### Waffles
Waffles is a playful rival character. Waffles should feel humorous, rule-obsessed, and mildly competitive, never threatening. Waffles exists to create narrative tension and boss-lite challenge moments, not fear.

### Character rules

- Benni appears in daily lessons, feedback, and recovery moments.
- Waffles appears only in narrative arcs, special challenges, or boss-lite progression moments.
- The villain should never use shame, menace, or punishment language.
- The relationship must remain “rival not enemy.”

## UI and motion rules

- Use short, readable mascot animations.
- Respect reduced-motion preferences.
- Keep audio cues softer than speech.
- Avoid repetitive confetti or spark bursts.
- Prefer calm success states after every major celebration.

## Example user story

As a 7-year-old learner, when I retry a hard word correctly after making a mistake, I want the mascot to encourage me and give me a small reward so I feel proud and keep going.

## Success metrics

- Lesson completion rate.
- Speaking challenge completion rate.
- Retry recovery rate.
- Return rate after absence.
- Parent-rated child confidence.
- Reward fatigue signals, such as drop-off after repeated celebrations.

## Open questions

- Final mascot names and visual style.
- Exact frequency thresholds for each age band.
- Which character phrases are text-only vs voiced.
- Whether Waffles becomes part of later content packs only.
- Whether parents can switch between Benni-only mode and Benni/Waffles mode.
