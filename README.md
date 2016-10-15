# Alexa Pi

I wanted to start experimenting with Amazon's Alexa, but didn't have an [Amazon Echo](http://amzn.to/2ct4yJl) on hand.

But [Emily Withrow](https://twitter.com/emilywithrow) mentioned it was possible to run Alexa on a Raspberry Pi -- and I _do_ have one of those.

## Ingredients

- **Raspberry Pi** I used an older Version 1-B, but all of the documentation addresses versions 2 and 3. See notes below.
- **USB Microphone** [This is the one I used](https://www.amazon.com/gp/product/B014MASID4/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B014MASID4&linkCode=as2&tag=reall046-20&linkId=400518241321157a5b4a39b4f4fc65cd) and it worked right off the bat.
- **A battery-powered speaker** [like this](https://www.amazon.com/gp/product/B00CLDM1F6/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=reall046-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=B00CLDM1F6&linkId=aad65659fca0ef44f9755709f2b79827).
- **A wifi dongle**

## Steps I took

First I checked out Amazon's own [Alexa-Raspberry Pi Github Page](https://github.com/alexa/alexa-avs-raspberry-pi) ... which is pretty cool.

I wasn't sure which model Pi I had, so I checked out [this page](https://www.element14.com/community/docs/DOC-78141/l/identifying-your-model-of-raspberry-pi) and determined I had a Verion 1-B. All of the documentation talks about Verion 2 and 3, but includes a link to [a thread](https://github.com/alexa/alexa-avs-raspberry-pi/issues/2) in which folks are discussing various versions and, in particular, a comment about [using Version 1](https://github.com/alexa/alexa-avs-raspberry-pi/issues/2#issuecomment-202176724)!

Then ...

I downloaded and installed the "Raspbian Jessie" Raspberry Pi operating system as [described in the Amazon documents](https://github.com/alexa/alexa-avs-raspberry-pi#0---setting-up-the-raspberry-pi). Even though some documentation says a 4GB SD card will work, I found you needed something bigger -- so I had to run down the street and pick up a 32GB card.

The Pi version doesn't let you address Alexa by saying "Alexa ... ." Instead, you have to push a button. In the Amazon instructions, that button is virtual -- on the screen the Pi is connected to.  I wanted to use a physical button, which is described [in a video by Novasprit Tech](https://www.youtube.com/watch?v=frH9HaQTFL8). 

The wiring diagram for the button is [here](https://github.com/jkeefe/AlexaPi/blob/master/Circuit%20diagram_bb.png) -- but be warned, the pins are likely different for various versions of the Pi. The key things to know are:

- Button connects to `GND` and `GPIO 18`
- Red LED connects to `GND` and `GPIO 24`
- Green LED connects to `GND` and `GPIO 25`

Your pins representing those GPIOs may vary.

Novaspirit Tech also has [code to go with the video](https://goo.gl/altsmD), too. So I decided to go that way.

Then I followed the instructions in the [video](https://www.youtube.com/watch?v=frH9HaQTFL8). Though I cloned the updated, original repo using: 

```
git clone https://github.com/sammachin/AlexaPi.git
```

The README in that repo is super useful, too.

### Notes

- I didn't need to do to `apt-get install git` ... as it was already loaded.

- You can't do the setup over SSH -- that is, remotely controlling your Pi -- unless you VPN into the the Pi and use the desktop remotely. This is because at one point during setup you actually need to go to Amazon with the Pi's own browser to get the access key. Instead of setting up a VPN, I just connected an HDMI monitor and keyboard to the Pi itself and worked directly on the Pi using the Terminal. 

- In addition, you must be logged into your Amazon developer account on that browser *before* running the setup for the script to get your key!

- I didn't get the error described in the video; my `creds.py` file seemed to be set up correctly.

- I had to force the pi's audio through the 3.5mm jack instead of going to the hdmi cable as described [here](https://www.raspberrypi.org/documentation/configuration/audio-config.md) using:

```
sudo raspi-config
```

## Managing the Device's Content/Settings

That happens here: https://www.amazon.com/mn/dcw/myx.html



## Random Reference for This Project

### SSH'ing into the Pi

To get the address of my pi, I opened the terminal on the pi and used:  

```
hostname -I
```

... though I'm pretty sure I've figured out before how to find it on my network.

```
ssh pi@10.0.1.18
```

The default password it `raspberry`


### Shutting Down

Reminding myself that to shut down:

```
sudo shutdown -h now
```

And to reboot:

```
sudo shutdown -r now
```

### Using my Wireless Dongle

I have a Netgear NW111v2, which was a specific model for another project. It requires a special driver. Here are my notes from that other project:

```
// Now loading the Carl Driver

// Found how to load it on Raspberry Pi here: http://rfcdotme.blogspot.com/2012/10/installing-carl9170-firmware-on.html

wget 'http://wireless.kernel.org/en/users/Drivers/carl9170/fw1.9.6?action=AttachFile&do=get&target=carl9170-1.fw' -O carl9170-1.fw

// But got the right link from here: http://wireless.kernel.org/en/users/Drivers/carl9170

http://wireless.kernel.org/en/users/Drivers/carl9170?action=AttachFile&do=get&target=carl9170-1.fw-1.9.9

// So

wget 'http://wireless.kernel.org/en/users/Drivers/carl9170?action=AttachFile&do=get&target=carl9170-1.fw-1.9.9' -O carl9170-1.fw

// Then: 

sudo mv carl9170-1.fw /lib/firmware

Connect your USB WiFi device to the board. The Carl9170 should automatically be loaded. 

// had to restart the pi … but then saw that the Antheros was registered as phy0 in the reboot info!
```





