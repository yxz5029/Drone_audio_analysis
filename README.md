# Drone_audio_analysis
> Non-confidential technical overview of Clover, an end-to-end drone pre-flight health diagnosis system developed in a private team repository.
This repository is a non-confidential project summary. The original implementation, trained models, and operational datasets remain in a private team repository.
# Clover: Blackbox + Audio Analysis

This repo now contains two main pipelines and a fusion step:

- blackbox/: Cleanflight/Betaflight log parsing and CSV export
- audio/: Microphone capture and audio fault inference (inference only)
- fusion/: Combine blackbox + audio results and produce a global Go/No Go

## Layout

- blackbox/data/input, blackbox/data/output
- audio/data/input, audio/data/output
- fusion/data/input, fusion/data/output

## Readmes

- Blackbox pipeline: [blackbox/README.md](blackbox/README.md)
- Audio pipeline: [audio/README.md](audio/README.md)
- Fusion pipeline: [fusion/README.md](fusion/README.md)

## Quick Start

TODO

### Blackbox

```bash
source clover_env/bin/activate
python blackbox/scripts/clover_pipeline.py -i path/to/log.bbl --validate
```

### Audio Inference

1) Copy your trained model checkpoint into audio/models/best_model.pt
2) Record or infer:

```bash
source clover_env/bin/activate
python audio/inference/cli.py record --duration 5 --output audio/data/input/recorded.wav
python audio/inference/cli.py infer --audio audio/data/input/recorded.wav --output audio/data/output/recorded.json
```

### Fusion (Go/No Go)

```bash
python fusion/combine_results.py \
  --blackbox-result blackbox/data/output/<set>/results/blackbox_result.json \
  --audio-result audio/data/output/recorded.json \
  --output fusion/data/output/combined.json
```

See the section readmes above for detailed setup and usage.
