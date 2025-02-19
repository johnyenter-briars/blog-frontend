---
title: projects
date: 2021-10-28 11:43:32
---
<style>
  .toggle-container {
      display: flex;
      align-items: center;
      gap: 10px;
      cursor: pointer;
  }

    .toggle-switch {
        width: 40px;
        height: 20px;
        background: #333; 
        border-radius: 10px;
        position: relative;
        display: inline-block;
        transition: 0.3s;
        box-shadow: none; 
    }


  .toggle-thumb {
      width: 18px;
      height: 18px;
      background: #10ffcb; 
      border-radius: 50%;
      position: absolute;
      top: 1px;
      left: 2px;
      transition: 0.3s;
      box-shadow: 0 0 5px #0ff;
  }

  .toggleImages:checked + .toggle-switch .toggle-thumb {
      left: 20px;
  }

  .toggleImages:checked + .toggle-switch {
        box-shadow: 0 0 8px rgba(0, 255, 255, 0.6); 
        background: #111; 
    }


  .imageGrid {
      display: none;
      margin-top: 10px;
      grid-template-columns: repeat(2, auto);
      gap: 10px;
  }
</style>

<script>
function toggleImages(gridId, checkboxId) {
    var grid = document.getElementById(gridId);
    if (document.getElementById(checkboxId).checked) {
        grid.style.display = "grid";
        grid.style.animation = "fadeIn 0.3s ease-in-out"; 
    } else {
        grid.style.display = "none";
    }
}
</script>

# My Projects

### Harmonize

A multi-media management app + server. Designed to take in audio + video media from a variety of sources, and blend it seamlessly from a unified UI. Currently the app is in MVP status, as several critical features like audio are not fully implemented. I hope to finish it one day.

[Source Code](https://github.com/johnyenter-briars/harmonize)


<label class="toggle-container">
    <input type="checkbox" id="harmonize-toggleImages" class="toggleImages" style="display: none;" onclick="toggleImages('harmonize-imageGrid', 'harmonize-toggleImages')">
    <span class="toggle-switch">
        <span class="toggle-thumb"></span>
    </span>
    <span style="color: #c9cacc;">Show Images</span> 
</label>

<div id="harmonize-imageGrid" class="imageGrid">

<img src="/images/harmonize/harmonize1.jpg" width="150px">
<img src="/images/harmonize/harmonize2.jpg" width="150px">
<img src="/images/harmonize/harmonize3.jpg" width="150px">
<img src="/images/harmonize/harmonize4.jpg" width="150px">

</div>

---

### gruvbox-material-vs

A simple yet elegant theme for Visual Studio designed to replicate the brilliant [Gruvbox Material](https://marketplace.visualstudio.com/items?itemName=sainnhe.gruvbox-material) plugin. I've been thrilled that ~4.5k people have given it a try!

[Source Code](https://github.com/johnyenter-briars/gruvbox-material-vs)
[Download and Install](https://marketplace.visualstudio.com/items?itemName=jyb.gruvbox-material-vs)

<label class="toggle-container">
    <input type="checkbox" id="gruvbox-toggleImages" class="toggleImages" style="display: none;" onclick="toggleImages('gruvbox-imageGrid', 'gruvbox-toggleImages')">
    <span class="toggle-switch">
        <span class="toggle-thumb"></span>
    </span>
    <span style="color: #c9cacc;">Show Images</span> 
</label>

<div id="gruvbox-imageGrid" class="imageGrid">

<img src="https://raw.githubusercontent.com/johnyenter-briars/gruvbox-material-vs/refs/heads/master/media/gruvbox-material-dark-custom.jpg" width="100%">
<img src="https://raw.githubusercontent.com/johnyenter-briars/gruvbox-material-vs/refs/heads/master/media/gruvbox-material-dark.jpg" width="100%">

</div>

---

### CAL

CAL is a simple app for CALendar management. Built on Maui with heavy use of [XCalendar](https://github.com/ME-MarvinE/XCalendar), CAL has been my daily calendar for 3 years.

[Source Code](https://github.com/johnyenter-briars/cal)

<label class="toggle-container">
    <input type="checkbox" id="cal-toggleImages" class="toggleImages" style="display: none;" onclick="toggleImages('cal-imageGrid', 'cal-toggleImages')">
    <span class="toggle-switch">
        <span class="toggle-thumb"></span>
    </span>
    <span style="color: #c9cacc;">Show Images</span> 
</label>

<div id="cal-imageGrid" class="imageGrid">

<img src="/images/cal/cal1.jpg" width="15%">

</div>

---

### Chess Engine

Chrust is a chess engine written in Rust. Its supposed to be a cute name combining the words "Chess" and "Rust". Its a simple AI, but suprisingly affective - if you can beat it, I'd love to hear about it!

[Source Code](https://github.com/johnyenter-briars/chrust)
[Live](/chrust)

<label class="toggle-container">
    <input type="checkbox" id="chrust-toggleImages" class="toggleImages" style="display: none;" onclick="toggleImages('chrust-imageGrid', 'chrust-toggleImages')">
    <span class="toggle-switch">
        <span class="toggle-thumb"></span>
    </span>
    <span style="color: #c9cacc;">Show Images</span> 
</label>

<div id="chrust-imageGrid" class="imageGrid">

<img src="/images/chrust4.png" width="50%">

</div>

---

### Reverse Date Parser

RDP is a web application allowing developers to insert a string formatted like a date. It then returns the possible date format strings that could compile to the given date string. Inspired by [Crontab Guru](https://crontab.guru/) its designed to reduce the ammount of times developers need to ask: "wait, does the string 'May' correspond to 'MMM' or '%M'?"

[Source Code](https://github.com/johnyenter-briars/chrust)
[Live](/rdp)

<label class="toggle-container">
    <input type="checkbox" id="rdp-toggleImages" class="toggleImages" style="display: none;" onclick="toggleImages('rdp-imageGrid', 'rdp-toggleImages')">
    <span class="toggle-switch">
        <span class="toggle-thumb"></span>
    </span>
    <span style="color: #c9cacc;">Show Images</span> 
</label>

<div id="rdp-imageGrid" class="imageGrid">

<img src="/images/currentrdp2.png" width="60%">

</div>

---

### Media-System

Media-System is an open source home media system I cobbled together using [LibreELEC OS](https://libreelec.tv/) installed on a [Raspberry Pi](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/). I then built an [Android App](https://github.com/johnyenter-briars/media-system-client) to control the system through its API.

I wrote a blog about the process [here](/2022/02/07/mediasystem).

<label class="toggle-container">
    <input type="checkbox" id="mediasystem-toggleImages" class="toggleImages" style="display: none;" onclick="toggleImages('mediasystem-imageGrid', 'mediasystem-toggleImages')">
    <span class="toggle-switch">
        <span class="toggle-thumb"></span>
    </span>
    <span style="color: #c9cacc;">Show Images</span> 
</label>

<div id="mediasystem-imageGrid" class="imageGrid">

<img src="/images/mediasystemapp.png" width="45%">

</div>

---

### Automata Tutor Updates

Automata Tutor is this weird obtuse software developed by some phd researchers in Germany for constructing and distributing Automata theory problems to students.
For a summer research project in 2020, I worked with my professor to update it's functionality and UI.

[Source Code](https://github.com/johnyenter-briars/AutomataTutorUpdates)








