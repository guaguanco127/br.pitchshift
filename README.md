# Max/MSP Patches, Abstractions, Externals, RNBO, VSTs, and Ableton Max for Live 

## br.pitchshift.1.1


By Brian Riordan  
[guaguanco127@gmail.com](mailto:guaguanco127@gmail.com)  
[brianriordanmusic@gmail.com](mailto:brianriordanmusic@gmail.com)  
[https://www.brianriordanmusic.com/](https://www.brianriordanmusic.com/) 

Repository for br.pitchshift.1.1, with all related files, can be found here: [https://github.com/guaguanco127/br.pitchshift](https://github.com/guaguanco127/br.pitchshift)  
Additional programs can be found here: [https://github.com/guaguanco127/plugins](https://github.com/guaguanco127/plugins)  

Version 1.1 was updated with Max 9. Version 1.0 was created with Max/MSP 8.5.6. 

## Links

[What's New in 1.1](#whats-new-in-11)  
[About](#About)   
[Ableton Max for Live Device](https://github.com/guaguanco127/br.pitchshift/tree/main/Ableton%20Max%20For%20Live) To use inside of Ableton Suite   
[Max/MSP Abstraction](https://github.com/guaguanco127/br.pitchshift/tree/main/MaxMSP%20Abstraction) To use as an abstraction within Max/MSP   

## What's New in 1.1

- **Much lower CPU.** The spectral processing switches itself off completely while the effect is bypassed. Resting CPU dropped to about 1%, and about 3% while shifting.
- **Cleaner highs.** Partials shifted above the top of the audio range are now dropped instead of folding back down as metallic, out-of-tune tones.
- **New Lowpass and Highpass controls** filter the sound going into the pitch shifter (the dry sound is untouched). Trimming noisy highs and rumbling lows before shifting keeps them from turning into artifacts.
- **Self-contained.** Everything it needs is included (the pitch-shifting FFT patch "br.pitchshift.pfft" ships in each folder); it no longer relies on Max's example files.
- **Starts bypassed** when loaded.

## <a name="About"></a>About

This is a spectral Max/MSP abstraction, and Ableton Max for Live device that allows the user to transpose the pitch of a stereo signal up to two octaves and down to two octaves. Good for harmonization and microtonal pitch-shifting. Currently works in any sample rate or bit depth.

This effect introduces a latency of 2048 samples. For a latency-free version of a pitch-shifter (that introduces some artifacts) use [br.whammy.1.0](https://github.com/guaguanco127/br.whammy.1.0) instead.  

Only works as an abstraction or a device. External objects and RNBO not available yet. An important file is included in each folder called "br.pitchshift.pfft.maxpat". Keep it in the same folder as the abstraction or device -- they will not work without it.

**On/Off:** Turn the effect on or bypass it. The default is bypass.
  
**Pitchshift:** Pitch-shift factor in semitones, -24 to 24. The default is 0. Microtonal pitch-shifting is possible by using numbers in between integers. For example, -0.50 is pitch-shifted down by a quarter tone.   

**Dry/Wet:** The amount of dry and wet signal between 0 and 100. The default is 100. The wet signal is latent by 2048 samples. 

**Lowpass:** Filters the high frequencies out of the sound before it is pitch-shifted, between 500 Hz and 20,000 Hz. The default is 20,000 Hz (fully open). Lower it to keep noisy highs from turning into artifacts, especially when shifting up.

**Highpass:** Filters the low frequencies out of the sound before it is pitch-shifted, between 20 Hz and 1,000 Hz. The default is 20 Hz (fully open). Around 40 Hz removes rumble that would otherwise be shifted up into audible range.
