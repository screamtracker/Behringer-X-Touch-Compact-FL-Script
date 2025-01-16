# Behringer-X-Touch-Compact-FL-Script
A Python controller script for the X-Touch Compact controller and FL Studio 2024

### Credits
- Ian Walker : [Blog and Forum posts](https://gadgeteer.home.blog/2021/02/22/using-a-behringer-compact-control-surface-with-fl-studio-in-mackie-control-mode-enhanced/)
- NicoG60    : [MCU protocol Repo](https://github.com/NicoG60/TouchMCU/blob/main/doc/mackie_control_protocol.md)
- ImageLine  : [Scripting docs](https://www.image-line.com/fl-studio-learning/fl-studio-online-manual/html/midi_scripting.htm#script_module_ui)
- ImageLine  : [API stubs page](https://il-group.github.io/FL-Studio-API-Stubs/midi_controller_scripting/midi/gt%20commands/)

---
![x-touch_wip](https://github.com/user-attachments/assets/06df06fa-7f62-42d9-8c39-e323f2fe6912)

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

Flip is useful but Track Select from the X-Touch takes you to mixer with no way to return to playlist, so an F5 toggle is preferred.

Marker drop did nothing (it may have been shift function per the code). Anyway its mapped correctly now.

Nudge opened a new Edison in Autorecord mode each time it pressed, pretty useless to me. Jumping between markers is preferred.

Loop toggles quantize On/Off which isnt helpful with no jog wheel to move clips around. 

Who uses main monitor out? :man_facepalming: Master mixer mapped, bonus this fader is motorized :metal:

Banking was weird to me, it would jump 8 on your first increment then 1 afterwards. Then jump back 16 with 1 afterwards. :man_facepalming: I was always lost.
Now it increments by 1, a very tiny bank but you can just crank it to get up to higher tracks, I rarely go above 12-16.

---
### To Do:
Refactor code to remove all non-usable buttons and jog methods **DONE**

Channel is useless to me as well, will remap to global tempo or swing.

Dive into the INST pot and see what I can do.

Touch Faders. There are controls defined in the scipt, but only for 3 touch faders...? Will see.
