import cairo

def text_to_image(text, image_path, font_size=12, font_color=(0, 0, 0), bg_color=(1, 1, 1), width=400, height=200):
    surface = cairo.ImageSurface(cairo.FORMAT_ARGB32, width, height)
    ctx = cairo.Context(surface)
    
    # Set background color
    ctx.set_source_rgb(*bg_color)
    ctx.rectangle(0, 0, width, height)
    ctx.fill()
    
    # Set font properties
    ctx.select_font_face("Arial", cairo.FONT_SLANT_NORMAL, cairo.FONT_WEIGHT_NORMAL)
    ctx.set_font_size(font_size)
    
    # Get text dimensions
    text_extents = ctx.text_extents(text)
    text_width = text_extents[4]
    text_height = text_extents[3]
    
    # Calculate text position to center it in the image
    text_x = (width - text_width) / 2
    text_y = (height + text_height) / 2
    
    # Set font color
    ctx.set_source_rgb(*font_color)
    
    # Draw text
    ctx.move_to(text_x, text_y)
    ctx.show_text(text)
    
    # Save image
    surface.write_to_png(image_path)

# Prompt user for input
text = input("Enter the text to be drawn on the image: ")
font_size = int(input("Enter the font size: "))
font_color = tuple(map(int, input("Enter the font color as RGB values (comma-separated): ").split(',')))
bg_color = tuple(map(int, input("Enter the background color as RGB values (comma-separated): ").split(',')))
image_path = input("Enter the image path (e.g., output.png): ")

# Call text_to_image function with user input
text_to_image(text, image_path, font_size, font_color, bg_color, width=600, height=300)
