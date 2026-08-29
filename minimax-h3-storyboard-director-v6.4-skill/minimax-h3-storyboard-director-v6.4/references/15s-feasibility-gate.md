# 15s Capacity Gate｜15秒容量闸门（V6.4）

## Purpose

Run this gate after the 15-second scene content and written shot plan are drafted, before generating the matching pure-background reference image and final H3 prompt. The gate keeps pacing efficient by using two clear capacity limits instead of conservative per-second performance estimates.

## Hard Pass Rules

A 15-second segment passes when both conditions are true:

1. **Total dialogue ≤ 40 characters.**
2. **Distinct visible actions ≤ 6.**

Do not apply the retired 2.2–2.6 Chinese-characters-per-second baseline, GREEN/YELLOW/RED 11s/13s bands, 13-second mandatory-content target, or mandatory 2-second buffer. Those rules must not be used to slow or automatically split an otherwise compliant segment.

## Dialogue Counting

Count all spoken content assigned to the segment, including on-screen dialogue, off-screen voiceover, narration, and lyrics.

- For Chinese, count Chinese characters; punctuation, spaces, line breaks, and speaker labels do not count.
- For mixed-language content, count the visible letters/numbers that form the spoken text; punctuation and spaces do not count.
- Count repeated words each time they are actually spoken.
- Preserve original dialogue verbatim. Do not paraphrase, delete, or accelerate it merely to fit the cap.
- If the total is **41 or more**, split at a natural dialogue or dramatic boundary.

## Action Counting

An action is a distinct, visible, must-complete character or object event with a readable start/change/result.

Count as one action when a continuous movement has one intent and one result, for example: “she crosses the room and stops at the door.” Count a new action when the intent changes or a separate result must be read, for example: “she stops, unlocks the door, opens it” contains three actions.

- Count character movements, prop interactions, reveals, entrances/exits, and required physical reactions when they are separate narrative events.
- Do not count a passive pose, facial baseline, static environment detail, camera cut, camera movement, lens choice, lighting description, ambient sound, or dialogue delivery as an action by itself.
- A reaction counts only when it is an explicit, visible, story-required change.
- If the total is **7 or more**, split at a natural completed-action boundary.

## Physical Plausibility Check

A segment that satisfies both numeric limits normally remains one 15-second video. Split it additionally only when the planned actions are physically incompatible or mutually dependent in a way that plainly cannot be completed within 15 seconds. Do not invent extra pauses, reaction holds, or camera-settle budgets solely to force a split.

## Written Beats Are Not Image Panels

The shot plan may use any reasonable number of written beats and H3 Shots. Several beats can remain in one continuous shot; a new Shot is created only when a meaningful viewpoint, composition, subject-focus, spatial, or narrative change benefits from a cut. The pure-background reference image contains none of these character/action beats.

## Dialogue and Action Count Audit

Perform twice: after drafting the shot plan and before final H3 delivery.

```text
Segment: [name/id]
Dialogue text: [verbatim text]
Dialogue character count: [N] / 40
Distinct visible actions:
1. [action]
2. [action]
...
Action count: [N] / 6
Physical plausibility: [pass / split required, brief reason]
Decision: [keep as one 15s segment / split into N segments]
```

The audit passes only when dialogue is ≤40 characters, actions are ≤6, and no clear physical impossibility remains.

## Split Logic

When a cap is exceeded, preserve every original line and required action, then split at a completed line, completed action, reaction, reveal, decision, entrance/exit, objective change, or clear hook. The ending state of segment A becomes the opening continuity state of segment B.

## Background Reference Dependency

Generate the pure-background reference only after the segment passes this gate and the target video-prompt content is approved. Extract environment information from that video content, but remove all characters, people, silhouettes, shadows, reflections, body parts, crowds, and character actions from the image prompt.
