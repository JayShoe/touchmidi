# TouchMIDI
Flexible HTML5 based control surface for controlling external devices via MIDI

Designed for use on touch screen devices, but also compatible with keyboard and mouse. A range of simple widgets is supported:
 * Vertical slider
 * Horizontal slider
 * Push button
 * Toggle button
 * Round encoder / knob
 * XY Pad

Supported MIDI messages are:
 * Note On & Note Off - For button widgets
 * CC - For all widgets
 * NRPN - For all widgets (planned)
 * Bank/patch change - For all widgets (planned)

Layout is done via HTML, but simplified, everything is laid out with div tags, four basic containers (e.g. row, column) and custom attributes. e.g.
```html
<div class="row">
  <div class="widget slider_v" colour="#EE8800" midicc="1, 51" label="#"></div>
</div>
```
Adds a slider widget, with a orange colour which will send MIDI control change (CC) number 51 on MIDI channel 1

## MIDI Actions
There are various MIDI actions that can be attached to a widget, this is done via standard XML/HTML attribute, e.g. `midinote="1, 2, 3"`. The parameters are positional so **_order is important_**. Parameters are comma seperated and expected to be integers, some minimal parsing and type checking is done, but beware. Multiple actions of the same type can be specified, seperated with a pipe, e.g. `midinote="1, 55, 127|1, 57, 64`. The action types closely map to various MIDI message types, as follows:

* **MIDI Note**

Send MIDI note on and off messages. Supported widget types: **`button`** only. Note on is sent when the button is first pressed, Note off sent when it is released. For toggle buttons the note will be held, which is useful for latching arpegigators
```bash
midinote="channel, note_number, velocity"
```

* **MIDI Control Change (CC)**

This is used to send control change messages with a range of values. Supported widget types: **ALL**. This action sends standard MIDI control messages, where the CC number = 0-127, for additional or equipment specific control messages a NRPN should be used (see below)
```bash
midicc="channel, cc_number [, val_on] [, val_off]"
```
The value sent is dependant on the widegt type:




### Tested Browsers
Tested on Chrome v49. Chrome is the only browser known to work due to limited MIDI support in other browsers e.g. Firefox and Safari do not support the Web MIDI API spec https://www.w3.org/TR/webmidi/

### Example Screenshots
![Screenshot](https://cloud.githubusercontent.com/assets/14982936/14225681/730c9920-f8c3-11e5-8b15-d5865770c0a2.png)
