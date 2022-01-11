---
title: Building an Open Source Media System
date: 2022-01-10
---

### Intro

I don't like Netflix or other big streaming services engorging themselves on my data. Nor do I use streaming services at all in my free time. Instead, I only watch movies through playing movie/tv show files in VLC and youtube.

As such, I realized I could strip out all proprietary software from my media consumption by building my own home media system. If you would like to learn how I did it, keep reading!

The basic idea is:  install a media system program on my raspberry pi, then build an android app to control the system via it's API.

#### Components

- [Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/)
- [LibreELEC OS](https://libreelec.tv/)
- [Android App](https://github.com/johnyenter-briars/media-system-client)

#### Installing on the PI

[Kodi](https://kodi.tv/) is an open source video playing software, supporting extended functionality through the use of add-ons. As such, it's the obvious choice for my media system. Kodi is just a program, so it needs an operating system to host it. In theory, I could have installed Kodi on the default OS installed on my Pi: [Raspbian](https://www.raspberrypi.com/software/). However, this is not advised since the OS would have to work on managing other processes which are *not* Kodi.

So instead, I chose an OS that is designed to host *only* KODI. Origionally, I had planned to use [OSMC](https://osmc.tv/), but I also tried [LibreELEC OS](https://libreelec.tv/) and liked it's design, philosophy, and community much more. 

Installing the operating system was just as simple as [installing](https://www.makeuseof.com/tag/install-operating-system-raspberry-pi/) any other OS on a Pi. Both operating systems are available on the Raspberry Pi Imager.

![](/images/pi-imager.png)

#### Building the App

Building the app was the most labor intensive part, but the most rewarding. I used [Android Studio](https://developer.android.com/studio) to develop the app, and chose [Kotlin](https://kotlinlang.org/) as the language. The app didn't need to be super complex, just a simple UI with buttons and sliders which make POST requests to the KODI JSON-RPC API.

As always, Android Studio makes it a breeze to build, test, and install apps.

![](/images/building-app.png)

Having never worked with Kotlin before, it was definitely an interesting challenge. Since the app is fairly simple, I didn't have a chance to really get into the nitty-gritty of Kotlin. But I did come away with some thoughts on the language. Perhaps those thoughts will make their way to a future blog post. 

You can find the source code for the app [here](https://github.com/johnyenter-briars/media-system-client)

#### Static Ip

One flaw in its current design is the nature of my Raspberry Pi's dynamic internal ip. By default, home routers are set to assign ip leases dynamically. This means that as new devices enter and leave the network (and reboot) they get assigned a new ip, depending on the next available address. 

In order to ensure that the system would keep the same ip, even on multiple restarts, I had to assign it a reserved ip by logging into my router and setting up a reserved ip for the raspberry pi.

![](/images/reserved-list.png)

#### Putting it all Together

Words are boring, so here's a diagram laying out the components and how they talk to one another over the network.

![](/images/mediasystemdiagram1.png)

#### Watching a Movie

![](/images/using-app.jpg)