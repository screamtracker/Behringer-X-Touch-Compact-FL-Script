# Behringer-X-Touch-Compact-FL-Script
A Python controller script for the X-Touch Compact controller and FL Studio 2024

### Credits
- Ian Walker : [Blog and Forum posts](https://gadgeteer.home.blog/2021/02/22/using-a-behringer-compact-control-surface-with-fl-studio-in-mackie-control-mode-enhanced/)
- NicoG60    : [MCU protocol Repo](https://github.com/NicoG60/TouchMCU/blob/main/doc/mackie_control_protocol.md)
- ImageLine  : [Scripting docs](https://www.image-line.com/fl-studio-learning/fl-studio-online-manual/html/midi_scripting.htm#script_module_ui)
- ImageLine  : [API stubs page](https://il-group.github.io/FL-Studio-API-Stubs/midi_controller_scripting/midi/gt%20commands/)

---
![x-touch_wip](https://github.com/user-attachments/assets/6d56f999-9b59-4a2d-8e7d-4cceeb7145c5)

---
### Remapped Controls:

| Control         | Function              | New Function            |
| :-------------- | :-------------------  | :---------------------  |
| **Flip**        | Invert Pan/Level      | Toggle F5 Playlist      |
| **Marker**      | Nothing (Shift?)      | Drop Auto Marker        |
| **Nudge**       | Edison Audiologger    | Jump Between Markers    |
| **Cycle**       | Toggle Snap Line/None | Pattern/Song loop mode  |
| **Master Fader**| Main Monitor level    | Master Fader            |

Flip is useful but Track Select from the X-Touch takes you to mixer with no way to return to playlist, so an F5 toggle is preferred.

Marker drop did nothing (it may have been shift function per the code). Anyway its mapped correctly now.

Nudge opened a new Edison in Autorecord mode each time it pressed, pretty useless to me. Jumping between markers is preferred.

Loop only toggled the quantize which isnt helpful with no jog wheel to move anything. 

Who uses main monitor out? :man_facepalming: Master mixer is now mapped and as a bonus this fader is motorized :metal: Monitor was not
