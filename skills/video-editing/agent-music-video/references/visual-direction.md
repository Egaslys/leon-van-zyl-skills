# Phase 4 — Visual direction & storyboard

Decide the look, the cast and the recurring devices BEFORE anyone builds a frame. Directors working in
parallel only produce one coherent film if these are pinned down in `STORYBOARD.md`.

## 1. The look — match the song, not the last project
The kit's default skin is **BlockFrame neobrutalism** (pastel grounds, thick black borders, hard offset
shadows, Inter 900 uppercase, sticker type). It suited a comedic funk-pop song. For other genres, re-theme:

| Song feel | Look ideas | Theme moves |
|---|---|---|
| comedic pop / funk / novelty | neobrutalist stickers (default), zine, toy packaging | default kit |
| synthwave / electronic | neon on night grounds, grids, chrome type | `--k-ink` → near-white glow, dark grounds, a mono or wide display font |
| lo-fi / chill | paper textures, muted palette, slow pans, handwritten labels | softer palette, thinner borders, slower camera, phrase-flow pacing |
| rock / punk | photocopy grain, ransom-note type, red/black/yellow | high contrast, rough textures, more shake |
| corporate / launch | clean product UI, one brand colour, calm motion | brand palette in theme.css; keep characters but tone down gags |

Browse `<skills>/hyperframes-creative/frame-presets/` for ready palettes + font pairings (read only the
preset's colours and fonts). Theme via `assets/theme.css` (CSS vars) + `assets/theme.js` (`KIT.theme({...})`
for SVG characters). **Fonts must be royalty-free** (OFL/Apache/MIT — see `assets/fonts/FONTS.md`).
Keep one accent colour reserved for alarms/censor/crash moments so it keeps its meaning.

## 2. The cast
- **The host — AGENT** (`KIT.mascot`): a boxy robot with an LED screen face (14 expressions), lip-sync, poses,
  grooves, sweat/tears, a chest badge (any short text — "A.I.", a team name, a version number) and
  accessories (beret, shades, headset, crown, party hat) or whole scene outfits (`KIT.outfit`, §6). Variants via `body`/`ear`/`eye` colours and
  `badge` make cousins and sidekicks (in the reference: HAIKU 5.5 = green + shades; COUSIN 4.5 = blue + headset).
  Use it as narrator whenever the song has a narrator voice; it is the reusable identity across videos.
- **The female AGENT** (`KIT.mascot({ id })` + `KIT.femme(id)`, which recolours her pink itself: pink shirt and ears, pink antenna bow,
  lashes, blush, same rig and expressions). **Casting rule (the user's): whoever sings a line on screen matches the voice.** Run
  `scripts/voice_cast.py` in phase 3; lines marked `voice:"f"` are sung by her, `"m"` by AGENT, `"duet"` by both. Never have AGENT
  lip-sync a female voice (the user caught this in Track 02's intro). Give her real moments, not a cameo, when she sings.
- **Brand mascot cameos** — real mascots of the companies in the story, rendered with affection and kept
  on-model (proportions matter: the user noticed when Clawd came out too wide). The kit ships **Clawd**
  (Claude Code's orange voxel critter, 3D, `K3.clawd`) — the user's favourite element; give him real dance
  moments, not edge-of-frame cameos. Build others the same way (simple primitives + toon + outline).
- **Gag characters** born from the lyrics (the reference's LE CHONK — Mistral's 1T "big boy" with beret,
  mustache, sash and bulb horn — `KIT.chonk`). Invent new ones per song; keep them simple SVG or 3D.

## 3. Recurring devices (the film's grammar)
- **Receipts**: the real screenshot in a browser window, tilted, with a highlighter sweeping the exact phrase
  on the sung word, plus a source pill (the outlet's name only). Use for every factual claim — it makes the jokes land as true.
- **Standalone rule (the user's):** every video stands on its own. No episode/track numbers, no video-title labels, no
  release or publish dates on screen (title card, pills, receipt tags, end card) unless the story needs them (a date the
  lyric sings, the days of a week the song is structured around). Dates live in research.md and the description.
- **A structural card** that orders the story (tear-off calendar per day, chapter cards, a scoreboard…).
- **The hook's visual gag** (e.g. A.I. → censor bar → yellow "S" sticker) that repeats and evolves each chorus.
- **Ground/colour flips on downbeats**, star bursts, dot grids — cheap, on-beat life.
- **Story-state continuity** (write these as explicit rules): e.g. "after 66.5 s the host's badge reads S.I. in every frame".

## 4. The chorus arc (lesson from three critic rounds)
Design the chorus grammar ONCE (word slams on the sung words, the hook gag, the shout) and then **re-stage it
each time**: chorus 1 = reference; chorus 2 = same timing inside new set pieces (a memo, a chat thread, a
Find & Replace dialog…); final chorus = its own look (e.g. a night stage with 3D letters and spotlights)
and clearly the biggest moment. Identical repeats were the critic's #1 complaint.
Same for the opening: the first 10–20 s must hook (a composed first frame, the host doing something, a
gag on the first spoken line), and the outro should bookend the intro.

## 5. Energy & the 2D+3D combo (match the gold standard)
The gold standard is **"Don't Say A.I."** (critic 8.8/10): `C:\sandbox\music videos\videos\2026-10-11-dont-say-ai` — study its
frames (`compositions/frames/`) and watch `renders/final/Dont-Say-AI_1080p60_YouTube.mp4` before storyboarding. It used 3D in
10 of 17 frames (≈ 16 `K3` calls/min) and ≈ 36 camera-div references/min (measured as grep counts over `compositions/frames/*.html` per minute of song: `K3.(text3d|clawd|box|cyl|sphere|coin)` calls, and references to a frame's camera div `"#…cam"`; Track 02 v2 measured 4/16 frames, ≈ 2.5 calls/min, ≈ 13 camera refs/min). Track 02 v2 was judged against it and "missing the energy,
and combo of 2D with 3D". Targets for every video:
- A real 3D hero moment in **≥ 60% of frames** and in **every chorus** (3D hook slabs / toon lettering), 3D Clawd in chorus
  instrumentals and breakdowns.
- 3D props layered WITH the 2D world (stickers, receipts, characters in front of and behind them), not 3D in a separate box.
- A camera move on every phrase (push-in, whip-pan, dolly, orbit on 3D), punches/shakes on hits, ground/colour flips on downbeats.
- No static hold > 0.6 s (except a deliberate musical stop).
Plan the 3D moment and the camera move per line in the storyboard, then count them before rendering.

**Cut density (measure it on a render with ffmpeg scene detection, cuts per minute per section).** The gold standard: 27/min
overall, choruses 48–59/min, breakdown 84/min, and energy PEAKS in the breakdown + final chorus. Track 02 v2 measured 17.6 overall,
choruses 22/15/29 and a breakdown of 10/min (its flattest section): the arc ran backwards and scored 6.6. Targets: hooks ≥ 45 cuts/min
with one composition per sung hook word, every hook word full-frame with a colour flip; the breakdown is the densest section (each
call-back gets its own full-frame 3D payoff); the final chorus brings the whole cast back. Characters 25–40% of frame height in
featured shots; never repeat the same cutaway angle more than twice.

## 6. Outfits per scene
Characters may change outfits to match the scene (`KIT.outfit` / `KIT.outfitSwap`, see `kit-api.md`): pit crew at a pit stop,
shades at a neon night show, reading glasses for a lecture, a crown for a victory lap. Rules: change outfits at scene/section cuts or
with an on-beat swap (`KIT.outfitSwap`); an outfit stays the same for the whole scene (write it in the storyboard's continuity
rules); identity markers never change: AGENT = blue body + yellow tilted MoE badge; her = pink body + antenna bow + MoE badge.

## 7. STORYBOARD.md
Use music-to-video's storyboard format (frontmatter + `## Frame N — NN-id` blocks with `src`, `duration`,
`span_sec`, `pacing`, `mood`, `feel`, `### Groups`) so `validate-plan.mjs` and `assemble-index.mjs` work.
In each group write WHAT, not HOW: the lyric anchors (track seconds), the copy, the receipt (shot name,
crop, mark rects from `rects.json`), and a one-paragraph story beat. Mark the planned thumbnail beats (≥ 1 per section: a big face + one bold word, held a few frames —
see delivery.md › Thumbnails). Add the cast list, recurring devices,
continuity rules, caption policy (which sections have the karaoke bar) and an owner per frame.
Example: `assets/examples/STORYBOARD-dont-say-ai.md`.
