# Alexa Pi

I wanted to start experimenting with Amazon's Alexa, but didn't have an [Amazon Echo](http://amzn.to/2ct4yJl) on hand.

But [Emily Withrow](https://twitter.com/emilywithrow) mentioned it was possible to run Alexa on a Raspberry Pi -- and I _do_ have one of those.

## Steps I took

First I checked out Amazon's own [Alexa-Raspberry Pi Github Page](https://github.com/alexa/alexa-avs-raspberry-pi) ... which is pretty cool.

I wasn't sure which model Pi I had, so I checked out [this page](https://www.element14.com/community/docs/DOC-78141/l/identifying-your-model-of-raspberry-pi) and determined I had a Verion 1 - B. All of the documentation talks about Verion 2 and 3, but includes a link to [a thread](https://github.com/alexa/alexa-avs-raspberry-pi/issues/2) in which folks are discussing various versions and, in particular, a comment about [using Version 1](https://github.com/alexa/alexa-avs-raspberry-pi/issues/2#issuecomment-202176724)!

Then ...

I downloaded and installed the "Raspbian Jessie" Raspberry Pi operating system as [described in the Amazon documents](https://github.com/alexa/alexa-avs-raspberry-pi#0---setting-up-the-raspberry-pi). Even though some documentation says a 4GB SD card will work, I found you needed something bigger -- so I had to run down the street and pick up a 32GB card.

The Pi version doesn't let you address Alexa by saying "Alexa ... ." Instead, you have to push a button. In the Amazon instructions, that button is virtual -- on the screen the Pi is connected to. 

I wanted to use a physical button, which is described [in a video by Novasprit Tech](https://www.youtube.com/watch?v=frH9HaQTFL8). He has [code to go with it](https://goo.gl/altsmD), too. So I decided to go that way.

Then I followd the instructions in the [video](https://www.youtube.com/watch?v=frH9HaQTFL8).

Cloned the repo with: 

```
git clone https://github.com/sammachin/AlexaPi.git
```


### Notes

- I needed to get a [USB microphone](http://amzn.to/2cZV78n) for my Raspberry Pi.

- I didn't need to do to `apt-get install git` ... as it was already loaded.

- You can't do the setup over SSH (unless you VPN into the desktop, I guess). So I did it from the terminal on the Pi itself, with a keyboard and monitor plugged in. That's because you actually need to hit the pi with its own browser to get the access key.

- In addition, you must be logged into your Amazon developer account on that browser *before* running the setup for the script to get your key!

- I didn't get the error described in the video; my `creds.py` file seemed to be set up correctly.

- I had to force the pi's audio through the 3.5mm jack instead of going to the hdmi cable as described [here](https://www.raspberrypi.org/documentation/configuration/audio-config.md) using:

```
sudo raspi-config
```

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




