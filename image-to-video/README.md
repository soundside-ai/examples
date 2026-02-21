# Image to Video

Generate an image with Grok, then animate it with Veo.

```python
import requests

BASE = "https://mcp.soundside.ai/mcp"
HEADERS = {"Authorization": "Bearer YOUR_API_KEY"}

# Step 1: Generate image
img = requests.post(f"{BASE}/create_image", headers=HEADERS, json={
    "provider": "grok",
    "prompt": "A serene mountain lake at golden hour",
    "project_id": "YOUR_PROJECT_ID"
}).json()

image_id = img["resource_id"]
print(f"Image: {image_id}")

# Step 2: Animate with Veo
vid = requests.post(f"{BASE}/create_video", headers=HEADERS, json={
    "provider": "vertex",
    "prompt": "The lake shimmers gently in the breeze, birds fly overhead",
    "first_frame": image_id,
    "project_id": "YOUR_PROJECT_ID"
}).json()

print(f"Video: {vid['resource_id']} (status: {vid['state']})")
# Poll lib_list until status == "completed"
```
