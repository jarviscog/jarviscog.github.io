---
title: 'internal-demos'
date: 1084-12-17T09:37:36-04:00
draft: true
---

# Code block

Some `python` code
{{< highlight py "linenos=inline,hl_lines=8 15-17,linenostart=199" >}}
from pprint import pprint
# ... code
def go_to(content: str):
    print(content)
{{< / highlight >}}


# Embed
{{< figure src="/images/flashbang-leds.jpg" title="LEDs in a row" width="400">}}

# Table

| Col 1 | Col 2 | Col 3 |
|------:|-------|-------|
| Hello | Hello2|Hello3 |

# Youtube video
{{< youtube J_J6DgB_2rw >}}.

# Side by side

`# TODO`

# Audio
{{<audio src="audio/dance-song.mp3" caption="Test audio">}}

# 3D Models

{{< model-viewer 
    src="/models/bearing6.gltf" 
    alt="My model" 
    autoRotate="true" 
    cameraControls="true" 
    width="100%" 
    height="500px" 
>}}






