# dump1090-fa-tools
Scripts and stuff for manipulating the json files generated by FlightAware's version of dump1090. Mostly command line.

## Requirements
- a working FlightAware instance of Dump1090 (e.g. PiAware, [this one](https://github.com/flightaware/dump1090))
- a command line
- python
- ncurses

> Note: The scripts do *not* have to reside on the same machine that dump1090 is running. Meaning that you can forward output from a dump1090 port to a net-only dump1090 input port on the machine running the script. Alternatively, if you have a URL to an aircraft.json file, it will work -- though for some reason that seems messy.

## Installation
- put scripts somewhere, presumably in your $PATH
- edit variables near the top of your scripts:

```python
SiteLat= 47.449888     #site latitude, decimal degrees
SiteLon= -122.3117778  #site longitude, decimal degrees

# time to sleep; how often to update the screen?
tts= 1   

# system path to the aircraft.json file generated by your FlightAware version of Dump1090
pathtojson = /run/dump1090-fa/aircraft.json

# alternatively a URL to the aircraft.json file generated by a FlightAware version of Dump1090 
# (be nice, don't steal people's aircraft.json without asking)
hosturl = 

#(initial) distance for assembled list of aircraft closest/nearest to your Site
dxthreshold = 100
```

## The Scripts

### overhead1090-fa

Tells you the ICAO (hex) and flight number of the closest aircraft to your Site (lat/lon is user configurable). A delightfully crude ncurses PFD (primary flight display) metaphor is used to indicate other informations such as squawk, altitude, speed, heading, etc.

Most interestingly, the script calculates the compass bearing of the aircraft from your Site, so you know which direction to look for it.

A second mode shows a list of the 20 aircraft nearest your site, sorted by distance from Site.

A third "marquee" mode simply flashes the flight number in the center of the screen... so that you can set up a monitor in your back yard and see in only what is flight over you at the very moment.

### dx1090-fa

![PFD style display of farthest aircraft](https://github.com/hardfemmegarage/dump1090-fa-tools/blob/screenshots/dx1090-fa-PFD.png)

Tells you the ICAO (hex) and flight number of the farthest aircraft to your Site (lat/lon is user configurable). A delightfully crude ncurses PFD (primary flight display) metaphor is used to indicate other informations such as squawk, altitude, speed, heading, etc.

Most interesting, the script calculates the compass bearing of the aircraft from your Site, so you know which direction to look for it.


![PFD style display of farthest aircraft](https://github.com/hardfemmegarage/dump1090-fa-tools/blob/screenshots/dx1090-fa-LIST.png)

A second mode shows a list of the 20 aircraft farthest from your site, sorted by distance from Site. For distance, this is probably the most useful feature as you can see a list of distant contacts and enjoying "dx-ing" like that ham radio folk do.
