---
layout: post
title:  "Tacspeak - speech recognition for gaming"
date:   2023-12-14 17:47:00 +1100
categories: blog
tags: tacspeak speech recognition gaming asr kaldi dragonfly
excerpt_separator: <!--more-->
---
Tacspeak - speech recognition for gaming. I made something cool! 

Link to [Youtube video](https://youtu.be/qBL0bCt_VMo) of me playing Ready or Not, commanding the AI with Tacspeak.

[![Watch the video demo of me using Tacspeak while playing Ready or Not](https://img.youtube.com/vi/qBL0bCt_VMo/maxresdefault.jpg)](https://youtu.be/qBL0bCt_VMo)

Link to [Tacspeak Github repo](https://github.com/jwebmeister/tacspeak) 

Link to [Tacspeak Nexusmods mod page](https://www.nexusmods.com/readyornot/mods/3159)

<!--more-->
---

Tacspeak has been designed specifically for **recognising speech commands while playing games**, particularly system resource and FPS hungry games!

**Fast** - typically on the order of 10-50ms, from detected speech end (VAD) to action.

**Lightweight** - it runs on CPU, with ~2GB RAM.

**Modular** - you can build your own set of voice commands for additional games, or modify [existing ones](tacspeak/grammar).

**Open source** - you can modify any part of Tacspeak for yourself, and/or contribute back to the project and help build it as part of the community.

---

Tacspeak is built atop the excellent [Dragonfly](https://github.com/dictation-toolbox/dragonfly) speech recognition framework for Python. 
- Note: Tacspeak uses a *modified version* of Dragonfly located at [jwebmeister/dragonfly](https://github.com/jwebmeister/dragonfly).
- Please see the Dragonfly [docs](http://dragonfly.readthedocs.org/en/latest/) for information on building grammars and rules (i.e. voice commands). 
- Please also see the existing [examples](tacspeak/grammar) of Tacspeak grammar modules.

Also built atop the excellent [Kaldi Active Grammar](https://github.com/daanzu/kaldi-active-grammar/), which provides the [Kaldi](https://github.com/kaldi-asr/kaldi) (also excellent) engine backend and model for Dragonfly.

---

See the links below for more info:

- [Tacspeak Github repo](https://github.com/jwebmeister/tacspeak) 
- [Tacspeak Nexusmods mod page](https://www.nexusmods.com/readyornot/mods/3159)
- [Youtube video](https://youtu.be/qBL0bCt_VMo) of me playing Ready or Not, commanding the AI with Tacspeak.