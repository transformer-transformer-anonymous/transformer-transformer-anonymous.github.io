# Transformer Transformer — Anonymous Project Page

Project page for **Transformer Transformer: A Unified Model for Motion-Conditioned Robot Co-design**, anonymous submission to CoRL 2026.

- Live page: `index.html` (open directly in a browser, or serve with `python3 -m http.server 8000`)
- Template: forked from [`umi-on-legs.github.io`](../umi-on-legs.github.io), stripped of identifying info
- Anonymity: no author block, no GitHub link, no analytics, no personal/lab references in the page chrome

---

## Repo layout

```
transformer-transformer-anonymous.github.io/
├── index.html                       ← the page
├── README.md                        ← this file (TODOs + tweet drafts)
└── static/
    ├── css/                         ← bulma + custom (index.css)
    ├── js/                          ← bulma carousel/slider + fontawesome
    ├── images/                      ← paper figures, already copied in
    │   ├── teaser.jpg               ← from t2-paper/figures/teaser_v6.jpg
    │   ├── tokenization.png         ← from t2-paper/figures/tokenization_v2e.png
    │   ├── robotokens-compactness.png  ← from t2-paper/figures/robotokens_v3.png
    │   ├── architecture.jpg         ← from t2-paper/figures/hardware_diffusion_v14.jpg
    │   ├── qualitative.jpg          ← from t2-paper/figures/qualitative_results_v4.jpg
    │   ├── hardware-opt.jpg         ← from t2-paper/figures/hardware_opt_results_v3.jpg
    │   ├── real-world.jpg           ← from t2-paper/figures/real_world_v1.jpg
    │   ├── real-world-velocity.jpg  ← from t2-paper/figures/real_world_velocity_v0.jpg
    │   ├── reward-prediction.jpg    ← from t2-paper/figures/reward_prediction_accuracy_v0.jpg
    │   └── quadruped-control.jpg    ← from t2-paper/figures/quadruped_control_performance_v0.jpg
    ├── videos/
    │   └── transformer-transformer-supp.mp4   ← 16-min technical summary (already in place)
    └── paper.pdf                    ← TODO: drop anonymous paper PDF here
```

Existing paper figures and the 16-min summary video are already in place — the only outstanding visual work is **6 new short clips** for the body of the page (see TODO #2) plus the anonymous paper PDF.

---

## TODO #1 — Drop the anonymous paper PDF

Path: `static/paper.pdf`

The "Paper" button in the page header links here. If the PDF lives elsewhere, change the `href` in the navbar (search `static/paper.pdf` in `index.html`, two occurrences).

---

## TODO #2 — Produce the 6 new video clips

(The 16-min technical summary video is self-hosted at `static/videos/transformer-transformer-supp.mp4` and already wired up in the page.)

All clips go under `static/videos/`. The 16-min source video lives at `~/t2-paper/transformer transformer supp.mp4` (note the spaces in the filename) — most of these can be cut from it.

The page already references each clip by exact path; once the file exists, the placeholder div disappears from view (the page logic doesn't conditionally hide the placeholder, so once you drop the files, also remove the corresponding `<div class="placeholder">…</div>` block in `index.html`).

| # | Path | Priority | Length | Source | What it shows |
|---|------|---------|--------|--------|---------------|
| 1 | `static/videos/teaser.mp4` | Nice-to-have | 8–12 s loop | New composite | Hero background. Composite: diffusion-of-robot → that robot tracking motion in sim → real ALOHA running. Auto-plays muted under the title. Falls back gracefully if missing (just black background). |
| 2 | `static/videos/embodiment-matters.mp4` | High | 3–5 s loop | Cut from supp video | Section "What is the best robot for a given manipulation task?" — a randomly-generated quadruped face-planting while attempting a toss. Drives "embodiment matters" viscerally. |
| 3 | `static/videos/cross-embodiment-quadruped.mp4` | High | 6–10 s loop | Cut from supp video | Architecture section, "An embodiment-aware controller". 2×2 grid of visibly different quadrupeds (different leg lengths, knee directions, DoF, spring-loaded vs serial) all tracking the same trajectory under the same policy. |
| 4 | `static/videos/diffusion-grid.mp4` | High | 3–5 s loop | New animation | Architecture section, "A generator over diverse robot classes". 2×3 grid: Gaussian noise → denoised robot, in 6 different robot classes (e.g., Allegro hand, UR5e, ANYmal, Cassie, humanoid, ALOHA). Communicates "this is a generative model for robots" instantly. |
| 5 | `static/videos/landscape-guidance.mp4` | Medium | 5–8 s loop | New animation | Self-guidance section. 2D slice of a reward landscape with diffusion samples as dots; with guidance, dots climb toward peaks. Makes the gradient-guidance idea visual. Already implicit in the supp video — this would be the skim-friendly still/loop version. |
| 6 | `static/videos/aloha-before-after.mp4` | **MUST-HAVE** | 10–12 s | Real-world rollouts | **The single highest-leverage asset.** Real-world ALOHA cloth-flinging, side-by-side: original design failing to track on left, optimized design unfolding the cloth on right. With on-screen labels "−73% tracking error" and "−30% max joint speed". Reused as the Tweet 1 GIF and as the hero clip of the real-world section. |

When you replace a placeholder, also delete its corresponding `<div class="placeholder">…</div>` block in `index.html` — they're not auto-hidden when the underlying media exists.

---

## TODO #4 — Tweet thread

Six tweets, result-first hook, drafted to fit ~280 chars. The first tweet's media is the single highest-leverage asset (video clip #6 above). No emojis in the drafts — add to taste.

### Tweet 1 — Hook (post first)
**Media:** Trimmed version of `static/videos/aloha-before-after.mp4` (6–8 sec loop, square or 4:5 for feed).
**Text:**
> One model redesigns robots for any manipulation task — and we built its design in the real world.
>
> 73% lower tracking error on cloth flinging with ALOHA. It made the arms longer and mounted them upside-down, for a more efficient underarm swing.
>
> How a diffusion transformer co-designs robots ↓

### Tweet 2 — The framing
**Media:** `static/images/teaser.jpg` (the "Demonstrate, Generate, Validate" teaser).
**Text:**
> Setup: given target end-effector motions and a reward function, generate the best complete robot for the task — link lengths, joints, motors, everything.
>
> We call this motion-conditioned robot co-design. Our solution: Transformer Transformer.

### Tweet 3 — RoboTokens
**Media:** Preferred: a short loop of 6–8 robots being tokenized + reconstructed (cuttable from supp video). Fallback: `static/images/robotokens-compactness.png`.
**Text:**
> Step 1: one tokenizer for any robot.
>
> RoboTokens encode every link, joint, motor, state, and action. Same vocabulary spans fixed arms, quadrupeds, dexterous hands, humanoids.
>
> Bonus: 27–110× more compact than raw MJCF/URDF — small enough to diffuse directly.

### Tweet 4 — One model, many hats
**Media:** `static/images/architecture.jpg` (the architecture diagram).
**Text:**
> Step 2: one diffusion transformer, different masking schemes.
>
> Mask the actions → cross-embodiment controller.
> Mask the embodiment → robot generator.
> Same weights. Trained jointly on dynamics.

### Tweet 5 — Dynamics Self-Guidance
**Media:** Preferred: `static/videos/landscape-guidance.mp4` (the gradient-climbing animation). Fallback: `static/images/qualitative.jpg`.
**Text:**
> Step 3: optimize rewards the model has never seen.
>
> At inference, we turn the model's own dynamics predictions into pseudo-rewards. The gradient of that reward steers diffusion toward higher-value designs.
>
> No reward function appeared during training. The model zero-shots new ones.

### Tweet 6 — Real-world payoff + links
**Media:** Longer cut of `static/videos/aloha-before-after.mp4` (10–15 sec, with the -73% and -30% titles on screen).
**Text:**
> And it transfers to hardware.
>
> Fabricated optimized ALOHA: 73% lower tracking error, 30% lower max joint speed on dynamic cloth flinging.
>
> Paper: [link]
> Project page (with 16-min talk): [link]

---

## Anonymity checklist (verify before release)

- [ ] No author names anywhere in `index.html` (currently clean)
- [ ] No GitHub repo link (currently absent)
- [ ] No analytics tag — no `gtag.js`, no `_ga` IDs (currently absent)
- [ ] Footer does not reference a specific lab or person (currently generic)
- [ ] `static/paper.pdf` is the anonymized version (no metadata in the PDF either — check `pdfinfo paper.pdf`)
- [ ] Self-hosted video has no identifying metadata (`exiftool transformer-transformer-supp.mp4` to check)
- [ ] Domain is `transformer-transformer-anonymous.github.io` (the repo owner *is* a deanonymizing signal — host under an anonymous GH account or behind a CoRL-provided reviewer URL)

---

## Sanity checks

- Open `index.html` in a browser. The page should render with paper figures inline and dashed placeholder boxes where videos will go.
- Click any inline citation `[N]` — should scroll to and highlight the corresponding entry in the References section.
- Tab through the hero nav links — each should jump to the right section.
- Phone-width: resize to mobile width; the hero typography should shrink, and the layout should remain single-column.

---

## Where each blog section came from

If you need to edit the prose, the source material is:
- Section openers: adapted from `~/t2-paper/video_script.md` (matches the casual voice)
- Captions: rewritten from the paper figure captions in `~/t2-paper/text/v7.tex` to be self-contained for skim-readers
- Numbers (73%, 30%, 27–110×, etc.): pulled from the paper main text and `~/t2-paper/text/supp.tex` tables
