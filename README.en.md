# Promo Creator Skills

English · [中文](README.md)

> A production-grade skill pack for turning real products into credible launch films: product judgment, narrative structure, visual planning, HyperFrames editing, BGM direction, and delivery notes.

Most AI-generated promo videos fail for the same reason: they start with visuals before they understand the product. They decorate instead of deciding. They turn a repo, a SaaS page, or a new feature into generic motion graphics.

Promo Creator Skills takes the opposite route. It treats a promo film as a sequence of production decisions: what the product is, why it matters, what the viewer must understand first, which real assets prove it, how each shot moves, and what kind of music actually supports the cut. The result is not a magic button. It is a disciplined agent workflow for making product videos that feel specific, inspectable, and worth shipping.

Use it when the goal is not "make something flashy", but "make the product legible, credible, and worth a second look in 60-90 seconds."

```bash
npx skills add kangarooking/promo-creator-skills
```

If your skill runner does not support `npx skills add`, copy the `promo-*` folders into your agent skills directory.

---

## Demo Gallery

### WorkBuddy OPC · Commercial Product Launch

Modern product-launch BGM direction: beat, bass, hook, and CTA momentum. Useful when the video should feel like a launch film rather than background UI music.

[Watch MP4](demos/workbuddy-commercial-launch.mp4)

<video src="demos/workbuddy-commercial-launch.mp4" controls width="100%"></video>

### WorkBuddy OPC · Clean UI Demo Groove

Software-demo BGM direction: cleaner rhythm, UI-card timing, workflow motion, and enough energy to carry real interface shots.

[Watch MP4](demos/workbuddy-ui-groove.mp4)

<video src="demos/workbuddy-ui-groove.mp4" controls width="100%"></video>

### Cangjie Skill · Open Source Project Promo

A 90-second Swiss International-style promo for an open-source meta-skill that compiles books into callable Agent Skills. The point is not louder claims; it is making a valuable method visible: book knowledge becomes triggers, steps, boundaries, and tests an agent can actually use.

[Watch MP4](demos/cangjie-skill-promo.mp4)

<video src="demos/cangjie-skill-promo.mp4" controls width="100%"></video>

---

## What It Does

This pack is built around one principle: **a good product video is a compressed product argument**. The visuals are there to carry that argument, not to hide the absence of one.

| Skill | Job | Output |
|---|---|---|
| `promo-brief` | Research the product and choose the narrative direction | `01-brief.md` |
| `promo-storyboard` | Write shot-by-shot visual and motion specs | `02-storyboard.md` |
| `promo-asset-producer` | Plan and gather generated assets plus real product material | `03-asset-plan.md`, `assets/` |
| `promo-editor` | Build the HyperFrames edit and render the MP4 | `04-edl.md`, `master-edit.html`, `final/promo.mp4` |
| `promo-music-maker` | Design BGM prompts, hit points, and product-promo music lanes | `06-music-plan.md`, `assets/bgm/` |
| `promo-workflow` | Orchestrate the whole staged pipeline | delivery-ready run folder |

The workflow is deliberately staged. A good promo is not a one-shot prompt; it is a chain of decisions:

```text
Product / repo / URL
  -> brief
  -> storyboard
  -> asset plan
  -> edit decision list
  -> HyperFrames master edit
  -> BGM direction and candidates
  -> final MP4
  -> delivery notes
```

Each stage leaves an artifact behind, so you can challenge the reasoning before paying the cost of rendering, regenerating assets, or burning music credits.

---

## Why This Is Different

- **It starts with product strategy**: the brief decides audience, positioning, narrative shape, and proof points before any frame is designed.
- **It designs shots, not vibes**: the storyboard specifies frame composition, typography, timing, motion, and asset needs.
- **It prefers real product evidence**: screenshots, docs, GitHub data, and interface details carry more weight than decorative AI imagery.
- **It treats BGM as part of editing**: music prompts include genre, rhythm, bass, hook, energy curve, and hit points instead of vague "premium tech" language.
- **It keeps the work inspectable**: every phase produces Markdown or source files that can be reviewed, corrected, and reused.

---

## BGM That Does Not Collapse Into Generic AI Ambience

The music skill includes a hard-won product-promo rule: visual minimalism is not the same as ambient music.

For software product videos, the default pair is now:

- **Commercial Product Launch**: 118 BPM, tight electronic drums, sidechained synth bass, bright plucked synth hook.
- **Clean UI Demo Groove**: 112 BPM, syncopated digital percussion, rubbery synth bass, short glass-pluck motif.

This avoids the common failure mode where every option becomes `minimal / ambient / soft pulse / glass ticks` and sounds interchangeable.

Mureka generation is supported through `scripts/mureka.py`:

```bash
export MUREKA_API_KEY="..."
export MUREKA_API_URL="https://api.mureka.cn" # optional, for the China endpoint

python scripts/mureka.py instrumental \
  --prompt "<validated product-promo BGM prompt>" \
  -n 2 \
  --format mp3 \
  --output outputs/promo-runs/<run-id>/assets/bgm/
```

---

## Usage

Ask your agent:

```text
Use promo-workflow to make a 60-second Apple-style product promo for this GitHub repo:
https://github.com/owner/project
```

Or:

```text
Use the promo skills to create a launch video for my SaaS. Pause after the brief and storyboard.
```

For existing footage or screenshots:

```text
Use promo-editor and promo-music-maker. I already have the storyboard and assets.
```

---

## Repository Structure

```text
promo-creator-skills/
├── promo-brief/              # product research and creative brief
├── promo-storyboard/         # shot-by-shot visual specs
├── promo-asset-producer/     # generated and sourced asset planning
├── promo-editor/             # HyperFrames edit and render workflow
├── promo-music-maker/        # product-promo BGM prompt and Mureka workflow
├── promo-workflow/           # orchestration skill
├── references/
│   ├── mureka_prompt_guide.md
│   └── product_promo_bgm_prompting.md
├── scripts/
│   └── mureka.py
└── demos/
    ├── workbuddy-commercial-launch.mp4
    ├── workbuddy-ui-groove.mp4
    └── cangjie-skill-promo.mp4
```

`SKILL.md` at the repository root is a lightweight entrypoint for installers that expect a root skill file; the detailed workflow still lives in the `promo-*` folders.

---

## Requirements

- Node.js 22+
- HyperFrames CLI for HTML-to-video work
- FFmpeg available on `PATH`
- Python 3.10+
- `requests` for Mureka API calls
- Optional: `MUREKA_API_KEY` for BGM generation

The skills can still design BGM prompts without an API key; they only call Mureka when explicitly asked to generate audio.

---

## Design Principles

- **Intermediate files over black boxes**: every major decision lands in Markdown before render.
- **Real product signal first**: UI screenshots, docs, GitHub data, and brand assets beat decorative filler.
- **Storyboard before assets**: image generation without a shot plan is expensive randomness.
- **Music has a job**: product videos need rhythm, hook, bass movement, and section contrast.
- **Pause points are part of quality**: good agent workflows invite correction before the expensive step.

---

## Limitations

- This is a skill pack, not a hosted video editor.
- Final visual quality depends on available product assets and the agent's render environment.
- Mureka output can vary; generate 2-3 candidates and pick by watching the video, not by listening in isolation.
- Large local production runs are ignored by git; curated public examples live in `demos/`.

---

## License

MIT.
