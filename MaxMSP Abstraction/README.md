# Max/MSP Abstraction: br.pitchshift.abs.1.2  

By Brian Riordan  
[guaguanco127@gmail.com](mailto:guaguanco127@gmail.com)  
[brianriordanmusic@gmail.com](mailto:brianriordanmusic@gmail.com)  
[https://www.brianriordanmusic.com/](https://www.brianriordanmusic.com/) 

Repository for br.pitchshift.1.2, with all related files, can be found here: [https://github.com/guaguanco127/br.pitchshift](https://github.com/guaguanco127/br.pitchshift)  
Additional programs can be found here: [https://github.com/guaguanco127/br.max](https://github.com/guaguanco127/br.max)  

Versions 1.1 and 1.2 were updated with Max 9. Version 1.0 was created with Max/MSP 8.5.6. 

## Table of Contents 

[What's New in 1.2](#whats-new-in-12)  
[What's New in 1.1](#whats-new-in-11)  
[About](#About)   
[What is an abstraction?](#Abstraction)  
[How To Install](#Install)  
[How To Use](#Use)  
[State outlet](#State)  
[Example Patch](#Example)  

## What's New in 1.2

- **State outlet** (abstraction only): a new last outlet sends every setting as a named message the moment it changes (`on`, `pitch`, `drywet`, `lowpass`, `highpass`). See [State outlet](https://github.com/guaguanco127/br.pitchshift/tree/main/MaxMSP%20Abstraction#State).
- Every inlet and the L/R outlets are unchanged, so 1.2 swaps in for 1.1 without rewiring.
- **New example patch:** _br.pitchshift.example.1.2 with a demo source, messages into every inlet and a State outlet tab.
- The controls have readable names (On/Off, Pitchshift, Dry/Wet, Lowpass, Highpass), so presets and pattr show them clearly.
- The pfft file and the Max for Live device are unchanged (1.1).

## What's New in 1.1

- **Much lower CPU.** The spectral processing switches itself off completely while the effect is bypassed. Resting CPU dropped to about 1%, and about 3% while shifting.
- **Cleaner highs.** Partials shifted above the top of the audio range are now dropped instead of folding back down as metallic, out-of-tune tones.
- **New Lowpass and Highpass controls** filter the sound going into the pitch shifter (the dry sound is untouched). Trimming noisy highs and rumbling lows before shifting keeps them from turning into artifacts.
- **Self-contained.** Everything it needs is included (the pitch-shifting FFT patch "br.pitchshift.pfft" ships in each folder); it no longer relies on Max's example files.
- **Starts bypassed** when loaded.

## <a name="About"></a>About

This is a spectral Max/MSP abstraction, and Ableton Max for Live device that allows the user to transpose the pitch of a stereo signal up to two octaves and down to two octaves. Good for harmonization and microtonal pitch-shifting. Currently works in any sample rate or bit depth.

This effect introduces a latency of 2048 samples. For a latency-free version of a pitch-shifter (that introduces some artifacts) use [br.whammy](https://github.com/guaguanco127/br.whammy) instead.  

Only works as an abstraction or a device. External objects and RNBO not available yet. An important file is included in each folder called "br.pitchshift.pfft.maxpat". Keep it in the same folder as the abstraction or device -- they will not work without it.

**On/Off:** Turn the effect on or bypass it. The default is bypass.
  
**Pitchshift:** Pitch-shift factor in semitones, -24 to 24. The default is 0. Microtonal pitch-shifting is possible by using numbers in between integers. For example, -0.50 is pitch-shifted down by a quarter tone.   

**Dry/Wet:** The amount of dry and wet signal between 0 and 100. The default is 100. The wet signal is latent by 2048 samples. 

**Lowpass:** Filters the high frequencies out of the sound before it is pitch-shifted, between 500 Hz and 20,000 Hz. The default is 20,000 Hz (fully open). Lower it to keep noisy highs from turning into artifacts, especially when shifting up.

**Highpass:** Filters the low frequencies out of the sound before it is pitch-shifted, between 20 Hz and 1,000 Hz. The default is 20 Hz (fully open). Around 40 Hz removes rumble that would otherwise be shifted up into audible range.

## <a name="Abstraction"></a>What is an Abstraction?

An abstraction is a subpatcher that is saved as an external file, and can be used just like a standard Max object. As long as your abstraction can be found in the Max file path, you can type its name into a new object box and it will be loaded directly into your patch.  

By saving your logic in an abstraction, you can create modules that can be used in future work with little or no additional programming. This allows you to parlay your Max knowledge into more efficient work in the future, and will help you create programming systems that are modular and easier to maintain.

## <a name="Install"></a>How To Install

1. Make sure you have Max 9 installed in your computer. And, make sure you are using a Max patch that is inside of a folder.  

2. Copy and paste br.pitchshift.abs.1.2.maxpat inside of the same folder as the Max patch you are using.      

3. Also, copy and paste the file called br.pitchshift.pfft.maxpat into the same folder. If this file is already there, then there is no reason to copy and paste it. **The abstraction will not work without this file.**

4. In the Max patch you are using, create an object called br.pitchshift.abs.1.2 

5. Alternatively, you could also create this inside of a bpatcher object and use all of the preset UI objects featured inside the abstraction. To do this, create a bpatcher object. Then, go inside of its inspector, select "choose" next to "Patcher File" and select the br.pitchshift.abs.1.2.maxpat located within the same folder as your project. 

## <a name="Use"></a>How To Use

The first two inlets are for the left and the right stereo signals. The first two outlets are the left and right outputs; the third is the State outlet.

Every control has its own inlet. Sending a value to an inlet moves its on-screen control too, so the display always matches the sound. Hover over an inlet in Max to see the same information.

| Inlet | Control | Type | Range | Default |
|---|---|---|---|---|
| 1 | Left audio in | Signal | | |
| 2 | Right audio in | Signal | | |
| 3 | On/Off | Int | 0 = Bypass, 1 = On | 0 |
| 4 | Pitch Shift | Float | -24 - 24 semitones | 0 |
| 5 | Dry/Wet | Float | 0 - 100 % | 100 |
| 6 | Lowpass | Float | 500 - 20000 Hz, before the pitch shift | 20000 |
| 7 | Highpass | Float | 20 - 1000 Hz, before the pitch shift | 20 |

| Outlet | Output | Type |
|---|---|---|
| 1 | Left Out | Signal |
| 2 | Right Out | Signal |
| 3 | State | Messages: `<name> <value>` (see [State outlet](#State)) |

**Updating from 1.1:** 1.2 only adds the State outlet; every inlet and the L/R outlets are unchanged. Replace br.pitchshift.abs.1.1.maxpat with br.pitchshift.abs.1.2.maxpat; br.pitchshift.pfft.maxpat stays the same.

**Upgrading from 1.0:** inlets 1-5 are unchanged, but On/Off now defaults to 0 (bypass). Inlets 6 (Lowpass) and 7 (Highpass) are new.

Double click on the object and you can see inside of the object. This way you can study how it was built. 

## <a name="State"></a>State outlet

The last outlet sends the current settings as named messages the moment they change, for example `pitch 7.`, `on 1`, `drywet 50.`. Clicking a control, numbers into the inlets and preset recalls all show up; repeats are filtered out. Use it to keep a display, Mira or another patch in sync. Pick them out by name with [route on pitch drywet lowpass highpass], not by position, so your patch keeps working if a later version adds controls.

| Name | Control | Values |
|---|---|---|
| on | On/Off | 0 = Bypass, 1 = On |
| pitch | Pitchshift | -24 - 24 semitones |
| drywet | Dry/Wet | 0 - 100 % |
| lowpass | Lowpass | 500 - 20000 Hz |
| highpass | Highpass | 20 - 1000 Hz |

## <a name="Example"></a>Example Patch

Open _br.pitchshift.example.1.2.maxpat (keep it in the same folder as the abstraction and br.pitchshift.pfft.maxpat). Turn on the audio with the toggle, then raise the gain slider, which starts muted.

- **Source:** the demo tone (a saw at 110 Hz on the left and 165 Hz on the right) is on when the patch opens; turn on the mic / line in 1 + 2 toggle to use your own sound.
- **Pitch:** it opens bypassed, so click Pitch on the panel (or the On/Off toggle), then try the pitch messages (-12, -5, 0, 7, 12).
- **Messages:** every inlet has message boxes: Dry/Wet, Lowpass and Highpass.
- **State outlet tab:** the numbers follow every setting as you change it on the panel or with the messages.

## <a name="Credits"></a>Credits

Built around gizmo~ (Cycling '74).
