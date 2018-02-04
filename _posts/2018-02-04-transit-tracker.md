---
layout: post
title: "Transit Tracker: Hardware"
date: 2018-02-04
comments: true
---
Ever since moving near a light rail station I've been looking for a way to visualize the trains' movement across the cities. When I first planted myself in the Twin Cities I was using the light rail almost every day and became accustom to its peculiarities, how it always seemed like there were more trains bound for where I wasn't going than where I was, how you'd get long unexpected waits followed by two trains a few minutes apart. I wanted to gain a birds-eye view to get some real context into what was going on across the whole system.

My first attempt was both incredibly simple and stupidly complex. I wrote a command line script that scraped [NexTrip](https://www.metrotransit.org/nextrip) for arrival times at all of the stops on the Green line and "triangulated" the locations of trains based on the differing times between them. It took these trains and plotted them as ascii art slowly moving across a previously abandoned monitor that I'd picked out of a recycling bin. While a bit kludgey it ended up serving in my living room as a conversation piece for a good year.

_It was only a couple weeks after completing the project that I realized that Metro Transit actually had a [pretty nice api](http://svc.metrotransit.org/) that exposed the actual GPS coordinates of their vehicles._

Never being totally happy with my command line version and looking for a project that could use a Raspberrry Pi Zero W, I started getting a more artistic vision in my head for the next iteration of my "Transit Tracker". I wanted to take a typical transit-style map and have each part of it light up as trains passed by.

# Building the map #
While I had aspirations of making a laser etched map in Plexiglas, I figured that it was better to get 100% of the way to pretty good than 0% of the way to ideal and I did not see myself getting access to a laser cutter any time soon. So instead I decided to turn to the ever economical wood and paper.

The first step was to print the map out. I took my original image file ([.png](/assets/tracker/light_rail_logo_free.png)\|[.svg](/assets/tracker/light_rail_logo_free.svg)) and broke it apart into several standard printer paper sized pieces using [rasterbator.net](https://rasterbator.net/). After printing it out and trimming off the edges I put them together to determine how big of a board I would need to hold it. I cut the board to length and rounded off the edges.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/painted_wood.jpg"/>

To make the transition from paper to wood less harsh I gave the board a single coat of white spray paint, focusing on covering the edges rather than the center since it was going to be covered by the map.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/base_layer.jpg"/>

After letting the paint dry overnight it was time to attach the map to the board. This is something I had to try twice. The first time I used a really thick layer of Mod Podge between the wood and paper. This ended up leading to a lot of unsightly wrinkles in the map. On the second try I put as thin a layer as I could and placed each sheet individually, taking care to remove any air bubbles that might have been trapped.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/sticking_the_map.jpg"/>

Once the map was firmly glued I added additional layers of Mod Podge to give it a built up finish. The initial layers had to be thin to prevent bubbling, but after the third layer I was able to add more aggressively. I ended up with a total of five layers.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/final_layer.jpg"/>

To display the locations of the trains I'm using an [ALITOVE WS2811 12mm Diffused Digital RGB LED](https://www.amazon.com/gp/product/B01AG923GI/ref=oh_aui_detailpage_o09_s00?ie=UTF8&psc=1) strand. In order to fit the individual LEDs into the map I drilled through the front with a bit matching the size of the LED's bulb. To avoid tearing around the drill site apply only gentle pressure and set the drill press speed to high.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/drill_front.jpg"/>

Since the back end of the LED is significantly larger than the bulb I drilled a half inch hole starting from the back of the board. This hole goes just shy of all the way through the board, so you need to take care to avoid drilling too far.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/drill_back.jpg"/>

After all of the holes were drilled I pushed each LED into its hole. The holes were snug enough that I didn't need to use any additional fasteners. I also added a French cleat for mounting it to the wall.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/plugged_leds.jpg"/>

I decided to keep it simple for mounting the brains of the tracker, setting four eye bolts in the corners of the intended Raspberry Pi mounting area on the backside of the board. Between these bolts I ran a couple rubber bands to hold the Pi and its supporting bread board. While not being the most graceful it did have the benefit of being cost effective and very easy to mount and unmount which was useful during debugging.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/mounted_pi_zero.jpg"/>

I used Jeremy Garff's [rpi_ws281x](https://github.com/jgarff/rpi_ws281x) to confirm that all of the LEDs were working as expected and I hadn't broken anything along the way. After confirming that the Pi could control the LEDs I declared the hardware side of the project of a success. The next step was software, but since that was a significant endeavor on its own I will leave it as the subject of a later post.

<img style="padding: 10px" src="{{ site.url }}/assets/tracker/finished_lights.jpg"/>
