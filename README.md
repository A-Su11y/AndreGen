# ComfyUI Vast.ai Quick Setup

## How to use

### Option A: Provisioning Script (recommended)

1. **Upload `provision.sh` to a GitHub Gist** (or your own repo)
   - Go to https://gist.github.com
   - Paste the contents of `provision.sh`
   - Click "Create secret gist" (or public, up to you)
   - Click "Raw" and copy that URL

2. **Upload your workflows** to the same gist or a GitHub repo
   - Create a repo like `github.com/yourname/comfyui-config`
   - Put the workflow JSONs in there
   - Set `WORKFLOW_REPO` to the raw URL base

3. **Create a Vast.ai template** using the ComfyUI base image:
   - Image: Use whatever ComfyUI image you're currently using
   - Environment Variables:
     ```
     PROVISIONING_SCRIPT=https://gist.githubusercontent.com/YOU/GIST_ID/raw/provision.sh
     HF_TOKEN=hf_YourTokenHere
     CIVITAI_TOKEN=YourCivitAITokenHere
     WORKFLOW_REPO=https://raw.githubusercontent.com/YOU/comfyui-config/main/workflows
     ```
   - Ports: Make sure 8090 is included (for FileBrowser)

4. **Launch an instance** with your template — provisioning runs automatically on first boot.

### Option B: Run manually on an existing instance

```bash
# Upload provision.sh to your instance, then:
bash /workspace/provision.sh
```

### Downloading large models (>8GB)

By default, models over 8GB are skipped. To download them:

```bash
DOWNLOAD_LARGE=true bash /workspace/provision.sh
```

Or download them one at a time through the Jupyter terminal.

## What gets installed

### Custom Nodes
All nodes required by your 5 workflows, plus ComfyUI Manager.

### Models (auto-downloaded, ≤8GB)
| Model | Folder | Size |
|-------|--------|------|
| 4x_foolhardy_Remacri.pth | upscale_models | 64MB |
| sam_vit_b_01ec64.pth | sams | 358MB |
| hand_yolov9c.pt | ultralytics/bbox | 50MB |
| face_yolov9c.pt | ultralytics/bbox | 50MB |
| Eyeful_v2-Paired.pt | ultralytics/bbox | 22MB |
| yolo11m-seg.pt | ultralytics/segm | 44MB |
| ntd11_anime_nsfw_segm_v5-variant1.pt | ultralytics/segm | 20MB |
| unwantedV10x.pt | ultralytics/segm | 138MB |
| sdxl_vae.safetensors | vae/SDXL | 320MB |
| wan_2.1_vae.safetensors | vae | 243MB |
| control-lora-canny-rank256.safetensors | controlnet/SDXL | 739MB |
| control-lora-depth-rank256.safetensors | controlnet/SDXL | 739MB |
| noobaiXLControlnet_openposeModel.safetensors | controlnet | 2.3GB |
| noobaiInpainting_v10.safetensors | controlnet | 286MB |
| OpenPoseXL2.safetensors | controlnet/SDXL | 4.7GB |
| ip-adapter-plus_sdxl_vit-h.safetensors | ipadapter | 809MB |
| ip-adapter-faceid-plusv2_sdxl.bin | ipadapter | 1.4GB |
| CLIP-ViT-H-14-laion2B-s32B-b79K.safetensors | clip_vision | 3.7GB |
| clip_vision_g.safetensors | clip_vision | 3.5GB |
| clip_vision_h.safetensors | clip_vision | 1.2GB |
| umt5_xxl_fp8_e4m3fn_scaled.safetensors | text_encoders | 6.3GB |
| Lightspeed LoRAs (high + low) | loras | ~1.2GB |
| MMAudio models (4 files) | mmaudio | ~4GB |

### Models (manual download, >8GB)
| Model | Folder | Size |
|-------|--------|------|
| fabricatedXL_v70.safetensors | checkpoints | ~6.5GB |
| waiIllustriousSDXL_v160.safetensors | checkpoints | ~6.5GB |
| Wan 2.2 I2V high/low noise (safetensors or GGUF) | unet | ~14GB each |

### FileBrowser
Installed on port 8090, added to Instance Portal.

## Workflows included
- **Advanced_V29.json** — Full T2I with IP-Adapter, OpenPose, Refiner
- **Basic_V29.json** — Streamlined T2I
- **Detailer_V29.json** — Image improvement/detailing
- **DaSiWa_UseThisForVideosV2.json** — Video generation (I2V/S2V)
- **Smooth_Workflow_-_Digital_Pastel_-_I2V.json** — I2V with MMAudio
