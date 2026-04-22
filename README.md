# content-engine

AI content generation pipeline. Manages persona design, image generation, LoRA training, and content posting across platforms.

## Machine Layout

| Machine | Role |
|---|---|
| SAP M2 Mac | Claude CLI, scripting, job design, prompt engineering |
| M1 MacBook Pro 16GB | ComfyUI local image generation, script execution |
| UniCluster | LoRA training, large batch image generation |
| Google Drive | All generated images, videos, model weights |

## Repo Structure

```
/characters    # Persona sheets, LoRA training configs per character
/prompts       # Prompt libraries for image gen, captions, DMs
/scripts       # ComfyUI scripts, automation, posting pipelines
/jobs          # UniCluster SLURM job files
/content       # Generated content metadata, caption drafts
/course        # Meta account content, course outline
```

## Setup

1. Clone repo on each machine
2. `cp .env.example .env` and fill in API keys
3. See `/scripts/setup.md` for ComfyUI install instructions

## Workflow

1. Design character + prompts on SAP Mac (Claude CLI)
2. Push to GitHub
3. Pull on M1, run ComfyUI image generation
4. Generated images auto-sync to Google Drive
5. For LoRA training: push job config, pull on UniCluster, submit SLURM job
6. Trained weights saved to Google Drive
