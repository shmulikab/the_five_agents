---
name: nano-banana-2
description: >
  Use this skill to generate or edit images using Google Nano Banana 2
  (Gemini 3.1 Flash Image Preview via MCP). Invoke when the user asks to
  create, generate, illustrate, or edit any image or visual. This skill
  sends a prompt to the model and returns the generated image.
---

# Nano Banana 2 — Image Generation Skill

Google Nano Banana 2 (`gemini-3.1-flash-image-preview`) is Google's fast, high-quality image generation model. It is available in this project via MCP server (`nano-banana-2-mcp`).

---

## Prerequisites

The MCP server must be running. It is configured in `.claude/settings.json`:

```json
{
  "mcpServers": {
    "nano-banana-2": {
      "command": "npx",
      "args": ["-y", "nano-banana-2-mcp"],
      "env": { "GEMINI_API_KEY": "${GEMINI_API_KEY}" }
    }
  }
}
```

The user must have `GEMINI_API_KEY` set as an environment variable (obtain from [Google AI Studio](https://aistudio.google.com/apikey)).

---

## Available MCP Tools

### `generate_image`

Generates a new image from a text prompt.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `prompt` | string | ✓ | Detailed description of the image to generate |
| `aspect_ratio` | string | — | `"1:1"` (default), `"16:9"`, `"9:16"`, `"4:3"`, `"3:4"` |
| `resolution` | string | — | `"standard"` (default), `"hd"`, `"4k"` |
| `num_images` | integer | — | 1–4 (default: 1) |
| `negative_prompt` | string | — | Elements to avoid in the image |

**Response:** Image data (URL or base64). Save to file using Write tool.

### `edit_image`

Edits an existing image based on a prompt.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `image_path` | string | ✓ | Path to the source image file |
| `prompt` | string | ✓ | Description of the desired edit |
| `mask_path` | string | — | Path to mask file (white = edit, black = keep) |
| `strength` | float | — | Edit strength 0.0–1.0 (default: 0.75) |

---

## How to Use This Skill

### Generating a new image

```
1. Compose a detailed, descriptive prompt:
   - Subject + action
   - Style (photorealistic, illustration, watercolor, vector...)
   - Lighting, mood, color palette
   - Composition (close-up, wide angle, bird's-eye...)
   - Negative prompt for unwanted elements

2. Call: generate_image(prompt=..., aspect_ratio=..., resolution=...)

3. Save the result:
   - Write the returned image data to a file
   - Use a descriptive filename: outputs/<subject>-<date>.png
```

### Editing an existing image

```
1. Identify the source image path
2. Describe the edit precisely
3. Call: edit_image(image_path=..., prompt=...)
4. Save result to outputs/
```

---

## Prompt Writing Guide

**Good prompt structure:**
```
[Style] [Subject] [Action/Pose] [Setting] [Lighting] [Color palette] [Details]
```

**Example:**
```
Flat vector illustration, a friendly orange cat sitting on a wooden desk,
warm afternoon light through a window, muted pastel colors with terracotta accents,
minimalist style, clean lines, no background clutter
```

**Tips:**
- Be specific about art style — "illustration" is vague; "flat vector illustration" is precise
- Mention color palette explicitly to maintain visual consistency
- Use negative_prompt to exclude unwanted elements: `"blurry, low quality, text, watermark"`
- For character consistency, describe distinctive features in every prompt

---

## Saving Images

Always save generated images to `outputs/` with a meaningful filename:

```
outputs/hero-banner-2026-04-27.png
outputs/product-shot-blue-variant.png
outputs/logo-concept-v2.png
```

Never overwrite existing outputs — use versioned filenames.

---

## Error Handling

| Error | Likely cause | Action |
|-------|-------------|--------|
| MCP connection failed | GEMINI_API_KEY not set or npx not available | Ask user to set API key and ensure Node.js is installed |
| Content policy violation | Prompt contains restricted content | Rewrite prompt, remove problematic elements |
| Rate limit | Too many requests | Wait 30 seconds, retry |
| Invalid aspect_ratio | Unsupported value | Use one of the supported ratios listed above |
