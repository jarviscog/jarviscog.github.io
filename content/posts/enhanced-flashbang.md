---
title: 'Real life CS:GO flashbang'
date: 2022-03-13T09:12:17-04:00
draft: false
tags: ["Projects", "Hardware"]
hideToc: true
---


A while ago [this](https://www.youtube.com/watch?v=D75ZuaSR8nQ) Michael Reeves video came out demoing a creative project in which he shot himself based on what was happening in the Fortnite game he was playing. This gave a barrage of new ideas for the hacker house.

Lucky for us, we had the perfect skill set to recreate a [funny video](https://www.youtube.com/watch?v=ybaK3y_6YXg) that we had seen online. Essentially, a real life flashbang that didn't just blind you in your game of CS:GO, but outside as well.

### Meet the Team

###### Paxton "Demoman" Marchifava
*Specialty: Hardware*

###### Malcolm "The Engineer" Boyes
*Specialty: Embedded Devices*

###### Jarvis "Support" Coghlin
*Specialty: Programming*


### Meet the Hardware
LEDs are pretty good at their job these days. Ten 100-watt cells from Aliexpress did the job.

{{< figure src="/images/flashbang-leds.jpg" >}}

Power was obtained from an off-the-shelf 24V PSU, and the setup could be controlled with a 5V relay and Arduino Nano.
{{< figure src="/images/flashbang-electronics.jpg" >}}


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

The `is_white()` function can be adjusted for fine-tuning, however during testing we had no issues with a value of ~245.


### Final Setup

Once the code is uploaded to the Arduino and everything is plugged in, this is the result: 

{{< youtube J_J6DgB_2rw >}}.
  
Thanks for reading! This turned out to be a relatively simple, but very fun project. 
You can check out the project [here](https://github.com/jarviscog/enhanced-flashbang) and create your own.
