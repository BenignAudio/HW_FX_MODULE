# HW_FX_MODULE

In deze readme wordt beschreven wat de voortgang is van onze hardware FX module.

PROJECTVOORSTEL (1e opzet) Teensy Pedal (Multi-) FX w Eurorack Integration (optioneel)

Overzicht
____________________________________________________________________
In dit document leg ik uit hoe ik getracht heb een standalone, Teensy-gestuurde module te maken, waarbij de gebruiker middels draaiknoppen een voorgeprogrammeerd effect/effecten naar keuze kan beïnvloeden. 
De module is dusdanig ontworpen dat de gebruiker zelf de code voor het gewenste effect oplevert; gezien deze digitale signaalprocessor voorprogrammeerbaar is, is het mogelijk meerdere effecten door de signaalketen uit te sturen, waarbij er met vijf draaiknoppen geruime parametrische speelruimte is.  
Voor dit voorbeeld heb ik een vrij eenvoudig stukje dummy-script geschreven.
Doelen
Het vrijelijk transformeren van een signaal door middel van een teensy & draaiknoppen..
De module acht voorprogrammeerbaar te zijn.

Doelstelling Hardware lessenreeks:
____________________________________________________________________
Simpel FX pedaaltje ontwerpen- hooguit 1 a 2 effecten (eg. delay/buffer loop), zodat die processing in ieder geval ook ‘ goed’ klinkt, voorzover dat mogelijk is, en eventueel als uitbreiding de mogelijkheid om het icm Eurorack standard te gebruiken.
Simpele switch van gitaarpedaal(modus) => mono jack thru, geen voeding nodig (althans, de Teensy wel), naar Eurorack (CV) >>> +5V|+12V|GND|GND|GND|-12V






Materialenlijst:
____________________________________________________________________
Vijf (5) 		x			Elektrolytische ontkoppelingscondensator - 10uF/25V
Een (1) 	x			Teensy 3.2
Een (1)		x			Teensy Audio Board (3.x)
Een (1)		x			DIP Socket Soldeervoetje - 8-pin
Een (1)		x			Op-amp - LM358
Vijf (5)		x			Knop - 15x19mm
Vijf (5)		x			Draaipotmeter - 10k Ω, lineair
Een (1)		x			Spanningsregelaar - 5V (L7805)
Twee (2)	x			Weerstand - 1M Ω
Twee (2)	x			Weerstand - 100K Ω
Twee (2)	x			Weerstand - 22K Ω
Twee (2)	x			Weerstand - 10K Ω
Veertig (40)	x			Break-away headers - recht
± Vijftig (50)	x			Kabeltjes - Solid core/stranded - 22 AWG
Een (1)		x			9 Volt batterij aansluitkapje
Een (1)		x			3PDT foot switch
Twee (2)	x			TRS jackaansluitingen (¼”)
Een (1)		x			2.1mm barrel jack DC aansluiting
Een (1)		x			3-pole switch







Gereedschap:
____________________________________________________________________
Soldeerbout
Soldeertin
Kniptang
Eventueel een punttang
Schroevendraaier (- & +)
Breadboard
Breadboard kabeltjes
Kabelstripper
Eventueel labvoeding;
zo niet, gebruik dan een voedingsadapter met kabel

Toegang tot een computer met internet is een vereiste om je eigen code te kunnen toevoegen! >>> Verdere benodigdheden worden nog toegevoegd. => bypass input tevens al gesoldeerd! (EDIT)


Sub-circuits:
____________________________________________________________________
De module bestaat uit een aantal sub-circuitjes. Deze omvatten:
Input buffer circuit (AUDIO-IN)



Output versterker circuit (AUDIO-OUT)



Spanningsregelaar circuitje met aan en uit knop.



Circuit analoge besturing
	


Stappen:
____________________________________________________________________
Voltage Regulator



Input Buffer



Output Amplifier



Potmeters/ Verbinding Teensy



Arduino Library Code

#include <Audio.h>
#include <Wire.h>
#include <SPI.h>
#include <SD.h>
#include <SerialFlash.h>

// GUItool: begin automatically generated code
AudioSynthWaveformDc     dc1;            //xy=63,352
AudioInputI2S            i2s1;           //xy=64,219
AudioFilterBiquad        biquad3;        //xy=201,250
AudioSynthWaveformSine   sine1;          //xy=201,397
AudioFilterBiquad        biquad1;        //xy=202,176
AudioFilterBiquad        biquad2;        //xy=202,213
AudioEffectMultiply      multiply1;      //xy=211,346
AudioMixer4              mixer1;         //xy=356,213
AudioAnalyzePeak         peak1;          //xy=357,292
AudioFilterStateVariable filter1;        //xy=373,352
AudioOutputI2S2          i2s2_1;         //xy=516,345
AudioConnection          patchCord1(dc1, 0, multiply1, 1);
AudioConnection          patchCord2(i2s1, 0, biquad1, 0);
AudioConnection          patchCord3(i2s1, 0, biquad2, 0);
AudioConnection          patchCord4(i2s1, 0, biquad3, 0);
AudioConnection          patchCord5(biquad3, 0, mixer1, 2);
AudioConnection          patchCord6(sine1, 0, filter1, 1);
AudioConnection          patchCord7(biquad1, 0, mixer1, 0);
AudioConnection          patchCord8(biquad2, 0, mixer1, 1);
AudioConnection          patchCord9(multiply1, peak1);
AudioConnection          patchCord10(multiply1, 0, filter1, 0);
AudioConnection          patchCord11(mixer1, 0, multiply1, 0);
AudioConnection          patchCord12(filter1, 0, i2s2_1, 0);
// GUItool: end automatically generated code
