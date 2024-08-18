---
title: 'Real life CS:GO flashbang'
date: 2022-03-13T09:12:17-04:00
draft: true
tags: ["Projects"]
hideToc: true
---


A while ago [this](https://www.youtube.com/watch?v=D75ZuaSR8nQ) Michael Reeves video came out demoing a creative project in which he shot himself based on what was happening in the Fortnite game he was playing. This gave a barrage of new ideas for the hacker house.

This was the perfect skill set to recreate a [funny video](https://www.youtube.com/watch?v=ybaK3y_6YXg) that I had seen online, with a bit of a kick.

### Meet the Team

###### Paxton "Demoman" Marchifava
Specialty: Hardware

###### Malcolm "The Engineer" Boyes
Specialty: Ideas

###### Jarvis "Support" Coghlin
Specialty: Programming


### Meet the Hardware
LEDs are pretty good at their job these days. Ten 100-watt cells off of Aliexpress did the job. 

<!-- {{< figure src="/images/flashbang-leds.jpg" title="LEDs in a row" width="400">}} -->
{{< figure src="/images/flashbang-leds.jpg" >}}

Power was obtained from an off-the-shelf 24V PSU, and the setup could be controlled with a 5V relay and Arduino Nano.


### Meet the Software

Very simple. If multiple points on the screen are detected to be brighter than a certain threshold, fire away!
The Python code for this looks something like this:

{{< highlight py "linenos=inline" >}}
def is_white(r,g,b):
    cutoff_brightness = 245
    if r > cutoff_brightness and g > cutoff_brightness and b > cutoff_brightness:
        return 1
    return 0

def check_pixels_for_flash(img):
    pixels_to_check = [(30, 30),
                       (200, 200),
                       (150, 150), ]
    for pixel in pixels_to_check:
        pixel_colors = img.getpixel(pixel)
        if not is_white(pixel_colors[0], pixel_colors[1], pixel_colors[2]):
            return 0
    print("All pixels were white...FLASH ME")
    return 1

if __name__ == "__main__":
    while True:
        img = pyautogui.screenshot(region=(0,0,300,300))
        if check_pixels_for_flash(img):
            comms.turn_on_lights()
            print("Flashed")
            time.sleep(2)
        time.sleep(0.01)
{{< / highlight >}}

The `is_white()` function can be adjusted for fine-tuning, but during testing we had no issues with a value of ~245.


### Final Setup

Once the code is uploaded to the Arduino and everything is plugged in, this is the result: 

{{< youtube J_J6DgB_2rw >}}.
  
Thanks for reading! You can check out the project [here](https://github.com/jarviscog/enhanced-flashbang)
