# Behringer-X-Touch-Compact-FL-Script
Python controller script for X-Touch compact controller and FL Studio 2024

### Credit:
Ian Walker for his [blog post](https://gadgeteer.home.blog/2021/02/22/using-a-behringer-compact-control-surface-with-fl-studio-in-mackie-control-mode-enhanced/) that got me started
NicoG60 for his [repo](https://github.com/NicoG60/TouchMCU/blob/main/doc/mackie_control_protocol.md) breaking down MCU protocol
ImageLine for the [scripting docs](https://www.image-line.com/fl-studio-learning/fl-studio-online-manual/html/midi_scripting.htm#script_module_ui)
ImageLine for the [API stubs page](https://il-group.github.io/FL-Studio-API-Stubs/midi_controller_scripting/midi/gt%20commands/)



### Remapped buttons:
| Control     | Function              | New Function            |
| :---------- | :-------------------: | :---------------------: |
| Flip        | Invert Pan/Level      | Toggle F5 Playlist      |
| Marker      | Nothing (Shift?)      | Drop Auto Marker        |
| Nudge       | Edison Audiologger    | Jump Between Markers    |
| Cycle       | Toggle Snap Line/None | Pattern/Song loop mode  |

Flip is useful but since selecting a track takes you to mixer with no way to return to playlist, an F5 toggle is preferred.
Marker drop did nothing, it may have been a shift function per the code. Anyway now its mapped correctly.
Nudge opened a new Edison in autorecord mode each time it pressed, pretty useless to me. Jumping between markers is preferred.
Loop only toggled the quantize which isnt helpful with no jog wheel to move anything. 

### To Do:
The last thing I want is for Fader 9 to control the main mixer channel fader, not the main monitor out.
The main mixer fader is motorized  and the monitor control is not.

Right now Ive had come close by adding these two bits, which allow me to move both controls with fader 9, but I dont know how it retains that link to main monitor.
``` python
#Adding these two pieces gets it to control BOTH but not just the master fader

	def OnInit(self):

		self.FirstTrackT[0] = 1
		self.FirstTrack = 0
		self.SmoothSpeed = 469
		self.Clicking = True

		device.setHasMeters()
		self.LastTimeMsg = bytearray(10)

		for m in range (0, len(self.FreeCtrlT)):
			self.FreeCtrlT[m] = 8192 # default free faders to center
		if device.isAssigned():
			device.midiOutSysex(bytes([0xF0, 0x00, 0x00, 0x66, 0x14, 0x0C, 1, 0xF7]))

		self.SetBackLight(2) # backlight timeout to 2 minutes
		self.UpdateClicking()
		self.UpdateMeterMode()

		self.SetPage(self.Page)
		self.OnSendTempMsg('Linked to ' + ui.getProgTitle() + ' (' + ui.getVersion() + ')', 2000);


		# define track numbers for faders, including MAIN
		for x in range(9):
			self.ColT[x].TrackNum = x

        # Catch-all for MAIN fader or unexpected channels
        else:
            event.inEv = event.data1 + (event.data2 << 7)
            event.outEv = (event.inEv << 16) // 16383
            event.inEv -= 0x2000

            # Map to Main mixer channel (Track number 0)
            main_mixer_channel = 0
            event.handled = True
            mixer.automateEvent(mixer.getTrackVolumeEventID(main_mixer_channel), self.AlphaTrack_SliderToLevel(event.inEv + 0x2000), midi.REC_MIDIController, self.SmoothSpeed)
            n = mixer.getAutoSmoothEventValue(mixer.getTrackVolumeEventID(main_mixer_channel))
            s = mixer.getEventIDValueString(mixer.getTrackVolumeEventID(main_mixer_channel), n)
            if s != '':
                s = ': ' + s
            self.OnSendTempMsg('Main Mixer Channel' + s, 500)
