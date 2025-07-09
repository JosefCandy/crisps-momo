from PIL import Image, ImageDraw, ImageFont

# Image Configuration
image_size = (892, 331)
background_color = (255, 255, 255)  # White
text = "Crisps MoMo"

# Create a new blank image
img = Image.new("RGB", image_size, background_color)
draw = ImageDraw.Draw(img)

# Load font or fallback to default
try:
    font = ImageFont.truetype("DejaVuSans-Bold.ttf", 70)
except IOError:
    font = ImageFont.load_default()

# Calculate text position to center it
text_bbox = draw.textbbox((0, 0), text, font=font)
text_width = text_bbox[2] - text_bbox[0]
text_height = text_bbox[3] - text_bbox[1]
position = ((image_size[0] - text_width) // 2, (image_size[1] - text_height) // 2)

# Draw "Crisps" in orange, "MoMo" in dark gray
highlight_text = "Crisps"
highlight_width = draw.textlength(highlight_text, font=font)
draw.text(position, highlight_text, fill=(255, 102, 0), font=font)
draw.text((position[0] + highlight_width, position[1]), " MoMo", fill=(51, 51, 51), font=font)

# Save the image
img.save("crisps-momo.png")
print("✅ Image saved as 'crisps-momo.png'")
