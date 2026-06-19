# Technical Specification: Engagement Engine and Character System

## Purpose

This technical spec translates the simulator logic into implementation requirements for the Maltese Quest engagement engine, mascot system, and character-driven reward layer.

## Scope

The system shall support:

- Behavior detection.
- Context scoring.
- Age-band based motivation balancing.
- Mascot state selection.
- Reward throttling.
- Narrative unlock triggering.
- Accessibility support.
- Future reuse by the Kids Connect platform.

## Core architecture

### 1. Behavior event layer

The app shall emit normalized learner events such as:

- correct_pronunciation
- streak_maintenance
- session_completion
- retry_after_error
- help_request
- return_after_absence

Each event shall contain metadata including learner id, age band, timestamp, lesson context, challenge level, session duration, recent feedback count, and prior reward frequency.

### 2. Context scoring layer

The system shall compute a response context score from the event metadata. The score should influence:

- emotional state selection,
- reward size,
- animation strength,
- feedback density,
- whether a narrative unlock is appropriate.

### 3. Emotion selection layer

The system shall map events to one of three emotional states:

- celebratory,
- encouraging,
- empathetic.

The selection should prioritize the meaning of the behavior, not just its correctness.

### 4. Reward policy layer

The reward policy shall determine:

- visible celebration frequency,
- XP amount,
- badge eligibility,
- progress meter updates,
- story unlock timing.

Reward bursts shall be throttled to avoid fatigue and over-stimulation.

## Rules engine requirements

- No major animation burst inside 25 seconds.
- No badge award for help requests.
- No badge award for first recovery attempts.
- High fatigue pressure shall reduce animation intensity and shift rewards toward progress indicators.
- Older age bands shall receive more autonomy and less frequent overt celebration.
- Missed sessions shall never trigger shaming language.

## Character implementation

### Benni
Benni shall be the default hero mascot. Benni should have:

- encouraging expressions,
- celebratory states,
- empathetic recovery states,
- short voice and text lines.

### Waffles
Waffles shall be implemented as a narrative rival. Waffles should:

- appear only in special arcs,
- use playful challenge lines,
- avoid menace or fear,
- never directly shame the learner.

## Asset requirements

- Mascot illustrations in vector or high-resolution SVG/PNG.
- Separate artwork layers for expressions, ears, eyes, mouth, and action accents.
- Animated states for encourage, celebrate, and empathize.
- Optional reduced-motion fallback frames.

## Audio requirements

- Short spoken lines for mascot prompts.
- Soft audio cues for correct answers and milestones.
- Clear distinction between speech and effects.
- Audio volume must stay below or equal to voice volume.

## Performance requirements

- Mascot animations shall remain smooth on mobile and desktop browsers.
- The page shall remain responsive with the simulator logic loaded.
- Reward evaluation shall occur instantly after event submission.
- Reduced-motion preference shall disable non-essential animation.

## Accessibility requirements

- Keyboard navigation shall be supported.
- Focus states shall remain visible.
- Contrast shall remain readable in light and dark themes.
- Motion shall respect user preferences.
- Mascot feedback shall have text equivalents for voiced cues.

## Data model requirements

The data model should include:

- users / parents,
- child profiles,
- approved contacts,
- behavior events,
- reward events,
- mascot state history,
- narrative unlock history,
- age-band configuration,
- fatigue threshold settings.

## API and module boundaries

The engagement engine should be separable into reusable modules:

- event ingestion,
- rules evaluation,
- reward calculation,
- character selection,
- notification generation,
- progress tracking.

This modularity is required so the same identity and contact system can later support Kids Connect.

## Logging and analytics

The system shall log:

- behavior type,
- emotional state chosen,
- reward tier,
- throttling decision,
- age band,
- feedback density,
- session length,
- fatigue flags.

These logs shall be used for product iteration, not for public child exposure.

## Testing requirements

- Validate behavior-to-emotion mapping.
- Validate reward throttle timing.
- Validate age-band differences.
- Validate no shame responses are emitted.
- Validate reduced-motion behavior.
- Validate Benni and Waffles appear only in the correct contexts.

## Deployment notes

The current simulator may be published as a single-page static app.
For V1 product work, the engagement engine should be implemented as a reusable front-end logic module with a clear event interface.

## Open implementation questions

- Where state should live: client, server, or hybrid.
- Whether reward rules are configuration-driven or hard-coded for V1.
- Whether voice lines are pre-recorded or generated.
- Whether Waffles is part of the base bundle or loaded as optional content.
- Whether reward tuning is editable in an admin panel.
