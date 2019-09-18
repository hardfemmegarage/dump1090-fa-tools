# dump1090-fa-tools
Scripts and stuff for manipulating the json files generated by FlightAware's version of dump1090. Mostly command line.

## Requirements
- a working FlightAware instance of Dump1090 (e.g. PiAware, [this one](https://github.com/flightaware/dump1090))
- a command line
- python
- ncurses
- retrofuturistic dreams

Ncurses scripts are optimized for 80x25 terminal display because there is no need for anything bigger. That said, have at it to hack away for larger terminal windows if you'd like.

> Note: The scripts do *not* have to reside on the same machine that dump1090 is running. Meaning that you can forward output from a dump1090 port to a net-only dump1090 input port on the machine running the script. Alternatively, if you have a URL to an aircraft.json file, it will work -- though for some reason that seems messy.

## Installation
- put scripts somewhere, presumably in your $PATH
- edit variables near the top of your scripts. Details in each script's section below


## The Scripts

### overhead1090-fa

![PFD style display of nearest aircraft](https://github.com/hardfemmegarage/dump1090-fa-tools/blob/screenshots/overhead1090-fa-PFD.png)

Tells you the ICAO (hex) and flight number of the closest aircraft to your Site (lat/lon is user configurable). A delightfully crude ncurses PFD (primary flight display) metaphor is used to indicate other informations such as squawk, altitude, speed, heading, etc. The PFD also indicates trends: meaning it will subtly display whether an aircraft is getting closer are farther from the Site, and whether it is ascending/level/descending.

Additionally, the script calculates the compass bearing of the aircraft from your Site, so you know which direction to look for it.

![PFD style display of nearest aircraft](https://github.com/hardfemmegarage/dump1090-fa-tools/blob/screenshots/overhead1090-fa-LIST.png)

A second mode shows a list of the 20 aircraft nearest your site, sorted by distance from Site.

A third "marquee" mode simply flashes the flight number in the center of the screen... so that you can set up a monitor in your back yard and see in only what is flight over you at the very moment.

#### configuration

Options are found at the top of the script

```python

# Receiver Site Location

# Stock (KSEA)
#SiteLat= 47.449888     #site latitude, decimal degrees
#SiteLon= -122.3117778  #site longitude, decimal degrees

# WOTIK
#SiteLat = 47.56265
#SiteLon = -122.317

# BlauHaus
SiteLat = 47.562978
SiteLon = -122.319394

# Location of aircraft.json file to be used
#   local pathtojson is preferred, a URL can be used as a backup, if you must

pathtojson = '/usr/local/www/hardfemmegarage.org/airtrac/sites/dradis-sea01/data/aircraft.json'
#pathtojson = '/run/dump1090-fa/aircraft.json'

urltojson = 'http://be.nice.com/do/not/steal/without/asking/other/peoples/aircraft.json'
#urltojson = 'http://www.hardfemmegarage.org/airtrac/sites/dradis-sea01/data/aircraft.json'

# Initial ncurse screen to show. opts: pfd, marquee, list, config

display="pfd"

# Time To Sleep... between refresh

tts=1

# Distance threshold. We are interested in aircraft beyond this distance from Site

dxthreshold = 50

# stale report threshold

staleAge = 20

# some verbose shit

verbose = 1

```

### dx1090-fa


![PFD style display of nearest aircraft](https://github.com/hardfemmegarage/dump1090-fa-tools/blob/screenshots/dx1090-fa-PFD.png)

Tells you the ICAO (hex) and flight number of the farthest aircraft to your Site (lat/lon is user configurable). A delightfully crude ncurses PFD (primary flight display) metaphor is used to indicate other informations such as squawk, altitude, speed, heading, etc. The PFD also indicates trends: meaning it will subtly display whether an aircraft is getting closer are farther from the Site, and whether it is ascending/level/descending.


Additionally, the script calculates the compass bearing of the aircraft from your Site, so you know which direction to look for it.


![List style display of farthest aircraft](https://github.com/hardfemmegarage/dump1090-fa-tools/blob/screenshots/dx1090-fa-LIST.png)

A second mode shows a list of the 20 aircraft farthest from your site, sorted by distance from Site. For distance, this is probably the most useful feature as you can see a list of distant contacts and enjoying "dx-ing" like the ham radio folk do. Aging aircraft go dim before disappearing, like eaglets leaving the nest.

#### configuration

Options are found at the top of the script

```python
# Receiver Site Location

# Stock (KSEA)
SiteLat= 47.449888     #site latitude, decimal degrees
SiteLon= -122.3117778  #site longitude, decimal degrees

# Location of aircraft.json file to be used
#   local pathtojson is preferred, a URL can be used as a backup, if you must

pathtojson = '/run/dump1090-fa/aircraft.json'

urltojson = 'http://be.nice.com/do/not/steal/without/asking/other/peoples/aircraft.json'

# Initial ncurse screen to show. opts: pfd, marquee, list, config

display="list"

# Time To Sleep... between refresh

tts=1

# Distance threshold. We are interested in aircraft beyond this distance from Site

dxthreshold = 50

# stale report threshold

staleAge = 20

# some verbose shit

verbose = 1

```
