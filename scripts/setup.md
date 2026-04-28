# ComfyUI Setup — M1 MacBook Pro

ComfyUI is the local image generation interface that runs Flux models on your M1. This machine handles day-to-day generation; heavy batch work goes to UniCluster.

## Prerequisites

- Python 3.10+ (via Homebrew or pyenv)
- Git
- ~20GB free disk space for models

## 1. Install ComfyUI

```bash
git clone https://github.com/comfyanonymous/ComfyUI
cd ComfyUI
pip install -r requirements.txt
```

## 2. Install Flux Schnell model weights

Flux schnell is the fast variant of the Flux model — good quality, much faster than Flux dev, suitable for iteration and batch generation.

```bash
cd ComfyUI/models/checkpoints
# Download from HuggingFace (requires HF account)
huggingface-cli download black-forest-labs/FLUX.1-schnell flux1-schnell.safetensors --local-dir .
```

You'll also need the VAE and text encoders:

```bash
cd ComfyUI/models/vae
huggingface-cli download black-forest-labs/FLUX.1-schnell ae.safetensors --local-dir .

cd ComfyUI/models/text_encoders
huggingface-cli download comfyanonymous/flux_text_encoders clip_l.safetensors t5xxl_fp8_e4m3fn.safetensors --local-dir .
```

## 3. Install custom nodes

Custom nodes extend ComfyUI with extra functionality. Install via ComfyUI Manager (recommended) or manually.

**Install ComfyUI Manager first:**

```bash
cd ComfyUI/custom_nodes
git clone https://github.com/ltdrdata/ComfyUI-Manager
```

Restart ComfyUI, then use the Manager UI to install any additional nodes.

**Recommended nodes for this project:**
- `ComfyUI-Impact-Pack` — face detailing, refinement
- `ComfyUI_IPAdapter_plus` — style/character consistency without LoRA
- `ComfyUI-Advanced-ControlNet` — pose/composition control

## 4. Load a LoRA

Once you have trained LoRA weights (from Replicate, stored in Google Drive), drop them into:

```
ComfyUI/models/loras/
```

In the ComfyUI workflow, add a **Load LoRA** node between the model loader and the sampler. Set strength between `0.7–1.0` — higher = more character, lower = more prompt flexibility.

## 5. Run ComfyUI

```bash
cd ComfyUI
python main.py --force-fp16
```

Open `http://127.0.0.1:8188` in your browser. The `--force-fp16` flag is important on M1 — it reduces memory usage significantly.

## 6. Google Drive sync

Generated images should sync automatically if you have Google Drive for Desktop installed and the output folder pointed at your Drive location.

Set your output path in ComfyUI:  
**Settings → Output directory** → point to your local Google Drive folder:

```
~/Library/CloudStorage/GoogleDrive-<your-email>/My Drive/content-engine/characters/character-01/generated/
```

## Workflow files

ComfyUI workflows are saved as `.json` files. Store project workflows in `/scripts/workflows/` in this repo so they're version-controlled and available on all machines.

## Troubleshooting

**Out of memory errors** — lower batch size to 1, enable `--force-fp16`, close other apps.  
**Model not found** — check file is in the correct `models/` subfolder and restart ComfyUI.  
**Slow generation** — Flux schnell should do ~30–60s per image on M1 16GB. If slower, check Activity Monitor for memory pressure.
