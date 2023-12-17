+++
author = "Otto"
title = 'Beomaster 4000 Lamp Replacement'
date = 2021-12-15T14:30:17+02:00
image = "/images/dogs.jpg"
draft = false
+++

(Note this was first published on beoworld.org in 2021 but they removed the old posts)
# Background 
Like a lot older B&O systems, the Beomaster 4000 uses filament lamps. In most of the vintage B&O's these lamps are soldered but the lamps in the Beomaster 4000 fits into a holder. An ideal replacement would be LED's that directly fit into these holders. One additional factor to keep in mind is that the power lamp (red) runs from 22V AC while the other lamps run from 13-14V DC.

# Disassembled lamp. 
Normally you will not remove the complete shell on the right, you will simply pull out the holder in the middle from the inside. The lamp will come out with it. In this case removing took some effort after 40+ years and therefore the complete holder was removed.

![Disassembled lamp2](/images/b4lampass.jpg)

# Mechanical fit of LED replacements

![LED in Holder](/images/BO4LEDinHolder.jpg)


After several failures I have settled on using a cutoff pcb and SMD (surface mount) components. Most PCBs are 1.6mm thick but the slot for the lamp is about 2.3mm. The PCB will therefore need some "thickening". I have used 2 different approaches below. 

# Resistor Calculations
To limit the current some resistances are needed. Also keep in mind that the dissipation of resistances are limited and must be taken into account in this application. The calculations are shown below.

# LED selection

Surface mount LED's come in different sizes. Most of them are rated 20-25mA maximum. Any one of these can be used. The color obviously depends on the color of the lamp, most are red except for the stereo lamp which is green. If you only have white LED's available, these can also be used.

Comment: I have tried using 5mm through hole LEDs because they are more readily available but eventually gave up because the fit is to tight.
22V ac lamp replacement

# Resistor selection 

The power rail is 22V ac. The LED design should limit the current to the LED's to <20mA (preferably about 10-14mA) using a resistor that can dissipate the heat.

Assuming the voltage drop across the LED is about 2V and assume the RMS voltage is still 22V (a bit more complex due to halfwave rectification but wiil ignore that for this calculation), and the current is 10mA:
    R = V/I = (22-2)/10mA = 2k ohm

The dissipation through the resistor will then be:
   P = VI = 20*10mA = 200mW

The maximum power dissipation for common SMD resistor sizes:
Imperial 	Metric 	Watt
0603 	1608 	1/10 (0.10)
0805 	2012 	1/8 (0.125)
1206 	3216 	1/4 (0.25)

# AC lamp
From the table a 1206 SMD resistor should be ok, but taking into account that this rating is applicable in free air movement @ 25C,  it is better to select a larger resistor size or use 2 x 1k in series. The advantage of 2 in series is that it is easier to get 1k resistors. Combining it, the final circuit is 


![AC LEDs on PCB](/B4Lamp2LEDac.jpg)

My LED build (sorry soldering is not up to scratch)

Note the 2 LED's back to back which will each light up in one of the 2 half cycles of the 50Hz AC.

I used vero board but any old pcb, e.g. old PC card, with an edge connector can be cut for this purpose.

Note that I have changed the resistor positions with one resistor on each side of the LEDs.


Not shown is a thin shim (about 1mm) glued to the bottom because the PCB is to thin.

# DC lamps (13-14Vdc)

Similar to the calculations above:    R = V/I = 11/10mA = 1.1 kilo ohm 

To make it simpler, select 1k resistor for this one as well.

The dissipation through the resistor will then be about:
   P = VI = 10*11mA = 110mW

So one SMD 1206 1k ohm resistor should do it. If you need a brighter display, you can also add more LED's in series. (You can reduce the resistor to 680 or 820 ohm for 2 LED's in series but 1k should still be fine)

Note that in this case the LED orientation is important. If it does not work the first time, switch the orientation.


The DC LED PCB. Note that this pcb was not shimmed. I used thin wires, seen on the left, that folds under the pcb. This ensures much better contact  with the socket.

![LED on PCB](/images/BO4LEDinHolder.jpg)

LED fitted into holder.