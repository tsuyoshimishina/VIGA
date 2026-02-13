<h1 align="center">VIGA: Vision-as-Inverse-Graphics Agent via Interleaved Multimodal Reasoning</h1>

<p align="center">
    <a href="https://fugtemypt123.github.io/VIGA-website/"><img src="https://img.shields.io/badge/Page-Project-blue" alt="Project Page"></a>
    <a href="https://arxiv.org/abs/2601.11109"><img src="https://img.shields.io/badge/Paper-arXiv-b31b1b" alt="arXiv Paper"></a>
    <a href="https://huggingface.co/datasets/DietCoke4671/blenderbench"><img src="https://img.shields.io/badge/Benchmark-HuggingFace-yellow" alt="HuggingFace Benchmark"></a>
    <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green" alt="License"></a>
</p>

<p align="center"><img src="docs/images/art_cropped.png" width="33%"><img src="docs/images/render.gif" width="33%"><img src="docs/images/dynamic.gif" width="33%"></p>

<p align="center">
    <a href="#about">About</a> •
    <a href="#supported-domains">Supported Domains</a> •
    <a href="#quickstart">Quickstart</a> •
    <a href="#documentation">Documentation</a> •
    <a href="#citation">Citation</a>
</p>

<br>

# About

VIGA is an analysis-by-synthesis code agent for programmatic visual reconstruction. It approaches vision-as-inverse-graphics through an iterative loop of generating, rendering, and verifying scenes against target images.

A single self-reflective agent alternates between two roles:

- **Generator** — Writes and executes scene programs using tools for planning, code execution, asset retrieval, and scene queries.

- **Verifier** — Examines rendered output from multiple viewpoints, identifies visual discrepancies, and provides feedback for the next iteration.

The agent maintains an evolving contextual memory with plans, code diffs, and render history. This write-run-compare-revise loop is self-correcting and requires no finetuning.

<p align="center">
    <img src="docs/images/trajectory.png" alt="VIGA Trajectory" width="100%">
</p>

<br>

# Supported Domains

| Mode | Description | Output |
|------|-------------|--------|
| [BlenderGym](https://github.com/richard-guyunqi/BlenderGym-Open) | Single-step 3D graphics editing | Blender Python |
| [BlenderBench](https://huggingface.co/datasets/DietCoke4671/blenderbench) | Multi-step 3D graphics editing (Level 1-3) | Blender Python |
| [SlideBench](https://github.com/para-lost/AutoPresent) | 2D slide/document layout synthesis | PowerPoint |
| Custom Static Scene | Single-view 3D reconstruction | Blender scene |
| Custom Dynamic Scene | 4D dynamic scene with physics | Blender animation |

<br>

# Quickstart

## 1. Installation: Setup the environment

### Prerequisites

You need [Conda](https://docs.conda.io/en/latest/miniconda.html) installed. For 3D modes, an NVIDIA GPU with CUDA support is recommended.

### Clone repository

```bash
git clone https://github.com/Fugtemypt123/VIGA-release.git && cd VIGA-release
git submodule update --init --recursive
```

### Set up conda environments

VIGA requires separate conda environments for the agent and tools. The setup script creates all of them automatically:

```bash
./setup.sh
```

This creates 5 conda environments (all prefixed with `viga-`):

| Environment | Python | Purpose |
|---|---|---|
| `viga-agent` | 3.10 | Main agent runtime |
| `viga-blender` | 3.11 | Blender/Infinigen tools |
| `viga-sam3d-objects` | 3.11 | SAM-3D with CUDA extensions |
| `viga-sam` | 3.10 | Segment Anything (SAM) |
| `viga-sam3` | 3.11 | SAM 3 |

The script also generates `utils/_path.py` (environment path mappings) and downloads required model checkpoints.

To set up only specific environments:

```bash
./setup.sh agent blender        # only these two
```

To verify all environments are working:

```bash
./setup.sh --check
```

See [Requirements](requirements/README.md) for additional options.

### Configure API keys

Set API keys as environment variables:

```bash
export OPENAI_API_KEY=sk-...
export CLAUDE_API_KEY=sk-ant-...
```

## 2. Usage: Run the agent

```bash
conda activate viga-agent
python runners/dynamic_scene.py --task=artist --model=gpt-5
```

Custom data: place in `data/dynamic_scene/<your-data-name>` following the format in `data/dynamic_scene/artist`.

<br>

# Documentation

| Doc | Description |
|-----|-------------|
| [Architecture](docs/architecture.md) | System design and agent tools |
| [Requirements](requirements/README.md) | Conda environment setup |
| [Runners](runners/README.md) | Batch execution options |

<br>

# Citation

You can find a paper writeup of the framework on [arXiv](https://arxiv.org/abs/2601.11109).

If you find this project useful for your research, please consider citing:

```bibtex
@misc{yin2026visionasinversegraphicsagentinterleavedmultimodal,
      title={Vision-as-Inverse-Graphics Agent via Interleaved Multimodal Reasoning},
      author={Shaofeng Yin and Jiaxin Ge and Zora Zhiruo Wang and Xiuyu Li and Michael J. Black and Trevor Darrell and Angjoo Kanazawa and Haiwen Feng},
      year={2026},
      eprint={2601.11109},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2601.11109},
}
```
