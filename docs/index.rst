:notoc:

***********************
MoviePy documentation
***********************

.. image:: /_static/medias/logo.png
    :width: 50%
    :align: center

**Date**: |today| from moviepy.editor import TextClip, ImageClip, concatenate_videoclips, CompositeVideoClip
import os

# Video settings
W, H = 1920, 1080           # Video dimensions
duration_per_scene = 7.5     # Duration (in seconds) for each scene to total 30 seconds

# Scene 1: Title Screen
title_text = "Navigating the Depths of Success"
title_clip = TextClip(title_text, fontsize=80, color='white', size=(W, H),
                       method='caption', align='center').set_duration(duration_per_scene)

# Scene 2: Ocean and Whale Imagery
if os.path.exists("whale.jpg"):
    whale_clip = ImageClip("whale.jpg").resize((W, H)).set_duration(duration_per_scene)
else:
    whale_text = "A majestic whale glides through the vast ocean..."
    whale_clip = TextClip(whale_text, fontsize=50, color='white', size=(W, H),
                          method='caption', align='center').set_duration(duration_per_scene)

# Scene 3: Impact on Businesses and People
impact_text = ("We transform businesses and empower people.\n"
               "Our innovative solutions drive growth and inspire success.")
impact_clip = TextClip(impact_text, fontsize=60, color='white', size=(W, H),
                       method='caption', align='center').set_duration(duration_per_scene)

# Scene 4: Branding with Tagline
branding_text = "Whale Developers"
branding_clip = TextClip(branding_text, fontsize=80, color='yellow', size=(W, H),
                         method='caption', align='center').set_duration(duration_per_scene)

# Create a tagline text clip
tagline_text = "Riding Waves of Innovation"
tagline_clip = TextClip(tagline_text, fontsize=40, color='lightblue', method='caption')\
               .set_duration(duration_per_scene)

# Overlay the tagline onto the branding clip using CompositeVideoClip
# Position the tagline at the bottom center.
branding_composite = CompositeVideoClip([
    branding_clip,
    tagline_clip.set_position(("center", "bottom"))
], size=(W, H)).set_duration(duration_per_scene)

# Concatenate all scenes into the final 30-second video
final_video = concatenate_videoclips([title_clip, whale_clip, impact_clip, branding_composite], method="compose")

# Output the video file
final_video.write_videofile("whale_developers_video.mp4", fps=24)
