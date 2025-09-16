# StompMini
Stomp Mini is a DIY Percussion Pad similar to the Roland SPD ONE-Kick
FOR CONSTRUCTION DETAILS AND MORE, GO TO YOUTUBE AT https://youtu.be/xr_I2tv7yJs

This project uses an ESP-32 and the compiled code StompMini.  The code includes ten embedded hex PCM data array elements, which are played using the command:

playAudioDAC(audioFiles[counter1], audioSizes[counter1]

The hardware has a local unit with an extension right trigger pad.

The hardware is powered by 5vDC using a standard phone charging block and a matching charging cable with an appropriate USB male that mates with the ESP-32.

The Instruments/Sounds/Samples are selected by the rotary encoder on the Local unit.

REPROGRAMMING A SAMPLE

You can use any short (around a quarter second) .wav file as the source of the sound.  Be advised that the Stomp cannot retrigger until the sample being played is complete.  So, a short .wav file allows rapid repeat triggering
You can get appropriate samples from many internet sources.  One such source is the classic ’80s Linn Drum.  A free sample pack is available for download at:

LinnDrum Samples Free Download | Drum Kits & Sample Packs | Drumkito


Before beginning the process download the following two free pieces of software: 

Download and install Audacity (from Audacity download site), and also download and install HxD https://download.cnet.com/hxd-hex-editor/3000-2352_4-10891068.html (downloaded from CNET download site).

1.  Convert the selected .wav file into .raw format. 
i. Load the .wav file into Audacity. 
ii. Edit it as necessary
iii. Select Export audio.  At the export screen select:
iv. Format: Other uncompressed files	
v. Sample rate: 16000 hz
vi. Header: Raw (header-less)
vii. Encoding: Unsigned 8-bit PCM
viii. Export Range:  Entire Project

2.   Extract the .raw file PCM data to a Hex file with HxD
i. File => New
ii. File => Open => (.raw file name)
ii. Hold down <shift> and use the Mouse to highlight Hex code in screen middle
iv. Copy the selected hex values (<CTRL> C).
iv. Open Notepad.  Select New Tab
v. Copy the selected hex values to Notepad (<CRL> ).

3.  Format the hex values in Notepad:  The ESPStomp8 code needs the hex values to be formatted as  {0xnn, 0xmm...};.   Since the raw file just saved in Notepad looks like {nn mm ...}, 

i.  Add a space at the beginning of the file (before the first Hex value ).
ii. Select Edit -->Replace and in the top block put a space (no quotes, just press spacebar once).
iii. In the block below, type ,0x (comma, followed by the number zero, then lower case x).  
iv. Click Replace All.  
v.  Position the cursor to the very beginning of the file.  Press <DEL> once to remove the first comma.
vi. Type { which will now be the first character in the file.
vii. Move the cursor to the very end of the file.  Type the two characters };
Viii.  Save the file as (wav/raw file name).  For instance, if the original file is Kick.wav, save the Notepad file as Kick.txt.

4. EMBEDDING THE AUDIO FILES

The StompMini code includes ten lines:
const uint8_t audioFile1[] = {.. }
const uint8_t audioFile2[] = {.. }
const uint8_t audioFile3[] = {.. }
const uint8_t audioFile4[] = {.. }
const uint8_t audioFile5[] = {.. }
const uint8_t audioFile6[] = {.. }
const uint8_t audioFile7[] = {.. }
const uint8_t audioFile8[] = {.. }
const uint8_t audioFile9[] = {.. }
const uint8_t audioFile10[] = {.. }

You will embed the hex PCM values (stored in the Notepad .txt file) after the equals sign (=).  As an example, let’s say file one appears as:

const uint8_t audioFile1[] = {0x7B,0x8E,0xAA,0xA4,0xA9,0xA8,0xA7};

In practice the line willl be very long, since it will contain all the hex values needed to create the audio sound.

i.  Position your cursor at the very beginning of the line.
ii. Press <Enter> rapidly three times.  This will highlight the compete line.
iii. Press <DEL> to completely delete this line.
iv. Go to any other of the eight lines and copy the first portion, like

const uint8_t audioFile2[] = 

v. Paste this in the appropriate position (in this instance, it will be pasted before audioFile2[].
vi. Open the Notepad .txt file and copy the complete file.
vii. Paste it after the equals sign (=)
viii. Save and compile the revised code to the ESP-32

Do this for each audio file you want to reprogram.

======================================================================================================================================

Working With an ESP32 in Older Arduino IDE: 
1. Install the ESP32 Board Package

Open Arduino IDE.
Go to File > Preferences.
In the “Additional Board Manager URLs” field, paste this URL:
https://espressif.github.io/arduino-esp32/package_esp32_dev_index.json

Click OK.

2. Install ESP32 Boards via Board Manager
Go to Tools > Board > Boards Manager.
Search for “ESP32 by Espressif Systems”.
Click Install.

3. Select Your ESP32 Board
Go to Tools > Board and choose your specific ESP32 dev board (e.g., ESP32 Dev Module, ESP32-C3 DevKit, etc.).

4. Choose the Correct Port
Plug in your ESP32 via USB.
Go to Tools > Port and select the COM port that appears (it might say something like “ESP32 Dev Module”).
5. Install USB Drivers (if needed)

If your board uses a CP2102 or CH340 USB-to-serial chip and isn’t recognized, you may need to install drivers:
CP210x USB to UART Bridge VCP Drivers

6. Upload Your First Sketch
Try the classic Blink sketch.  Type in:

void setup() {
  pinMode(2, OUTPUT); // GPIO2 is often connected to onboard LED
}

void loop() {
  digitalWrite(2, HIGH);
  delay(500);
  digitalWrite(2, LOW);
  delay(500);
}

Click the Upload button.

If it doesn’t connect, press and hold the BOOT button on your ESP32 while uploading, then release when it starts flashing.

