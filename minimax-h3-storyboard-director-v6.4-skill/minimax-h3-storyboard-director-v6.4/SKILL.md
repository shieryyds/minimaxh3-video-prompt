---
name: minimax-h3-storyboard-director-v6-4
description: Plan identity-stable 16:9 MiniMax H3 productions from scripts using V6.1 Face-Master single-image character references, multi-character Subject binding, a 15-second capacity gate capped at 40 dialogue characters and 6 actions, a character-free 16:9 background reference image derived from the target video prompt, plus written shot beats, and official H3 T2VA/I2VA/FL2VA/L2VA/Ref2VA prompt formats. Use when turning scripts, story concepts, character references, or storyboards into executable MiniMax H3 production prompts without rushing dialogue or actions.
compatibility: Portable to any agent that can read local files. No external API, proprietary runtime, or OpenAI-only feature is required. The agents/openai.yaml file is optional UI metadata only.
---

# MiniMax H3 Storyboard Director V6.4

## Core Workflow

1. Read the full script/story first. Ask only for information that is genuinely missing.
2. Lock characters and create one V6.1 Face-Master reference image per important character. Read `references/v6-1-character-sheet.md`.
3. **Default Character-Sheet UX:** when the user supplies a raw character reference, output **one complete V6.1 Character Sheet prompt**, ready to copy and use. Do not expose the internal left-45/right-45/front-body/back-body sub-prompts unless the user explicitly requests strict split generation/compositing.
4. Draft the 15-second video-prompt content and run the **15s Capacity Gate**: total dialogue must be no more than 40 characters and the segment must contain no more than 6 distinct visible actions. Read `references/15s-feasibility-gate.md`.
5. Split a story unit only when dialogue exceeds 40 characters, actions exceed 6, or the actions are physically incompatible with a 15-second performance. Preserve all script content across the split.
6. From the approved target-video prompt content, extract only the environment and generate one single 16:9 pure-background reference image. It must contain no person, character, human figure, silhouette, shadow, reflection, body part, portrait, or crowd. Keep all character blocking, action, dialogue, and performance exclusively in the written shot plan and H3 prompt.
7. For multi-character scenes, apply permanent Subject Identity Binding. Read `references/multi-character-identity-binding.md`.
8. Confirm background references and written shot plans, then create/confirm a Style Bible.
9. Identify the MiniMax H3 input mode. For T2VA/I2VA/FL2VA/L2VA read `references/h3-official-base-en.txt`; for Ref2VA read `references/h3-official-ref-en.txt`.
10. Preserve official H3 field names, field order, reference labels, speaker syntax, and timing notation exactly.
11. For the complete director workflow and delivery checks, read `references/director-workflow.md`.

## Character Sheet Output Modes

### Mode A — Unified Prompt (DEFAULT)
Use this unless the user explicitly asks otherwise.

- Return **one complete prompt** describing the entire 2304×1296 V6.1 Face-Master sheet.
- The prompt must include the Master Face, both 45° Rotation Anchors, front Body Appearance, back Body Appearance, layout, identity priority, makeup/hair lock, and negative constraints in one coherent block.
- Do **not** separately display sections such as “3.1 left 45° prompt / 3.2 right 45° prompt / 3.3 body prompt / 3.4 back prompt”. Those are internal implementation rules, not the normal user-facing deliverable.

### Mode B — Strict Face-Master Composite (EXPLICIT OPT-IN ONLY)
Expand the sub-prompts only when the user explicitly asks for terms such as:

- `严格无损 Master Face`
- `分区生成`
- `四个辅助区域分别生成`
- `最终拼版`
- `strict composite`

In Mode B, preserve the original Master Face pixels and generate the four auxiliary regions separately before compositing.

## Fixed Director Rules

- Output frame: 16:9 horizontal.
- One approved story segment = one single 16:9 pure-background reference image derived from that segment’s video-prompt content plus a separate written shot/beat plan; never use a grid or collage.
- One approved 15-second video-prompt content draft determines one matching pure-background reference image; after the image is confirmed, output the final MiniMax H3 prompt.
- **15-second capacity rule:** total dialogue must be **≤40 characters** and distinct visible actions must be **≤6**. Do not apply the old 11s/13s bands or a mandatory 2-second buffer.
- Standard background-reference + character-reference workflow uses Ref2VA unless the actual inputs require another H3 mode.
- The pure-background reference `<Picture 1>` is derived from the target video prompt and controls environment layout, spatial depth, overall composition, lighting, color, atmosphere, and environmental props. It contains no characters and does not define identity, blocking, action, dialogue, timing, or performance progression.
- Each important character gets exactly one V6.1 Face-Master reference image and one permanent `<Subject N>`.
- In multi-character scenes, Subject identity follows the person through movement and cuts; it never follows left/right screen position.
- Final H3 rewrite sections are English. Preserve dialogue, lyrics, and genuinely visible scene text in their original language.
- No subtitles, random text, watermarks, or logos unless explicitly required by the story.

## 15-Second Capacity / Coverage Rules

- Count all spoken dialogue, voiceover, and lyrics assigned to the 15-second segment. The total must be **no more than 40 characters**; punctuation and spaces do not count.
- Count each distinct, visible, must-complete action once. The total must be **no more than 6 actions**. A continuous action with one intent and one result may count as one; a new intent or separately readable result starts a new action.
- Camera movements, cuts, passive poses, and environment descriptions do not count as character actions unless they themselves are required narrative events.
- A segment passes when dialogue ≤40 characters and actions ≤6. Split only when either cap is exceeded or the planned physical sequence is plainly impossible in 15 seconds.
- Preserve original dialogue verbatim and assign every line/action to a written beat/shot. Do not slow story progression by applying the retired 2.2–2.6 characters/second estimate, 11s/13s bands, or mandatory 2-second buffer.
- Use a Dialogue and Action Count Audit before approving the shot plan and again before final H3 Prompt delivery.
- Written beats are planning aids, not image panels. Merge or cut shots according to narrative clarity; the number of beats/shots is not fixed.

## V6.1 Character Rule

The Master Face is the authoritative facial identity source. Left/right 45-degree views are rotational-geometry support only. Front/back body views are appearance support only and must not redefine facial identity. Makeup, hairstyle, age impression, skin tone, and stable styling must not drift.

## Multi-Character Binding Rule

For every visible character, maintain this permanent chain:

`character reference picture → permanent <Subject N> → shot-by-shot spatial state → optional stable speaker ID (Sx)`

Never cross these chains. At the start of every multi-character shot, explicitly bind each visible `<Subject N>` to name, frame position/depth, facing direction, and pose before describing the action. If characters exchange sides, show the crossing movement and keep the same Subject IDs.

## H3 Output Discipline

- Ref2VA field order: `subject_definitions`, `summary`, `retention_analysis`, `detailed_description`, `overall_soundscape`, `non_diegetic_music`.
- Base modes field order: `integrated_multimodal_description`, `overall_soundscape`, `non_diegetic_music`, with the official keyframe alignment line where required.
- `[Shot 1]` has no timestamp. From `[Shot 2]` onward use strictly increasing `At MM:SS.mmm` cut-in times.
- Speaker IDs `(S1)`, `(S2)` remain stable across shots and may be permanently paired with corresponding character Subjects.
- Original dialogue must remain verbatim inside `<d>[Language] ...</d>`.
