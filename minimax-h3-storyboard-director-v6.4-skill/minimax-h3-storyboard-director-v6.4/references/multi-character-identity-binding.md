# Multi-Character Identity Binding｜V6.4

## Goal

Prevent character A/B face swaps, identity leakage, and subject reassignment across all shots in a 15-second scene when multiple V6.1 character sheets are supplied.

## Permanent Binding Chain

For every important character create one immutable chain:

`V6.1 character picture → permanent <Subject N> → shot spatial state → optional permanent speaker ID (Sx)`

Example:

```text
<Picture 1> = single 16:9 pure-background reference image derived from the target video prompt; environment and spatial continuity only, with no people or characters
<Picture 2> = Character A V6.1 Face-Master Sheet
<Picture 3> = Character B V6.1 Face-Master Sheet

<Subject 1> = Character A only
<Subject 2> = Character B only

<Subject 1> ↔ (S1) if Character A speaks
<Subject 2> ↔ (S2) if Character B speaks
```

## Reference Responsibility Isolation

- `<Picture 1>` pure-background reference: environment layout, spatial depth, lighting, atmosphere, environmental props, and overall composition only. It contains no people, characters, silhouettes, shadows, reflections, body parts, or crowds; shot order and action progression come from the written shot plan.
- `<Picture 2>`: Character A identity/appearance only.
- `<Picture 3>`: Character B identity/appearance only.
- No blocking figure or other person may appear in the pure-background reference. Character identity comes exclusively from the corresponding V6.1 Master Face Sheet.

## Subject Definition Pattern

```text
<Subject 1> is [Character A], whose facial identity and stable appearance come exclusively from <Picture 2>. The large frontal Master Face in <Picture 2> is the authoritative identity source; its left/right 45-degree views only support rotational geometry, while its body views only support body shape, hairstyle structure, clothing, and accessories. <Subject 1> must never inherit facial or appearance traits from <Subject 2> or <Picture 3>.

<Subject 2> is [Character B], whose facial identity and stable appearance come exclusively from <Picture 3>. The large frontal Master Face in <Picture 3> is the authoritative identity source; its auxiliary views are secondary support only. <Subject 2> must never inherit facial or appearance traits from <Subject 1> or <Picture 2>.
```

## Shot-by-Shot Binding

At the beginning of every multi-character shot, bind identity before action:

`identity → position/depth → facing direction → pose → action`

Example:

```text
[Shot 4] At 00:05.200, <Subject 1>, [Character A], remains in the left foreground facing right, while <Subject 2>, [Character B], stays in the right midground facing left. <Subject 1> turns her head toward <Subject 2>...
```

Do not rely only on `the woman`, `the man`, `she`, `he`, or screen-side shorthand after a cut.

## Crossing and Re-entry

Screen position is not identity. If subjects exchange sides, show the crossing movement while retaining the same Subject IDs. A subject leaving frame, being occluded, or returning after a single-character cut keeps the same permanent `<Subject N>`.

## Retention Pattern

```text
<Picture 1> (character-free pure-background reference derived from the approved target-video prompt): fully_preserved - environment layout, spatial depth, lighting logic, atmosphere, and key environmental props are retained; it contains no people or character traces and does not prescribe shot order, blocking, action, or identity.
<Subject 1> (...): fully_preserved - [Character A]'s facial identity remains exclusively derived from the Master Face in <Picture 2>; no traits from <Subject 2> or <Picture 3> transfer to <Subject 1>.
<Subject 2> (...): fully_preserved - [Character B]'s facial identity remains exclusively derived from the Master Face in <Picture 3>; no traits from <Subject 1> or <Picture 2> transfer to <Subject 2>.
```

## Secondary Identity Signature

When faces are small, support identity using stable non-face cues: hairstyle silhouette, body type, skin tone, costume silhouette, accessories, and other confirmed visual signatures. These are secondary and never override the Master Face.

## Speaker Binding

If characters speak, keep a stable mapping such as `<Subject 1> ↔ (S1)` and `<Subject 2> ↔ (S2)` for the entire video. Never swap speaker IDs after a cut or side change.

## Multi-Character Self-Check

- Every character has one permanent Subject ID.
- Every Subject has one exclusive V6.1 identity source.
- The pure-background reference contains no figures; character identity comes only from the character sheet.
- Every multi-character shot re-states visible Subjects and spatial state.
- Side changes are shown as movement, not instantaneous identity swaps.
- Re-entry uses the original Subject ID.
- No facial/appearance traits transfer across Subjects.
- Speaker IDs remain paired with the same Subjects.
