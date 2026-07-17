# awesome-ml-systems

![awesome-ml-systems](assets/banner.svg)

[![systems](https://img.shields.io/badge/systems-12-34d399?labelColor=0b0e11&style=flat)](#the-series)
[![Hopsworks](https://img.shields.io/badge/built_on-Hopsworks-1CB182?labelColor=0b0e11&style=flat)](https://www.hopsworks.ai/)

One small, honest ML system per day, each built end to end on
[Hopsworks](https://www.hopsworks.ai/). Same shape every time: an FTI (feature,
training, inference) pipeline, a real result with its caveats, and a served
model you can poke at. No notebooks-that-never-ship, no accuracy without a
holdout, no demo wired to a mock.

## The series

| # | system | the question | result | published | repo |
|---|---|---|---|---|---|
| 001 | README Vaporware Score | does a repo get abandoned, from its README text alone? | ROC-AUC 0.76 | 2026-06-29 | [readme-vaporware-score](https://github.com/MagicLex/readme-vaporware-score) |
| 002 | Asteroid Doomsday-o-meter | how big is an asteroid (so, how dangerous), from its Gaia spectrum alone? | size error ×1.13 vs ×1.34 blind | 2026-06-30 | [asteroid-size-from-light](https://github.com/MagicLex/asteroid-size-from-light) |
| 003 | Phishing at Issuance | is a freshly issued TLS certificate phishing, from its hostname alone? | ROC-AUC 0.78 holdout vs 0.50 blind | 2026-07-01 | [phish-at-issuance](https://github.com/MagicLex/phish-at-issuance) |
| 004 | Where on Earth | which country was a photo taken in, from its pixels alone? | top-1 52.3% / top-5 79.8% over 173 countries vs 21.2% zero-shot | 2026-07-02 | [where-on-earth](https://github.com/MagicLex/where-on-earth) |
| 005 | How Predictable. | can a machine learn your taste in 30 clicks, live, in front of you? | crowd prior 0.719 pairwise vs 0.511 zero-shot; per-user Bayesian layer climbs on-screen | 2026-07-03 | [how-predictable](https://github.com/MagicLex/how-predictable) |
| 006 | Live Sky Watch | where will every aircraft over Europe be in 60/180/300 s, and which one is not behaving like traffic here? | live same-sample: model 964 m vs physics 1427 m at 60 s where it intervenes; jamming grid + learned normalcy | 2026-07-06 | [live-sky-watch](https://github.com/MagicLex/live-sky-watch) |
| 007 | Ghost Fleet | which vessels behave like the sanctioned shadow fleet, from their AIS tracks alone? | 9.4x lift over a blind sanctions-list lookup, ROC-AUC 0.92 (population split); live network reveal | 2026-07-07 | [ghost-fleet](https://github.com/MagicLex/ghost-fleet) |
| 008 | the untested | which never-tested plant might fight a drug-resistant infection, from molecular structure alone? | mean AMR ROC-AUC 0.80, beats 1-NN Tanimoto on every scored head; recovers *Artemisia* for malaria from structure alone | 2026-07-08 | [the-untested](https://github.com/MagicLex/the-untested) |
| 009 | downwind | what is in the air where nobody is measuring? | PM2.5 20.9% RMSE under the raw CAMS prior at leave-stations-out stations (r2 0.61 vs 0.38); live all-Europe field with a monitored-vs-predicted frontier | 2026-07-09 | [downwind](https://github.com/MagicLex/downwind) |
| 010 | LLM Tell Auditor | does academic prose read like an LLM wrote it, from style alone? | ROC-AUC 0.986 held out by paper vs 0.50 blind (within-provider label); evidence per passage, signal not verdict | 2026-07-13 | [llm-tell-auditor](https://github.com/MagicLex/llm-tell-auditor) |
| 011 | empty-chair | which UK companies' ownership disclosure is shaped like known concealment, from the disclosure alone? | PR-AUC 0.199, 4.2x lift, precision@100 0.42, sector-blind; the 0.377 sector-aware version was retired by its own bias audit (top 1% was 99.3% real estate); signal not verdict | 2026-07-14 | [empty-chair](https://github.com/MagicLex/empty-chair) |
| 012 | unstarred | which repos would you have starred already, if you had seen them? | recall@100 10.45% on 144k future stars over 362k repos; shuffled-label control lands at 6.65% (the corpus-popularity floor), trending at 0.28%; personalization = 2.1x MRR over the floor | 2026-07-15 | [unstarred](https://github.com/MagicLex/unstarred) |

## The dog house

Honest exceptions. The series test is a decision someone can act on. These
builds are clean FTI systems and nice to look at, but the use case does not hold
up to that test, so they sit here, unnumbered, kept public because the
engineering is real.

| system | the question | why it is here | repo |
|---|---|---|---|
| dead-air | can you hear a solar flare black out the shortwave bands before the bulletin? | beautiful instrument, no decision attached: a few-minute lead measured against a bulletin nobody waits on (and negative on the holdout), and it misses roughly four flares in five. You cannot act on the ionosphere anyway. Real code, wrong problem. | [dead-air](https://github.com/MagicLex/dead-air) |
| cited or buried | will the AI answer quote your page, or just rank it? | the data tells a real story: 40% of AI citations go to a page that was not in the top-3 search results, and rank correlates with citation only -0.36. But that gap belongs to the answer engine, not to the model. Over raw search rank the model adds almost nothing: pointwise AUROC 0.746 vs 0.721, precision@3 +0.003 (rank already saturates the top). So the coach cannot tell you much beyond where you already rank. Clean corpus, honest finding, no lift to act on. | [cited-or-buried](https://github.com/MagicLex/cited-or-buried) |

## The standard

Every repo in the series follows the same mould, so they read as siblings.

**Shape.** An FTI system on Hopsworks. Sources to a feature pipeline to a
Feature Group, a Feature View to training to the Model Registry, a deployment to
an endpoint, an app that calls it. The skeleton lives in
[`templates/diagram.mmd`](templates/diagram.mmd).

**Banner.** Generated, not hand-drawn, so 30 of them stay consistent. Dark
canvas, emerald accent, the Hopsworks hop-mark as the fixed brand, only
title/tagline/emoji/index change per repo.

```bash
python tools/make_banner.py \
  --title "My System" \
  --tagline "What it predicts, in one honest sentence." \
  --emoji "🧪" --index 002 --out assets/banner.svg
```

**README.** Result first (with the metric and the holdout), then caveats, then
architecture (the diagram plus a file-by-file map), then reproduce, then the
served demo. Start from [`templates/README.template.md`](templates/README.template.md).

**Honesty rules.** The label is named and its proxy is stated. There is a
holdout number, not just cross-validation. No feature leaks the label. Heavy
fits run as Hopsworks jobs, not in a terminal. Feature extraction is one shared
function so training and serving cannot skew.

## New entry

```bash
mkdir ../my-new-system && cd ../my-new-system
cp -r ../awesome-ml-systems/tools .                       # the banner generator
cp ../awesome-ml-systems/templates/README.template.md README.md
python tools/make_banner.py --title "..." --tagline "..." --index NNN
# fill the README, paste templates/diagram.mmd, then add a row to the table above
```
