---
title: "GPS Gift Box"
description: A box that only opens at the GPS coordinates you set. Perfect for gifting, adventures, and wild goose chases.
---

Jan 2019


{{< rawhtml >}}
    <div class="flex flex-wrap justify-center pv4">
    <div class="imgdiv"><img src="img/gps-gift-box/gps_thumbnail_downsized.png" class="ph3 pv2 square"></div>
    <div class="imgdiv"><img src="img/gps-gift-box/open_lid.JPG" class="ph3 pv2 square rotate90"></div>
    </div>
{{< /rawhtml >}}


## Inception

This is an old project that I decided to re-master from way, way back - this was one of my first projects when I had just started tinkering with electronics.

The original idea comes from geocaching - the object of which is to travel to a set of GPS coordinates and attempt to find a hidden cache (treasure). This flips the idea on its head, where you have the goodies right from the start in a locked box that you take with you, which unlocks at a specific location. In this case, it's called reverse geocaching.

## Execution

I made a box with a built in screen which prompts you to go outside. Once it acquires a GPS fix, it displays (in km) how far away you are from your destination. The distance updates once every couple of seconds, so you can figure out in which direction to move - once you arrive at your destination, the box then unlocks.

{{< rawhtml >}}
    <div class="flex flex-wrap justify-center pv4">
    <div class="imgdiv"><img src="img/gps-gift-box/gps_guts.JPG" class="ph3 pv2 square"></div>
    <div class="imgdiv"><img src="img/gps-gift-box/lid_guts.JPG" class="ph3 pv2 square rotate90"></div>
    </div>
{{< /rawhtml >}}

The big components are two Arduinos, [an Adafruit GPS module with antenna](https://www.adafruit.com/product/746), a 16x2 LCD display, a servo to serve as a crude lock, a 5V power bank, and of course, the box itself. You might be cringing - why two Arduinos? One controls the servo, the other talks to the GPS module - the Servo library and Adafruit's GPS library don't play nice, because of some bug where software serial (needed for communicating with the GPS module) interferes with a timer needed for PWM (I forget the exact reason).

On one Arduino, you hard-code the GPS coordinates, run your GPS distance code, & output to the LCD. It talks to the other Arduino over hardware UART serial, whose sole job is to actuate the servo. Really dumb, I know. There's also a little IR sensor on the top of the lid for shining an IR LED onto to unlock the box. Turned out to be useful for test & debug.

## Improvements

For a next iteration, I would integrate everything save for the battery pack & locking actuator onto a single PCB, which would screw into the lid (screen and all). One microcontroller should be plenty - if I still decided to use a servo, I would probably have a dedicated chip over SPI/I2C for putting out the necessary PWM signal. And still, a servo isn't the wisest choice for keeping things locked, because any change to the PWM during power-down will change the servo's position - not great. It was convenient for keeping everything on a single 5V, USB-chargeable power source, though. In the future I will likely make a much more robust locking mechanism with a linear actuator like [this one](https://www.progressiveautomations.com/products/micro-linear-actuator?variant=18277344673859). It seems almost drag and drop.

{{< rawhtml >}}
    <div class="flex flex-wrap justify-center pv4">
    <div class="imgdiv"><img src="img/gps-gift-box/charging_cable.JPG" class="ph3 pv2 square rotate90"></div>
    <div class="imgdiv"><img src="img/gps-gift-box/screen.JPG" class="ph3 pv2 square rotate90"></div>
    </div>
{{< /rawhtml >}}

## Conclusion

I used this to surprise my girlfriend with her New Year's gift. I set the destination for the place where we had first met. Watching the remaining distance go down built anticipation, and we still enjoy the memory of opening her gift together :)

I'd like to make a more bulletproof iteration of this to use more regularly for wild goose chases and gifting.
