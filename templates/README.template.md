# {System Name}

![{System Name}](assets/banner.svg)

{One or two sentences: the question this system answers, and the honest one-line
answer including the headline metric.}

Part of [awesome-ml-systems](https://github.com/MagicLex/awesome-ml-systems), an
FTI system on [Hopsworks](https://www.hopsworks.ai/).

## The result

{What was trained, on what data, balanced how. State the metric on a holdout,
not just cross-validation.}

| metric | value |
|---|---:|
| ROC-AUC (CV) | 0.00 |
| ROC-AUC (holdout) | 0.00 |

## Caveats

Read these before quoting the number anywhere.

- **The label is a proxy.** {What "positive" actually means and how it can be wrong.}
- **Selection.** {How the sample was drawn and what bias that bakes in.}
- **{Model} only.** {What the model does not see, and why that is on purpose.}

## Architecture

An FTI (feature, training, inference) system on Hopsworks.

```mermaid
{paste templates/diagram.mmd, rename the nodes}
```

The file-by-file map:

```
ingest.py            source -> data/...                         (terminal, I/O bound)
feature_pipeline.py  data -> feature group                      (Hopsworks job)
train.py             feature view -> model -> registry          (Hopsworks job)
deploy.py            model -> endpoint                           (model serving)
app/app.py           input -> calls endpoint                    (Hopsworks app)
features.py          shared feature extraction (no skew)
```

## Reproduce

Clone into a Hopsworks project on the `/hopsfs/...` FUSE mount.

```bash
make features      # load the feature group        (Hopsworks job)
make train         # model -> registry             (Hopsworks job)
make serve         # deploy the model              (model serving)
make deploy-app    # deploy the app
```

## The demo

{One line on what the served app does.}

![the app](assets/demo.jpg)
