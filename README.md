# Ketron EVM-Button-Controller

This MIDI Pad Controller for Ketron EVM Sound Module is based on the Adafruit MacroPad RP2040 circuit board:
 
- Adadfruit kit: https://www.adafruit.com/product/5128
- Learning more about the Macropad, assembly instructions, and how to download custom code into the device: https://learn.adafruit.com/adafruit-macropad-rp2040. 
- The Starter kit can also be purchased from vendors such as Digikey: https://www.digikey.com/en/products/detail/adafruit-industries-llc/5128/14635377
- Adafruit Midi Library: https://docs.circuitpython.org/projects/midi/en/latest/api.html#adafruit_midi.system_exclusive.SystemExclusive.from_bytes
- The Starter kit is an assemble only, and requires no soldering or electronics experience.

The EVM Pad controller embedded in a case with low profile key switches and LED window keycaps:

![EVMPad](resources/AMEVMPad.jpg)

Why use the Macropad RP2040 to control the Ketron: The Macropad has USB HID keyboard drivers - just like the countless keypads you fill find on Amazon. However, these devices and even some dedicated MIDI controllers do not support sending MIDI SysEx messages. Ketron exposes a hardware MIDI pedal interface on the EVM, but also has generously provided a MIDI over USB implmenetation. This controller is coded to send MIDI CC and SysEX messages over USB using the Adafruit Circuit Python library.

### Macropad Controller Button:

The USB based MIDI Controller supports the most often used Arranger functions via SysEx messages. Button assignmeents can be changed by modifying the values in a config file saved on the controller's USB drive.

The controller is currently configured to the following EVM SysEx messages:

Row 1:
- Intro/End 1 (green)
- Intro/End 2 (green)
- Intro/End 3 (green)
- To End (red)

Row 2:
- Arr.A (blue)
- Arr.B (blue)
- Arr.C (blue)
- Arr.D (blue)

Row 3:
- Variation (blue)
- Fill (green)
- Break (orange)
- Start/End (red)

### Macropad Controller Encoder support:

The Encoder switch is coded to cycle through the following functions when pressed. The rotary encode is used to change the values for the selected function.
- Rotor Fast/Slow (blue) - default
- Tempo Up/Down (yellow)
- Volume Up/Down (purple)

Notes:
- The colors mentioned show on the Variation key. When you press Start/Stop, the EVM will start playing and the Variation button turns yellow to indicate that it is in Tempo adjustment mode. The Tempo and Volume modes once activated or pressed is timed to return to the default Rotor Fast/Slow after 60 seconds of no adjustments.
- For Volume to work, you must change the EVM configuration to listen on MIDI channel 16. You can do so by navigating to the EVM MIDI configuration screen, select the receive (RX) option, and then set Global to channel 16. The Controller encoder in Volume mode sends MIDI CC Expression to EVM RX Global channel 16 adjusting the volume of all channels in the EVM - acting similar to the EVM Master Volume knob. Also note that an attached MIDI keyboard/organ can be configured to send expression pedal messages to the EVM synchronizing volume between the devices in the same manner. 

### Connecting the EVM Macropad Controller to your EVM Module:
- The Ketron EVM expects all attached MIDI devices to be powered up before you start it up. It will not detect devices on the USB or MIDI ports that is not switched on or added after EVM power up.
- The Macropad has a single USB port that is used to connect to the EVM, and as a result of the EVM  power up connect requirement, we have to power it via a USB hub that provides external power. This is an example USB Hub that works:  Wenter 5 Ports USB 3.0 Hub (https://www.amazon.com/gp/product/B0BMFDLRSQ/ref=ewc_pr_img_1?smid=ATSSJE5RHO7GG&psc=1). The powered USB hub can also be used to charge a tablet if you use that to wirelessly control the EVM.

### Loading the customized EVM Controller code into the Macropad:
See the Adafruit learning website for detailed instructors on how to
-  Prepare the board for our custom solution in the code.py file in the code directory for this repository.
-  You have the following options:
   - Simply copy the code files from a local disk to the MacroPad USB drive mounted as 'CIRCUITPY'.  
   - Download the Mu Editor to your PC. Mu will connect to the Macropad board and allow you up/download and edit the code.py file. It also has a REPL terminal that can be used to interact with the board during development. 
   - Use your favoratite code editor - Visual Studio Code, Cursor, Notepad++ if you prefer.

### Testing the EVM Macropad Controller:
Before connecting to the EVM moodule, you may want to download and install MidiView (https://hautetechnique.com/midi/midiview/). Midi is useful to inspect and validate the output from any MIDI controller. In this case you should see the controller output the SysEx messages associated with keys or the rotary encoder.

### Customizing the EVM Cntroller button SysEx messages:
Keys are configured by updating the provided keysconfig.txt file. Modifying the mappings requires you to lookup the exact text for the required SysEWx MIDI message from either the Tabs (pedal_midis) or Pedal (tab_midis) lookup tables in the Ketron MIDI documentation, and copy it onto one of the keys of the keys. See the config file for the current configuration. Please be careful with the configuration. It is validating and if an error is enountered during startup, all keys will turn red. The unit continues to function though based on the coded defaults. It is preferred that you keep with the Pedal messages. There are many more Tab messages, and for instance Value Up/Down is very useful, but without context it results in unexpected behaviors in the EVM. Carefully test if you pick a value from Tabs other than VARATION. 
Note: The rotary encoder SysEx output for is fixed to tempo up/down,  rotary fast/slow or volume up/down on successive encoder button presses. It is note configurable at the moment.

#### Extra:
- Please let me know you need a 3D case for your solution
  - The 3D case .scad and .stl files are available in the case directory if you would like to print it yourself. Please note that it consists of three files: The main case, the top cover, and loose fitting filler that goes in between the PCB and the top cover to keep thetop cover flush with the case top.
  - I switched to using low profile key switches and caps you see in the picture. It feels and looks much better. Contact me if I can help.
  - If you are going to print a case and use low profile key switches, then I would recommend you buy the Adafruit Macropad bare bones board only.
  - If you have a need to tinker with the code, and try qwiic add-ons, then print the dev 3D case which has a larger slot that accepts a qwiic connector.

Setup with the Roland AT900C, Ketron EVM, iPad EVM Controller, and the out of the box Macropad RP2040:

![image](https://github.com/user-attachments/assets/b157a384-70e0-4774-a011-49b8d7b529fb)

Original Adafruit Macropad RP2040:

![image](https://github.com/user-attachments/assets/6fd9b969-9b77-4c2a-81fc-0f7a34129f4d)

For more information, support, or a completed unit please email me at a_minnie@hotmail.com.



