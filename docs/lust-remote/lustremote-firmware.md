---
title: Web Flasher
description: Firmware Web Flasher for LUST-Remote
---

<style>
  .md-content__button {
    display: none;
  }
  .pick-variant select {
    background: transparent;
    width: 300px;
    padding: 1px;
    font-size: 16pt;
    border: 1px solid #ddd;
    height: 51px;
    border-radius: 15px;
  }
  .invisible {
    visibility: hidden;
  }
  .radios li {
    list-style: none;
    line-height: 2em;
  }
</style>

# Web Flasher

Flash or Find your devices using next options:

1. Plug in your M5 Core2 or your OSSM to a USB port.
2. If your device is not Recognices install [ESP32 USB Driver CP210x](https://randomnerdtutorials.com/install-esp32-esp8266-usb-drivers-cp210x-windows/)
3. Hit "Install" and select the correct COM port.
4. Get LUST-Remote and OSSM firmware installed and connected in less than 3 minutes!

<p>Select your product</p>
<ul class="radios">
<li>
    <label><input type="radio" name="type" value="100mAh" />LUST-Remote With 100mAh Battery (Stock) V2.1.0</label>
</li>
<li>
    <label><input type="radio" name="type" value="1000mAh" />LUST-Remote With 1000mAh Battery Recomended in BOM V2.1.0</label>
</li>
<li>
    <label><input type="radio" name="type" value="s3" />LUST-Remote Core S3 With 1000mAh Battery Recomended in BOM V2.1.1</label>
</li>
<li>
    <label><input type="radio" name="type" value="stroke-11-2000-150mm" />OSSM-Stroke HW v1.1 Board 2000 Steps (Fixed Rail Length 150mm)</label>
</li>
<li>
    <label><input type="radio" name="type" value="stroke-22-2000" />OSSM-Stroke HW v2.2 Board 2000 Steps(Sensorless Homing)</label>
</li>
<li>
    <label><input type="radio" name="type" value="stroke-22-800" />OSSM-Stroke HW v2.2 Board 800 Steps (Gold and Prebuild motor)</label>
</li>
</ul>
<p class="button-row" align="center">
<esp-web-install-button class="invisible">
  <button slot="activate" class="md-button md-button--primary">INSTALL</button>
  <span slot="unsupported">Use Chrome Desktop</span>
  <span slot="not-allowed">Not allowed to use this on HTTP!</span>
</esp-web-install-button>
</p>

Powered by [ESP Web Tools](https://esphome.github.io/esp-web-tools/)

<script>
    document.querySelectorAll('input[name="type"]').forEach(radio =>
    radio.addEventListener("change", () => {
        const button = document.querySelector('esp-web-install-button');
        button.manifest = `../files/manifest_${radio.value}.json`;
        button.classList.remove('invisible');
    }
    ));
</script>
<script type="module" src="https://unpkg.com/esp-web-tools@10/dist/web/install-button.js?module"></script>