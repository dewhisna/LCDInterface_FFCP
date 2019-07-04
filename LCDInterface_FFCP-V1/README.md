# FlashForge 2016 LCD/SDCard/Keypad Interface

See this on Thingiverse: [https://www.thingiverse.com/thing:2007070](https://www.thingiverse.com/thing:2007070).

I'm tired of having SDCard read issues on my FlashForge Creator Pro 2016 printers.  I have three of those printers and all three have issues.  After digging through and analyzing the schematics, I think the primary culprit is either ringing or a slight timing skew between the SCLK timebase and the unbuffered MISO data output from the SDCard.  SDCards aren't designed to drive their data output down a 300mm ribbon cable.

Then if you add the other issues of no bypass capacitors, limited decoupling capacitors, no ESD protection, long off-board 3.3V power runs, and abuse of a 74AHC125 as a voltage level translator, it's a wonder, as Gary described with his [LCD ESD Protection board](https://www.thingiverse.com/thing:91656), "that it works at all".

I originally looked at just building one of [Gary's LCD ESD Protection boards](https://www.thingiverse.com/thing:91656) for each of my printers, since the circuit in my FlashForge Creator Pro 2016 printers is nearly identical to the Replicator design.  But, I decided that it physically wouldn't fit the printer all that well.

Since I had to make the boards regardless, I decided instead to completely redesign the main LCD Interface Board of the FlashForge -- which is the bottom board in the stack inside the LCD panel where the LCD and Keypad boards plug into.  That board had plenty of free space on it that could be used for the additional circuitry.  So, I took the circuit of the FlashForge Interface, which wasn't difficult to sketch out since it's nearly identical to the MakerBot Replicator Interface, and added the components of [Gary's LCD ESD Protection board](https://www.thingiverse.com/thing:91656) to it.

This board is the result...  a new drop-in replacement for the original FlashForge LCD Interface.  The only extra connection is the ESD Ground connection pad, which is designed to have a wire soldered to it and run to the chassis ground of the printer, which has a nice, convenient terminal connector in the electronics compartment of the printer near the power supply (see the posted pictures).  Unlike Gary's situation, the FFCP has some metal chassis parts already and has an earth ground in place, which is really convenient.

This board also adds pads for both the red and green LEDs that have signal runs from the MightyBoard, which are completely omitted on the original FlashForge Interface.  They may be useful if you are doing custom firmware coding work and need some extra LEDs for debugging and feedback -- otherwise, just don't populate them when you build this board.

I also added an option for an adjustable contrast control for the LCD, in addition to pads for the fixed resistor values that the FlashForge Interface uses.  This allows you to populate it either way.  If you want the simple, fixed-level contrast like the FFCP has, just populate the two fixed resistors that set that.  If you want to control it manually, mount the potentiometer instead.  Just don't mount both sets of components on the board or else the contrast level control will be a little wonky.

The board is nearly all surface-mount parts, but I used the larger 1206 size parts for the discrete components and I used the larger copper landing zones on all the footprints on the PCB to make it easier to hand-solder, though while assembling mine, I found the larger pads on the 1206 parts a bit annoying.

The hardest pieces to solder are the 74LVC1T45 chips, being a TSSOP-6 package with 0.65mm lead spacing.  TSSOPs are easier to hand-solder than you might think, but you will need a decent soldering iron, a bright work light, a magnifier glass, and some solder wick.  When assembling these boards, start with those pieces first so that the other components aren't in your way.  Also, after doing the TSSOP's, the SOIC's will feel huge and so will the rest of the components. 

Boards can be ordered from OSHPark: [https://www.oshpark.com/shared_projects/4YWmcdYh](https://www.oshpark.com/shared_projects/4YWmcdYh)

The schematic, bill-of-materials, and PCB Gerber files have been posted here in the files section.

**Update (15-Jan-2017)**: I've received my boards from OSHPark and got them assembled.  It came up and ran fine first time with no issues.  So I've removed the "work in progress" flag.

I did make one last-minute change in the parts I used from what is posted in the bill-of-materials.  I decided to use a 0.001uF (1000pF) capacitor for C2 for the loading on the SDCard SCLK signal, instead of the 0.1uF.  I decided on this change after running some numbers on the signal rise-time change that the added capacitor will create for the frequencies I believe the ATmega would most likely be using for the SDCard, based largely on calculation details in the textbook "High-Speed Digital Design: A Handbook of Black Magic".  As far as I know, either value will work.  The 0.001uF is working fine on my boards, and Gary previously proved out the 0.1uF on the board in his design.  I just felt more comfortable with the 0.001uF part.  So the part I actually used for C2 was DigiKey 709-1036-1-ND.

Otherwise, my boards were assembled as-per the diagram and bill-of-materials.  And I did install the ferrite cable clamp that Gary suggested, as seen in my posted pictures and included in the bill-of-materials.

So far the new board has been working with no issues and with no read errors from the SDCard.  Though the original FlashForge board worked OK sometimes too, so only time will confirm if I have truly solved the SDCard issues I previously had.

If I were to make any changes to the board on a future version, I would reduce the size of the 1206 SMD pads a bit, as I found them a bit annoying during hand-soldering with them being so large, even though the larger pads supposedly facilitates hand-soldering.  And, I would increase the annular ring size of the vias.  The vias seem to be fine and are working well, but I always feel more comfortable being generous with design rules, and they came out a bit smaller than I had intended.  And I would move the LEDs and the contrast control to the other side of the board to where they can be used with the LCD installed, making it possible to drill holes in the plastic LCD panel to access them.

For reference, I posted a picture of my board along side the original (green) FlashForge board so you can compare them.

**Update (23-Jan-2018)**: It's now been a full year since I built these to go on my FlashForge printers.  And I'm happy to report that with these boards, I've had zero read failures from the SDCard on any of my three printers, and they've logged many hundreds of hours of printing.  On the original boards that came with the printer, I experienced a read failure roughly six times out of every ten card insertions.  I believe I can safely claim they have completely resolved my SDCard issues.
