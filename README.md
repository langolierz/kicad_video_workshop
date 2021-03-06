# kicad_video_workshop

an interactive kicad workshop for diy video-art making instruments

## getting started:

- download [kicad](https://kicad-pcb.org/download/) ( version >=5 )
- download _this_ repo (git clone or as zip under _code_ here)
- open the file in _workshop_project_ / __workshop_project.pro__ with kicad

## the challenge:

together we will try to adapt a video glitch processing circuit created orginally by [Karl Klomp](https://www.karlklomp.nl/) known as __the rupter__. this project and many other interesting historic video hardware glitch machines can be seen on [web-archive](https://web.archive.org/web/20150206171254/https://www.karlklomp.nl/) of their site.

<details>
<summary>details of the original circuit</summary>

### original circuit:

[![image](https://user-images.githubusercontent.com/12017938/97462093-add4c000-193e-11eb-9234-b89c1700fb6e.png)](https://vimeo.com/13738566)


![image](https://user-images.githubusercontent.com/12017938/97461494-1b342100-193e-11eb-9746-ab868f613323.png)

![image](https://user-images.githubusercontent.com/12017938/97461894-79610400-193e-11eb-89d4-a3764f4bab7b.png)


![image](https://user-images.githubusercontent.com/12017938/97349019-3ac04080-188f-11eb-9a8b-2f2abbbc492c.png)

![image](https://user-images.githubusercontent.com/12017938/97349086-51669780-188f-11eb-94a8-aa0cae28450b.png)

### my interpretation:

- [video demo](https://videos.scanlines.xyz/videos/watch/c60b0d9a-0be3-4889-8f0d-863ae294ad4a)

there are a few quirks of this design that make it difficult to adapt to a pcb project:

- its not clear which pot values to use - 100k or 1k ? (100ohm pots are bery uncommon) after testing i liked the effects with 1k_pots better
- although possible to use a rotary switch on pcb, the footprints for these are a little complicated and i opted to use some (cheap) slide switches in parallel instead. lower resistor values seemed to work better here than higher ones. you should experiment for yourself which values to use here !
- a 'circuit bent' style schematic can be difficult to understand since often are based on misusing components. Bastien made a [simulation](https://tinyurl.com/yyvfhpfx) of the first stage which doesnt appear to do much in theory. as is often the case things will be different in practice. 

### further notes on the circuit

from building:

- tried skipping the power regulator part and going 5v straight into the ic -> seems to work quite well 
- [lm317](http://www.learningaboutelectronics.com/Articles/LM317-voltage-regulator) is adjustable voltage regulator - ouput voltage is `1.25*(1 + r2/r1)` where in this case r2=1k and r1=220ohm. so voltage output should be around 7v. confirmed this when building
- i measured the current from the lm317 and was around 20mA so could also use the smaller/cheaper [part](https://www.taydaelectronics.com/lm317lz-lm317l-lm317-0-1a-voltage-regulator-ic.html)
- tried with 200ohm , 1k and 100k pots. all were quite interesting. i would choose 1k pots myself.
- tried with some different cap values. no cap connected gives closer to a clean signal. higher caps tend to just give dropouts (with a few hard to tune effects) lower values seems most interesting. i would experiment some more with which cap values to use.
- i tried to figure out which way to orieintate the pots to make most sense. still it is not that obvious to me. would have to play around with the circuit some more to fine tune this.
- i tried switching -in/out of second opamp to see if liked the effect better but it wasnt as interesting.
- i tested with ntsc and it seems to give better colour glitches than as i remember with pal

</details>

## the schematic

here is a handdrawn schematic of my interpretation which we will try to create in kicad:

![image](https://user-images.githubusercontent.com/12017938/97461205-d1e3d180-193d-11eb-9b7b-289956e5a19f.png)

## some kicad shortcuts

Schematics shortcuts:

- __a__ to add symbol
- __m__ to move symbol
- __e__ to edit symbol
- __c__ to duplicate symbol
- __w__ to draw wire
- _esc_ to return to pointer tool

pcb_route shortcuts:

- __m__ to move item
- __x__ to route track
- __v__ to add via
- _esc_ to return to pointer tool


## links to parts used:

part | footprint | link
--- | --- | ---
rca_jack | - | [mouser](https://www.mouser.de/ProductDetail/CUI-Devices/RCJ-024?qs=%2Fha2pyFaduhcVxkiXFV6ZkU5qdMo9ssjy3LnObhig%2FI%3D), [ali](https://www.aliexpress.com/item/32851836707.html)
spdt_slide_switch | - | [tayda](https://www.taydaelectronics.com/slide-switch-1p2t-through-hole-0-3a-30vdc.html)
spdt_toggle_switch | - | [tayda](https://www.taydaelectronics.com/mini-toggle-switch-spdt-on-none-on.html)
dpst_slide_switch | - | [tayda](https://www.taydaelectronics.com/slide-switch-dpdt-solder-lug-3a-250vac.html)
dpst_toggle_switch | - | [tayda](https://www.taydaelectronics.com/mini-toggle-switch-dpdt-on-on.html)
ad8072 | - | [mouser_dip](https://www.mouser.de/ProductDetail/Analog-Devices/AD8072JNZ?qs=%2FtpEQrCGXCyHkd%2F8k%2FoSBQ%3D%3D)
1k_pot | - | [tayda](https://www.taydaelectronics.com/1k-ohm-linear-taper-potentiometer-round-knurled-plastic-shaft-pcb-9mm.html), [mouser](https://www.mouser.de/ProductDetail/Bourns/PTV09A-4225F-B102?qs=Qzws7J6gxqyeFhc0kO3Q7A%3D%3D)
7pst_rotary_switch | none | [tayda](https://www.taydaelectronics.com/rotary-switch-1-pole-7-position-alpha-sr2511-3599.html), [mouser](https://www.mouser.de/ProductDetail/Alpha-Taiwan/SR2511F-0107-19R0B-E9-S-W-159?qs=8%252Br4Hz5Xir%2FR%2FBhSWT66hw%3D%3D)
