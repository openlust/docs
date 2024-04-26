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

Flash or Find your device using next options:

1. Plug in your M5 Core2 to a USB port.
2. Hit "Install" and select the correct COM port.
3. Get LUST-Remote firmware installed and connected in less than 3 minutes!

<p>Select your product</p>
<ul class="radios">
<li>
    <label><input type="radio" name="type" value="100mAh" />LUST-Remote With 100mAh Battery (Stock) V2.0.1</label>
</li>
<li>
    <label><input type="radio" name="type" value="1000mAh" />LUST-Remote With 1000mAh Battery Recomended in BOM V2.0.1</label>
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
<script type="module" src="https://unpkg.com/esp-web-tools@8.0.1/dist/web/install-button.js?module"></script>