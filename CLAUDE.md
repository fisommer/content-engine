# content-engine — Claude Project Context

## What this project is
AI content generation pipeline for building and managing AI influencer personas across Instagram and TikTok. Two parallel tracks:
- **Track 1:** AI girl influencer accounts (image-based, monetized via OnlyFans/Fanvue)
- **Track 2:** Meta/journey account documenting the process (future course)

## Machine layout
| Machine | Role |
|---|---|
| SAP M2 Mac (this machine) | Claude CLI, scripting, prompt engineering, job design |
| M1 MacBook Pro 16GB | ComfyUI local image generation, script execution |
| UniCluster | LoRA training, large batch image generation |
| Google Drive | All generated images, videos, model weights |

## Repo structure
- `/characters` — persona sheets, LoRA training configs per character
- `/prompts` — prompt libraries for image gen, captions, DMs
- `/scripts` — ComfyUI scripts, automation, posting pipelines
- `/jobs` — UniCluster SLURM job files
- `/content` — generated content metadata, caption drafts
- `/course` — meta account content, course outline

## Google Drive structure
```
content-engine/
├── characters/
│   └── character-01/
│       ├── training-images/
│       ├── lora-weights/
│       └── generated/
├── videos/
├── captions/
└── course/
```

## Tech stack
| Tool | Purpose |
|---|---|
| ComfyUI + Flux schnell | Local image generation on M1 |
| fal.ai | High-quality single images |
| Replicate | LoRA training (one-time per character) |
| Kling AI | Image-to-video |
| CapCut | Video editing |
| ElevenLabs | Voice (optional) |
| Buffer/Later | Scheduling |

## Current status
- Repo scaffolded, Google Drive structure created
- Next: ComfyUI install on M1, first character sheet, first test image

## Personas (TBD)
Character types not yet decided — options: sporty / soft aesthetic / edgy urban
