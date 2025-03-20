import qrcode
import numpy as np
from PIL import Image, ImageDraw

# Instagram profile URL
instagram_username = "your_username"
instagram_url = f"https://www.instagram.com/{instagram_username}/"

# Create QR code
qr = qrcode.QRCode(
    version=5,  # Bigger version for better quality
    error_correction=qrcode.constants.ERROR_CORRECT_H,
    box_size=10,
    border=4,
)
qr.add_data(instagram_url)
qr.make(fit=True)

# Convert QR code to an image
qr_image = qr.make_image(fill="black", back_color="white").convert("RGBA")

# Get QR code size
qr_width, qr_height = qr_image.size

# Create a gradient background with Instagram colors
gradient = Image.new("RGBA", (qr_width, qr_height), (255, 255, 255, 255))
draw = ImageDraw.Draw(gradient)

# Define Instagram gradient colors
colors = [
    (255, 195, 0),   # Yellow
    (255, 87, 34),   # Orange
    (233, 30, 99),   # Pink
    (156, 39, 176),  # Purple
    (63, 81, 181)    # Blue
]

# Apply gradient effect
for y in range(qr_height):
    r, g, b = [
        int(colors[0][i] * (1 - y/qr_height) + colors[-1][i] * (y/qr_height))
        for i in range(3)
    ]
    draw.line([(0, y), (qr_width, y)], fill=(r, g, b), width=1)

# Combine QR code with gradient using transparency
qr_array = np.array(qr_image)
gradient_array = np.array(gradient)

# Make the black areas of the QR code transparent
for y in range(qr_height):
    for x in range(qr_width):
        if qr_array[y, x, 0] < 128:  # If it's a black pixel
            gradient_array[y, x] = (0, 0, 0, 255)  # Keep it black
        else:
            gradient_array[y, x, 3] = 0  # Make white pixels transparent

# Convert back to an image and save
final_qr = Image.fromarray(gradient_array)
final_qr.save("instagram_qr_colored.png")

print("QR code with Instagram colors generated and saved as 'instagram_qr_colored.png'.")
