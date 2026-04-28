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
2. Set up your environment variables:
   - Run `cp .env.example .env` — this creates a local `.env` file from the template
   - `.env` holds your real API keys (Replicate, fal.ai, etc.) and is **never committed to git** (it's in `.gitignore`) to keep credentials private
   - Open `.env` and fill in each value — see comments in the file for what each key is for
   - `.env.example` stays in the repo as a reference so anyone setting up the project knows which variables are needed
3. See `/scripts/setup.md` for ComfyUI install instructions (M1 MacBook Pro)

## Workflow

1. Design character + prompts on SAP Mac (Claude CLI)
2. Push to GitHub
3. Pull on M1, run ComfyUI image generation
4. Generated images auto-sync to Google Drive
5. For LoRA training: push job config, pull on UniCluster, submit SLURM job
6. Trained weights saved to Google Drive
