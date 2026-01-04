---
name: gemini-imagegen
description: Generate and edit images using Google's Gemini API. Use when creating images from text prompts, editing existing images, or generating visual content. Requires GEMINI_API_KEY environment variable.
---

# Gemini Image Generation

Generate and edit images using Google's Gemini API.

## Prerequisites

Set the `GEMINI_API_KEY` environment variable:

```bash
export GEMINI_API_KEY="your-api-key"
```

## Default Configuration

| Setting | Default |
|---------|---------|
| Model | `gemini-2.0-flash-exp` |
| Resolution | 1K |
| Aspect Ratio | 1:1 |
| Format | JPEG |

## Basic Generation

```python
import os
from google import genai
from google.genai import types

client = genai.Client(api_key=os.environ["GEMINI_API_KEY"])

response = client.models.generate_content(
    model="gemini-2.0-flash-exp",
    contents=["A serene mountain lake at sunset"],
    config=types.GenerateContentConfig(
        response_modalities=['TEXT', 'IMAGE'],
    ),
)

for part in response.parts:
    if part.text:
        print(part.text)
    elif part.inline_data:
        image = part.as_image()
        image.save("output.jpg")  # Always use .jpg
```

## Critical: File Format

**Gemini returns JPEG format by default—always use `.jpg` extension** to prevent media type errors.

## Aspect Ratios

Supported ratios:
- `1:1` - Square (default)
- `16:9` - Widescreen
- `9:16` - Portrait/mobile
- `4:3` - Standard
- `3:4` - Portrait standard
- `3:2` - Photo
- `2:3` - Portrait photo

## Image Editing

Pass existing images with text prompts:

```python
from PIL import Image

# Load existing image
existing_image = Image.open("input.jpg")

response = client.models.generate_content(
    model="gemini-2.0-flash-exp",
    contents=[
        "Remove the background and replace with a beach sunset",
        existing_image
    ],
    config=types.GenerateContentConfig(
        response_modalities=['TEXT', 'IMAGE'],
    ),
)
```

## Multi-Turn Refinement

Use chat for iterative editing:

```python
chat = client.chats.create(model="gemini-2.0-flash-exp")

# Initial generation
response = chat.send_message("Create a logo for a coffee shop")
# Save first version...

# Refine
response = chat.send_message("Make the colors warmer and add steam")
# Save refined version...
```

## Prompting Best Practices

### For Photorealism
Include camera settings:
```
"Portrait photo, Canon EOS R5, 85mm f/1.4, natural lighting,
shallow depth of field, golden hour"
```

### For Stylized Art
Specify art style:
```
"Watercolor painting of a Paris café, loose brushstrokes,
soft colors, impressionist style"
```

### For Text in Images
Include font specifications:
```
"Minimalist poster with 'HELLO' in bold Helvetica,
centered, white text on deep blue background"
```

### For Product Shots
Specify lighting setup:
```
"Product photo of a watch, studio lighting,
soft shadows, white background, high contrast"
```

## Error Handling

```python
try:
    response = client.models.generate_content(...)

    if not response.parts:
        print("No image generated")
        return

    for part in response.parts:
        if part.inline_data:
            image = part.as_image()
            image.save("output.jpg")

except Exception as e:
    print(f"Generation failed: {e}")
```

## Limitations

- Maximum ~14 reference images
- Some content restrictions apply
- Rate limits based on API tier
- JPEG output format only
