---
title: Hardware
weight: 3
---

I dabble in hardware development (really, mostly hacking existing products to do things I find useful).

### Button board
Through the process of collecting various kinds of psycholinguistic data, I found the need to have a versatile, inexpensive feedback system for participants to use in order to interact with a computer during the course of an experiment. Although button boxes exist already, they are typically very expensive, and not of the form factor we desired for use in experiments.

To solve this, I developed [a button board](https://github.com/jonkeane/buttonBoard) based on a [Teensy 2.0](http://www.pjrc.com/teensy/) microcontroler and a in conjunction with momentary switch (e.g. [Infogrip's Specs Switch](http://www.infogrip.com/products/switches/specs-switch.html)). The microcontroller is flexible enough to provide the computer with virtually any type of {{< smallcaps usb >}} input possible when one of up to 4 buttons are pressed.

### Kindle weather and {{< smallcaps cta >}} arrival times display

After seeing [a number](http://mpetroff.net/2012/09/kindle-weather-display/) [of people](https://github.com/pjimenezmateo/kindle-wallpaper) [make](http://hackaday.com/2013/04/01/kindle-weather-and-recycling-display/) [various](http://www.shatteredhaven.com/2012/11/1347365-kindle-weather-display.html) persistent display devices with kindles, I decided that what I really needed was a display for weather as well as various {{< smallcaps cta >}}  arrival times near my apartment.

I developed a [setup](https://github.com/jonkeane/kindle-weather-display) that grabs weather from [wunderground](http://www.wunderground.com/weather/api/) or [forecast.io](https://developer.forecast.io/), as well as arrival times for a limited number (5 currently, due to space restrictions of the kindle) of {{< smallcaps cta  >}} stops and stations. Then displays the arrivals persistently, and cycles through: current weather conditions, a 12 hour forecast, and a 5 day forecast.

Not content to just tack a kindle on the wall, I built [a wood frame](https://www.flickr.com/photos/jonkeane/sets/72157639487321246/) using a laser cutter to house the kindle and reroute the usb cable for charging.

{{< figure src="kindleWeather.jpg" alt="Image of the kindle weather and arrival times display, in a wood frame." class="scale-with-grid">}}
