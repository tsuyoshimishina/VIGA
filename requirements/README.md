# Requirements

Conda environment setup for VIGA.

## Quick Start

The setup script creates all required conda environments (prefixed with `viga-`), generates `utils/_path.py`, and downloads model checkpoints:

```bash
./setup.sh              # all environments
./setup.sh agent blender  # specific environments only
./setup.sh --check      # verify installations
```

For SlideBench mode, create the pptx environment manually:

```bash
conda create -n viga-pptx python=3.10 -y && conda activate viga-pptx
pip install -r requirements/requirement_pptx.txt
```

## Requirement Files

| File | Environment | Python | Modes |
|------|-------------|--------|-------|
| `requirement_agent.txt` | viga-agent | 3.10 | All (main runtime) |
| `requirement_blender.txt` | viga-blender | 3.11 | 3D modes |
| `requirement_sam3d-objects.txt` | viga-sam3d-objects | 3.11 | SAM-3D with CUDA extensions |
| `requirement_sam.txt` | viga-sam | 3.10 | Segment Anything (SAM) |
| `requirement_sam3.txt` | viga-sam3 | 3.11 | SAM 3 |
| `requirement_pptx.txt` | viga-pptx | 3.10 | SlideBench |
| `requirement_eval-blender.txt` | eval-blender | 3.11 | 3D evaluation |
| `requirement_eval-pptx.txt` | eval-pptx | 3.10 | Slides evaluation |

## External Dependencies

### Blender (for 3D modes)

Blender is installed automatically by `./setup.sh` as part of the `viga-blender` environment. For manual installation:

```bash
cd utils/third_party/infinigen
conda activate viga-blender
INFINIGEN_MINIMAL_INSTALL=True bash scripts/install/interactive_blender.sh
```

### LibreOffice (for SlideBench)

```bash
sudo apt-get install -y libreoffice unoconv
```

## Configuration

### API keys

Set API keys as environment variables:

```bash
export OPENAI_API_KEY=sk-...
export CLAUDE_API_KEY=sk-ant-...
export MESHY_API_KEY=...
```

### `_path.py`

`setup.sh` generates `utils/_path.py` automatically. To regenerate, delete the file and re-run `setup.sh`.

You can override the conda base path with the `VIGA_CONDA_BASE` environment variable.

## Verification

```bash
./setup.sh --check              # all environments
./setup.sh --check agent sam3   # specific environments only
```

## Troubleshooting

| Problem | Solution |
|---------|----------|
| ModuleNotFoundError | Ensure correct conda env is activated |
| Infinigen install fails | Check Python 3.11, install `build-essential cmake` |
| CUDA not found | Run `nvidia-smi`, reinstall PyTorch with correct CUDA |
| PPTX conversion fails | Reinstall LibreOffice |
| Wrong Python path | Update `_path.py` with `which python` output |

## Reference to Original Repositories

If you encounter installation issues, please refer to the original repositories:

- **Blender environment**: [BlenderGym](https://blendergym.github.io/) | [GitHub](https://github.com/para-lost/AutoPresent)
- **PPTX environment**: [AutoPresent](https://github.com/para-lost/AutoPresent)
- **SAM (Segment Anything Model)**: [Meta AI SAM](https://segment-anything.com/) | [GitHub](https://github.com/facebookresearch/segment-anything) | [SAM 2](https://ai.meta.com/sam2/)
- **vLLM**: [vLLM Official Site](https://vllm.ai/) | [GitHub](https://github.com/vllm-project/vllm)
