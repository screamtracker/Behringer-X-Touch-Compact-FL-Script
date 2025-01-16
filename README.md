# Behringer-X-Touch-Compact-FL-Script
A Python controller script for the X-Touch Compact controller and FL Studio 2024

### Credits
- Ian Walker : [Blog and Forum posts](https://gadgeteer.home.blog/2021/02/22/using-a-behringer-compact-control-surface-with-fl-studio-in-mackie-control-mode-enhanced/)
- NicoG60    : [MCU protocol Repo](https://github.com/NicoG60/TouchMCU/blob/main/doc/mackie_control_protocol.md)
- ImageLine  : [Scripting docs](https://www.image-line.com/fl-studio-learning/fl-studio-online-manual/html/midi_scripting.htm#script_module_ui)
- ImageLine  : [API stubs page](https://il-group.github.io/FL-Studio-API-Stubs/midi_controller_scripting/midi/gt%20commands/)

---
![x-touch_wip](https://github.com/user-attachments/assets/169045a9-f4e5-4833-8cb1-03e08cb7c459)

---
### Remapped Controls:

| Control         | Function              | New Function            | Hex/MIDI  |
| :-------------- | :-------------------  | :---------------------  | :---------|
| **Flip**        | Invert Pan/Level      | Toggle F5 Playlist      | 0x32      |
| **Marker**      | Nothing (Shift?)      | Drop Auto Marker        | 0x54      |
| **Nudge**       | Edison Audiologger    | Jump Between Markers    | 0x55      |
| **Cycle**       | Toggle Snap Line/None | Pattern/Song loop mode  | 0x56      |
| **Master Fader**| Main Monitor level    | Master Fader            | CH8       |
| **Bank**        | Bank Jump (8)         | Bank Jump (1)           | 0x2E/0x2F |
| **Channel**     | Channel Jump (1)      | Marker Jump and Select  | 0x30/0x31 |

**Flip** is useful but Track Select from the X-Touch takes you to mixer with no way to return to playlist, so an F5 toggle is preferred.

**Marker drop** did nothing (it may have been shift function per the code). Anyway its mapped correctly now.

**Nudge** opened a new Edison in Autorecord mode each time it pressed, pretty useless to me. Jumping between markers is preferred.

**Loop** toggles quantize On/Off which isnt helpful with no jog wheel to move clips around. 

**Master Fader** Who uses main monitor out? :man_facepalming: Master mixer mapped, bonus this fader is motorized :metal:

**Banking** was weird. Jump +8 on first increment then +1 after. Jump back -16 with -1 afterwards :man_facepalming:  
Now it increments by a bank of 1 and you can crank it to track 8 in a quarter turn.

**Channel Select** virtually shifts all faders +/- 1 without decent screen feedback. You get lost, quick. Moreso with the original banking method.  
Now I use it for marker jumps and it selects. 0x30 for back 0x31 for forward.

**Fader touch** now works and selects the touched track in the mixer.

---
### To Do:
Refactor code to remove all non-usable buttons and jog methods **DONE**

Channel is useless to me as well, will remap to global tempo or swing. Mapped to Marker.  **DONE**

Touch Faders. There are controls defined in the scipt, but only for 3 touch faders...? Will see. **DONE**

Now that I have available touch faders and 0x55 I will look at more reassignments. I may reinstate Flip Mode.

Dive into the INST pot and see what I can do, it is a powerful control


