from PIL import Image, ImageOps
import json

ORIGINAL = "a4e64c3e-004d-482b-a80c-ecfaa907fae5.png"
COORDS = "skyteam_logo_assets/logo_coordinates.json"

def make_gray(original_path=ORIGINAL):
    img = Image.open(original_path).convert("RGB")
    return ImageOps.grayscale(img).convert("RGB")

def restore_logo(logo_id, original_path=ORIGINAL, coords_path=COORDS, output_path=None):
    original = Image.open(original_path).convert("RGB")
    result = ImageOps.grayscale(original).convert("RGB")
    with open(coords_path, "r", encoding="utf-8") as f:
        coords = json.load(f)
    item = next(c for c in coords if c["id"] == logo_id)
    x, y, w, h = item["x"], item["y"], item["width"], item["height"]
    result.paste(original.crop((x, y, x+w, y+h)), (x, y))
    if output_path:
        result.save(output_path)
    return result

# Example:
# restore_logo(5, output_path="restore_05_china_airlines.png")
