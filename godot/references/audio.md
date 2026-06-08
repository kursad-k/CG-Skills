# Godot - Audio

**Pages:** 67

---

## AudioBusLayout

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiobuslayout.html

**Contents:**
- AudioBusLayout
- Description
- User-contributed notes

Inherits: Resource < RefCounted < Object

Stores information about the audio buses.

Stores position, muting, solo, bypass, effects, effect position, volume, and the connections between buses. See AudioServer for usage.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectAmplify

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectamplify.html

**Contents:**
- AudioEffectAmplify
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds an amplifying audio effect to an audio bus.

Increases or decreases the volume being routed through the audio bus.

float volume_db = 0.0 

void set_volume_db(value: float)

float get_volume_db()

Amount of amplification in decibels. Positive values make the sound louder, negative values make it quieter. Value can range from -80 to 24.

float volume_linear 

void set_volume_linear(value: float)

float get_volume_linear()

Amount of amplification as a linear value.

Note: This member modifies volume_db for convenience. The returned value is equivalent to the result of @GlobalScope.db_to_linear() on volume_db. Setting this member is equivalent to setting volume_db to the result of @GlobalScope.linear_to_db() on a value.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectBandLimitFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectbandlimitfilter.html

**Contents:**
- AudioEffectBandLimitFilter
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectFilter < AudioEffect < Resource < RefCounted < Object

Adds a band limit filter to the audio bus.

Limits the frequencies in a range around the AudioEffectFilter.cutoff_hz and allows frequencies outside of this range to pass.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectBandPassFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectbandpassfilter.html

**Contents:**
- AudioEffectBandPassFilter
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectFilter < AudioEffect < Resource < RefCounted < Object

Adds a band pass filter to the audio bus.

Attenuates the frequencies inside of a range around the AudioEffectFilter.cutoff_hz and cuts frequencies outside of this band.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectCapture

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectcapture.html

**Contents:**
- AudioEffectCapture
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Captures audio from an audio bus in real-time.

AudioEffectCapture is an AudioEffect which copies all audio frames from the attached audio effect bus into its internal ring buffer.

Application code should consume these audio frames from this ring buffer using get_buffer() and process it as needed, for example to capture data from an AudioStreamMicrophone, implement application-defined effects, or to transmit audio over the network. When capturing audio data from a microphone, the format of the samples will be stereo 32-bit floating-point PCM.

Unlike AudioEffectRecord, this effect only returns the raw audio samples instead of encoding them into an AudioStream.

can_get_buffer(frames: int) const

get_buffer(frames: int)

get_buffer_length_frames() const

get_discarded_frames() const

get_frames_available() const

get_pushed_frames() const

float buffer_length = 0.1 

void set_buffer_length(value: float)

float get_buffer_length()

Length of the internal ring buffer, in seconds. Setting the buffer length will have no effect if already initialized.

bool can_get_buffer(frames: int) const 

Returns true if at least frames audio frames are available to read in the internal ring buffer.

void clear_buffer() 

Clears the internal ring buffer.

Note: Calling this during a capture can cause the loss of samples which causes popping in the playback.

PackedVector2Array get_buffer(frames: int) 

Gets the next frames audio samples from the internal ring buffer.

Returns a PackedVector2Array containing exactly frames audio samples if available, or an empty PackedVector2Array if insufficient data was available.

The samples are signed floating-point PCM between -1 and 1. You will have to scale them if you want to use them as 8 or 16-bit integer samples. (v = 0x7fff * samples[0].x)

int get_buffer_length_frames() const 

Returns the total size of the internal ring buffer in frames.

int get_discarded_frames() const 

Returns the number of audio frames discarded from the audio bus due to full buffer.

int get_frames_available() const 

Returns the number of frames available to read using get_buffer().

int get_pushed_frames() const 

Returns the number of audio frames inserted from the audio bus.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectChorus

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectchorus.html

**Contents:**
- AudioEffectChorus
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a chorus audio effect.

Adds a chorus audio effect. The effect applies a filter with voices to duplicate the audio source and manipulate it through the filter.

get_voice_cutoff_hz(voice_idx: int) const

get_voice_delay_ms(voice_idx: int) const

get_voice_depth_ms(voice_idx: int) const

get_voice_level_db(voice_idx: int) const

get_voice_pan(voice_idx: int) const

get_voice_rate_hz(voice_idx: int) const

set_voice_cutoff_hz(voice_idx: int, cutoff_hz: float)

set_voice_delay_ms(voice_idx: int, delay_ms: float)

set_voice_depth_ms(voice_idx: int, depth_ms: float)

set_voice_level_db(voice_idx: int, level_db: float)

set_voice_pan(voice_idx: int, pan: float)

set_voice_rate_hz(voice_idx: int, rate_hz: float)

void set_dry(value: float)

The effect's raw signal.

float voice/1/cutoff_hz = 8000.0 

void set_voice_cutoff_hz(voice_idx: int, cutoff_hz: float)

float get_voice_cutoff_hz(voice_idx: int) const

The voice's cutoff frequency.

float voice/1/delay_ms = 15.0 

void set_voice_delay_ms(voice_idx: int, delay_ms: float)

float get_voice_delay_ms(voice_idx: int) const

The voice's signal delay.

float voice/1/depth_ms = 2.0 

void set_voice_depth_ms(voice_idx: int, depth_ms: float)

float get_voice_depth_ms(voice_idx: int) const

The voice filter's depth.

float voice/1/level_db = 0.0 

void set_voice_level_db(voice_idx: int, level_db: float)

float get_voice_level_db(voice_idx: int) const

float voice/1/pan = -0.5 

void set_voice_pan(voice_idx: int, pan: float)

float get_voice_pan(voice_idx: int) const

The voice's pan level.

float voice/1/rate_hz = 0.8 

void set_voice_rate_hz(voice_idx: int, rate_hz: float)

float get_voice_rate_hz(voice_idx: int) const

The voice's filter rate.

float voice/2/cutoff_hz = 8000.0 

void set_voice_cutoff_hz(voice_idx: int, cutoff_hz: float)

float get_voice_cutoff_hz(voice_idx: int) const

The voice's cutoff frequency.

float voice/2/delay_ms = 20.0 

void set_voice_delay_ms(voice_idx: int, delay_ms: float)

float get_voice_delay_ms(voice_idx: int) const

The voice's signal delay.

float voice/2/depth_ms = 3.0 

void set_voice_depth_ms(voice_idx: int, depth_ms: float)

float get_voice_depth_ms(voice_idx: int) const

The voice filter's depth.

float voice/2/level_db = 0.0 

void set_voice_level_db(voice_idx: int, level_db: float)

float get_voice_level_db(voice_idx: int) const

float voice/2/pan = 0.5 

void set_voice_pan(voice_idx: int, pan: float)

float get_voice_pan(voice_idx: int) const

The voice's pan level.

float voice/2/rate_hz = 1.2 

void set_voice_rate_hz(voice_idx: int, rate_hz: float)

float get_voice_rate_hz(voice_idx: int) const

The voice's filter rate.

float voice/3/cutoff_hz 

void set_voice_cutoff_hz(voice_idx: int, cutoff_hz: float)

float get_voice_cutoff_hz(voice_idx: int) const

The voice's cutoff frequency.

float voice/3/delay_ms 

void set_voice_delay_ms(voice_idx: int, delay_ms: float)

float get_voice_delay_ms(voice_idx: int) const

The voice's signal delay.

float voice/3/depth_ms 

void set_voice_depth_ms(voice_idx: int, depth_ms: float)

float get_voice_depth_ms(voice_idx: int) const

The voice filter's depth.

float voice/3/level_db 

void set_voice_level_db(voice_idx: int, level_db: float)

float get_voice_level_db(voice_idx: int) const

void set_voice_pan(voice_idx: int, pan: float)

float get_voice_pan(voice_idx: int) const

The voice's pan level.

float voice/3/rate_hz 

void set_voice_rate_hz(voice_idx: int, rate_hz: float)

float get_voice_rate_hz(voice_idx: int) const

The voice's filter rate.

float voice/4/cutoff_hz 

void set_voice_cutoff_hz(voice_idx: int, cutoff_hz: float)

float get_voice_cutoff_hz(voice_idx: int) const

The voice's cutoff frequency.

float voice/4/delay_ms 

void set_voice_delay_ms(voice_idx: int, delay_ms: float)

float get_voice_delay_ms(voice_idx: int) const

The voice's signal delay.

float voice/4/depth_ms 

void set_voice_depth_ms(voice_idx: int, depth_ms: float)

float get_voice_depth_ms(voice_idx: int) const

The voice filter's depth.

float voice/4/level_db 

void set_voice_level_db(voice_idx: int, level_db: float)

float get_voice_level_db(voice_idx: int) const

void set_voice_pan(voice_idx: int, pan: float)

float get_voice_pan(voice_idx: int) const

The voice's pan level.

float voice/4/rate_hz 

void set_voice_rate_hz(voice_idx: int, rate_hz: float)

float get_voice_rate_hz(voice_idx: int) const

The voice's filter rate.

int voice_count = 2 

void set_voice_count(value: int)

int get_voice_count()

The number of voices in the effect.

void set_wet(value: float)

The effect's processed signal.

float get_voice_cutoff_hz(voice_idx: int) const 

There is currently no description for this method. Please help us by contributing one!

float get_voice_delay_ms(voice_idx: int) const 

There is currently no description for this method. Please help us by contributing one!

float get_voice_depth_ms(voice_idx: int) const 

There is currently no description for this method. Please help us by contributing one!

float get_voice_level_db(voice_idx: int) const 

There is currently no description for this method. Please help us by contributing one!

float get_voice_pan(voice_idx: int) const 

There is currently no description for this method. Please help us by contributing one!

float get_voice_rate_hz(voice_idx: int) const 

There is currently no description for this method. Please help us by contributing one!

void set_voice_cutoff_hz(voice_idx: int, cutoff_hz: float) 

There is currently no description for this method. Please help us by contributing one!

void set_voice_delay_ms(voice_idx: int, delay_ms: float) 

There is currently no description for this method. Please help us by contributing one!

void set_voice_depth_ms(voice_idx: int, depth_ms: float) 

There is currently no description for this method. Please help us by contributing one!

void set_voice_level_db(voice_idx: int, level_db: float) 

There is currently no description for this method. Please help us by contributing one!

void set_voice_pan(voice_idx: int, pan: float) 

There is currently no description for this method. Please help us by contributing one!

void set_voice_rate_hz(voice_idx: int, rate_hz: float) 

There is currently no description for this method. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectCompressor

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectcompressor.html

**Contents:**
- AudioEffectCompressor
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a compressor audio effect to an audio bus.

Reduces sounds that exceed a certain threshold level, smooths out the dynamics and increases the overall volume.

Dynamic range compressor reduces the level of the sound when the amplitude goes over a certain threshold in Decibels. One of the main uses of a compressor is to increase the dynamic range by clipping as little as possible (when sound goes over 0dB).

Compressor has many uses in the mix:

In the Master bus to compress the whole output (although an AudioEffectHardLimiter is probably better).

In voice channels to ensure they sound as balanced as possible.

Sidechained. This can reduce the sound level sidechained with another audio bus for threshold detection. This technique is common in video game mixing to the level of music and SFX while voices are being heard.

Accentuates transients by using a wider attack, making effects sound more punchy.

float attack_us = 20.0 

void set_attack_us(value: float)

float get_attack_us()

Compressor's reaction time when the signal exceeds the threshold, in microseconds. Value can range from 20 to 2000.

void set_gain(value: float)

Gain applied to the output signal.

void set_mix(value: float)

Balance between original signal and effect signal. Value can range from 0 (totally dry) to 1 (totally wet).

void set_ratio(value: float)

Amount of compression applied to the audio once it passes the threshold level. The higher the ratio, the more the loud parts of the audio will be compressed. Value can range from 1 to 48.

float release_ms = 250.0 

void set_release_ms(value: float)

float get_release_ms()

Compressor's delay time to stop reducing the signal after the signal level falls below the threshold, in milliseconds. Value can range from 20 to 2000.

StringName sidechain = &"" 

void set_sidechain(value: StringName)

StringName get_sidechain()

Reduce the sound level using another audio bus for threshold detection.

float threshold = 0.0 

void set_threshold(value: float)

float get_threshold()

The level above which compression is applied to the audio. Value can range from -60 to 0.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectDelay

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectdelay.html

**Contents:**
- AudioEffectDelay
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a delay audio effect to an audio bus. Plays input signal back after a period of time.

Two tap delay and feedback options.

Plays input signal back after a period of time. The delayed signal may be played back multiple times to create the sound of a repeating, decaying echo. Delay effects range from a subtle echo effect to a pronounced blending of previous sounds with new sounds.

void set_dry(value: float)

Output percent of original sound. At 0, only delayed sounds are output. Value can range from 0 to 1.

bool feedback_active = false 

void set_feedback_active(value: bool)

bool is_feedback_active()

If true, feedback is enabled.

float feedback_delay_ms = 340.0 

void set_feedback_delay_ms(value: float)

float get_feedback_delay_ms()

Feedback delay time in milliseconds.

float feedback_level_db = -6.0 

void set_feedback_level_db(value: float)

float get_feedback_level_db()

Sound level for feedback.

float feedback_lowpass = 16000.0 

void set_feedback_lowpass(value: float)

float get_feedback_lowpass()

Low-pass filter for feedback, in Hz. Frequencies below this value are filtered out of the source signal.

bool tap1_active = true 

void set_tap1_active(value: bool)

bool is_tap1_active()

If true, the first tap will be enabled.

float tap1_delay_ms = 250.0 

void set_tap1_delay_ms(value: float)

float get_tap1_delay_ms()

First tap delay time in milliseconds.

float tap1_level_db = -6.0 

void set_tap1_level_db(value: float)

float get_tap1_level_db()

Sound level for the first tap.

float tap1_pan = 0.2 

void set_tap1_pan(value: float)

Pan position for the first tap. Value can range from -1 (fully left) to 1 (fully right).

bool tap2_active = true 

void set_tap2_active(value: bool)

bool is_tap2_active()

If true, the second tap will be enabled.

float tap2_delay_ms = 500.0 

void set_tap2_delay_ms(value: float)

float get_tap2_delay_ms()

Second tap delay time in milliseconds.

float tap2_level_db = -12.0 

void set_tap2_level_db(value: float)

float get_tap2_level_db()

Sound level for the second tap.

float tap2_pan = -0.4 

void set_tap2_pan(value: float)

Pan position for the second tap. Value can range from -1 (fully left) to 1 (fully right).

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectDistortion

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectdistortion.html

**Contents:**
- AudioEffectDistortion
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a distortion audio effect to an Audio bus.

Modifies the sound to make it distorted.

Different types are available: clip, tan, lo-fi (bit crushing), overdrive, or waveshape.

By distorting the waveform the frequency content changes, which will often make the sound "crunchy" or "abrasive". For games, it can simulate sound coming from some saturated device or speaker very efficiently.

Digital distortion effect which cuts off peaks at the top and bottom of the waveform.

There is currently no description for this enum. Please help us by contributing one!

Low-resolution digital distortion effect (bit depth reduction). You can use it to emulate the sound of early digital audio devices.

Mode MODE_OVERDRIVE = 3

Emulates the warm distortion produced by a field effect transistor, which is commonly used in solid-state musical instrument amplifiers. The drive property has no effect in this mode.

Mode MODE_WAVESHAPE = 4

Waveshaper distortions are used mainly by electronic musicians to achieve an extra-abrasive sound.

void set_drive(value: float)

Distortion power. Value can range from 0 to 1.

float keep_hf_hz = 16000.0 

void set_keep_hf_hz(value: float)

float get_keep_hf_hz()

High-pass filter, in Hz. Frequencies higher than this value will not be affected by the distortion. Value can range from 1 to 20000.

void set_mode(value: Mode)

float post_gain = 0.0 

void set_post_gain(value: float)

float get_post_gain()

Increases or decreases the volume after the effect, in decibels. Value can range from -80 to 24.

float pre_gain = 0.0 

void set_pre_gain(value: float)

Increases or decreases the volume before the effect, in decibels. Value can range from -60 to 60.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectEQ10

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffecteq10.html

**Contents:**
- AudioEffectEQ10
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectEQ < AudioEffect < Resource < RefCounted < Object

Adds a 10-band equalizer audio effect to an Audio bus. Gives you control over frequencies from 31 Hz to 16000 Hz.

Each frequency can be modulated between -60/+24 dB.

See also AudioEffectEQ, AudioEffectEQ6, AudioEffectEQ21.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectEQ21

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffecteq21.html

**Contents:**
- AudioEffectEQ21
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectEQ < AudioEffect < Resource < RefCounted < Object

Adds a 21-band equalizer audio effect to an Audio bus. Gives you control over frequencies from 22 Hz to 22000 Hz.

Each frequency can be modulated between -60/+24 dB.

See also AudioEffectEQ, AudioEffectEQ6, AudioEffectEQ10.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectEQ6

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffecteq6.html

**Contents:**
- AudioEffectEQ6
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectEQ < AudioEffect < Resource < RefCounted < Object

Adds a 6-band equalizer audio effect to an audio bus. Gives you control over frequencies from 32 Hz to 10000 Hz.

Each frequency can be modulated between -60/+24 dB.

See also AudioEffectEQ, AudioEffectEQ10, AudioEffectEQ21.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectEQ

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffecteq.html

**Contents:**
- AudioEffectEQ
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Inherited By: AudioEffectEQ10, AudioEffectEQ21, AudioEffectEQ6

Base class for audio equalizers. Gives you control over frequencies.

Use it to create a custom equalizer if AudioEffectEQ6, AudioEffectEQ10 or AudioEffectEQ21 don't fit your needs.

AudioEffectEQ gives you control over frequencies. Use it to compensate for existing deficiencies in audio. AudioEffectEQs are useful on the Master bus to completely master a mix and give it more character. They are also useful when a game is run on a mobile device, to adjust the mix to that kind of speakers (it can be added but disabled when headphones are plugged).

get_band_count() const

get_band_gain_db(band_idx: int) const

set_band_gain_db(band_idx: int, volume_db: float)

int get_band_count() const 

Returns the number of bands of the equalizer.

float get_band_gain_db(band_idx: int) const 

Returns the band's gain at the specified index, in dB.

void set_band_gain_db(band_idx: int, volume_db: float) 

Sets band's gain at the specified index, in dB.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectfilter.html

**Contents:**
- AudioEffectFilter
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Inherited By: AudioEffectBandLimitFilter, AudioEffectBandPassFilter, AudioEffectHighPassFilter, AudioEffectHighShelfFilter, AudioEffectLowPassFilter, AudioEffectLowShelfFilter, AudioEffectNotchFilter

Adds a filter to the audio bus.

Allows frequencies other than the cutoff_hz to pass.

FilterDB FILTER_6DB = 0

Cutting off at 6dB per octave.

FilterDB FILTER_12DB = 1

Cutting off at 12dB per octave.

FilterDB FILTER_18DB = 2

Cutting off at 18dB per octave.

FilterDB FILTER_24DB = 3

Cutting off at 24dB per octave.

float cutoff_hz = 2000.0 

void set_cutoff(value: float)

Threshold frequency for the filter, in Hz.

void set_db(value: FilterDB)

Steepness of the cutoff curve in dB per octave, also known as the order of the filter. Higher orders have a more aggressive cutoff.

void set_gain(value: float)

Gain amount of the frequencies after the filter.

float resonance = 0.5 

void set_resonance(value: float)

float get_resonance()

Amount of boost in the frequency range near the cutoff frequency.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectHardLimiter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffecthardlimiter.html

**Contents:**
- AudioEffectHardLimiter
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a hard limiter audio effect to an Audio bus.

A limiter is an effect designed to disallow sound from going over a given dB threshold. Hard limiters predict volume peaks, and will smoothly apply gain reduction when a peak crosses the ceiling threshold to prevent clipping and distortion. It preserves the waveform and prevents it from crossing the ceiling threshold. Adding one in the Master bus is recommended as a safety measure to prevent sudden volume peaks from occurring, and to prevent distortion caused by clipping.

float ceiling_db = -0.3 

void set_ceiling_db(value: float)

float get_ceiling_db()

The waveform's maximum allowed value, in decibels. This value can range from -24.0 to 0.0.

The default value of -0.3 prevents potential inter-sample peaks (ISP) from crossing over 0 dB, which can cause slight distortion on some older hardware.

float pre_gain_db = 0.0 

void set_pre_gain_db(value: float)

float get_pre_gain_db()

Gain to apply before limiting, in decibels.

float release = 0.1 

void set_release(value: float)

Time it takes in seconds for the gain reduction to fully release.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectHighPassFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffecthighpassfilter.html

**Contents:**
- AudioEffectHighPassFilter
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectFilter < AudioEffect < Resource < RefCounted < Object

Adds a high-pass filter to the audio bus.

Cuts frequencies lower than the AudioEffectFilter.cutoff_hz and allows higher frequencies to pass.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectHighShelfFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffecthighshelffilter.html

**Contents:**
- AudioEffectHighShelfFilter
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectFilter < AudioEffect < Resource < RefCounted < Object

Adds a high-shelf filter to the audio bus.

Reduces all frequencies above the AudioEffectFilter.cutoff_hz.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectInstance

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectinstance.html

**Contents:**
- AudioEffectInstance
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: AudioEffectSpectrumAnalyzerInstance

Manipulates the audio it receives for a given effect.

An audio effect instance manipulates the audio it receives for a given effect. This instance is automatically created by an AudioEffect when it is added to a bus, and should usually not be created directly. If necessary, it can be fetched at run-time with AudioServer.get_bus_effect_instance().

_process(src_buffer: const void*, dst_buffer: AudioFrame*, frame_count: int) virtual required

_process_silence() virtual const

void _process(src_buffer: const void*, dst_buffer: AudioFrame*, frame_count: int) virtual required 

Called by the AudioServer to process this effect. When _process_silence() is not overridden or it returns false, this method is called only when the bus is active.

Note: It is not useful to override this method in GDScript or C#. Only GDExtension can take advantage of it.

bool _process_silence() virtual const 

Override this method to customize the processing behavior of this effect instance.

Should return true to force the AudioServer to always call _process(), even if the bus has been muted or cannot otherwise be heard.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectLimiter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectlimiter.html

**Contents:**
- AudioEffectLimiter
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Deprecated: Use AudioEffectHardLimiter instead.

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a soft-clip limiter audio effect to an Audio bus.

A limiter is similar to a compressor, but it's less flexible and designed to disallow sound going over a given dB threshold. Adding one in the Master bus is always recommended to reduce the effects of clipping.

Soft clipping starts to reduce the peaks a little below the threshold level and progressively increases its effect as the input level increases such that the threshold is never exceeded.

float ceiling_db = -0.1 

void set_ceiling_db(value: float)

float get_ceiling_db()

The waveform's maximum allowed value, in decibels. Value can range from -20 to -0.1.

float soft_clip_db = 2.0 

void set_soft_clip_db(value: float)

float get_soft_clip_db()

Applies a gain to the limited waves, in decibels. Value can range from 0 to 6.

float soft_clip_ratio = 10.0 

void set_soft_clip_ratio(value: float)

float get_soft_clip_ratio()

There is currently no description for this property. Please help us by contributing one!

float threshold_db = 0.0 

void set_threshold_db(value: float)

float get_threshold_db()

Threshold from which the limiter begins to be active, in decibels. Value can range from -30 to 0.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectLowPassFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectlowpassfilter.html

**Contents:**
- AudioEffectLowPassFilter
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectFilter < AudioEffect < Resource < RefCounted < Object

Adds a low-pass filter to the audio bus.

Cuts frequencies higher than the AudioEffectFilter.cutoff_hz and allows lower frequencies to pass.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectLowShelfFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectlowshelffilter.html

**Contents:**
- AudioEffectLowShelfFilter
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectFilter < AudioEffect < Resource < RefCounted < Object

Adds a low-shelf filter to the audio bus.

Reduces all frequencies below the AudioEffectFilter.cutoff_hz.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectNotchFilter

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectnotchfilter.html

**Contents:**
- AudioEffectNotchFilter
- Description
- Tutorials
- User-contributed notes

Inherits: AudioEffectFilter < AudioEffect < Resource < RefCounted < Object

Adds a notch filter to the Audio bus.

Attenuates frequencies in a narrow band around the AudioEffectFilter.cutoff_hz and cuts frequencies outside of this range.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectPanner

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectpanner.html

**Contents:**
- AudioEffectPanner
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a panner audio effect to an audio bus. Pans sound left or right.

Determines how much of an audio signal is sent to the left and right buses.

void set_pan(value: float)

Pan position. Value can range from -1 (fully left) to 1 (fully right).

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectPhaser

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectphaser.html

**Contents:**
- AudioEffectPhaser
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a phaser audio effect to an audio bus.

Combines the original signal with a copy that is slightly out of phase with the original.

Combines phase-shifted signals with the original signal. The movement of the phase-shifted signals is controlled using a low-frequency oscillator.

void set_depth(value: float)

Determines how high the filter frequencies sweep. Low value will primarily affect bass frequencies. High value can sweep high into the treble. Value can range from 0.1 to 4.0.

float feedback = 0.7 

void set_feedback(value: float)

Output percent of modified sound. Value can range from 0.1 to 0.9.

float range_max_hz = 1600.0 

void set_range_max_hz(value: float)

float get_range_max_hz()

Determines the maximum frequency affected by the LFO modulations, in Hz. Value can range from 10 to 10000.

float range_min_hz = 440.0 

void set_range_min_hz(value: float)

float get_range_min_hz()

Determines the minimum frequency affected by the LFO modulations, in Hz. Value can range from 10 to 10000.

float rate_hz = 0.5 

void set_rate_hz(value: float)

Adjusts the rate in Hz at which the effect sweeps up and down across the frequency range.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectPitchShift

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectpitchshift.html

**Contents:**
- AudioEffectPitchShift
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a pitch-shifting audio effect to an audio bus.

Raises or lowers the pitch of original sound.

Allows modulation of pitch independently of tempo. All frequencies can be increased/decreased with minimal effect on transients.

FFTSize FFT_SIZE_256 = 0

Use a buffer of 256 samples for the Fast Fourier transform. Lowest latency, but least stable over time.

FFTSize FFT_SIZE_512 = 1

Use a buffer of 512 samples for the Fast Fourier transform. Low latency, but less stable over time.

FFTSize FFT_SIZE_1024 = 2

Use a buffer of 1024 samples for the Fast Fourier transform. This is a compromise between latency and stability over time.

FFTSize FFT_SIZE_2048 = 3

Use a buffer of 2048 samples for the Fast Fourier transform. High latency, but stable over time.

FFTSize FFT_SIZE_4096 = 4

Use a buffer of 4096 samples for the Fast Fourier transform. Highest latency, but most stable over time.

FFTSize FFT_SIZE_MAX = 5

Represents the size of the FFTSize enum.

FFTSize fft_size = 3 

void set_fft_size(value: FFTSize)

FFTSize get_fft_size()

The size of the Fast Fourier transform buffer. Higher values smooth out the effect over time, but have greater latency. The effects of this higher latency are especially noticeable on sounds that have sudden amplitude changes.

int oversampling = 4 

void set_oversampling(value: int)

int get_oversampling()

The oversampling factor to use. Higher values result in better quality, but are more demanding on the CPU and may cause audio cracking if the CPU can't keep up.

float pitch_scale = 1.0 

void set_pitch_scale(value: float)

float get_pitch_scale()

The pitch scale to use. 1.0 is the default pitch and plays sounds unaffected. pitch_scale can range from 0.0 (infinitely low pitch, inaudible) to 16 (16 times higher than the initial pitch).

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectRecord

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectrecord.html

**Contents:**
- AudioEffectRecord
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Audio effect used for recording the sound from an audio bus.

Allows the user to record the sound from an audio bus into an AudioStreamWAV. When used on the "Master" audio bus, this includes all audio output by Godot.

Unlike AudioEffectCapture, this effect encodes the recording with the given format (8-bit, 16-bit, or compressed) instead of giving access to the raw audio samples.

Can be used (with an AudioStreamMicrophone) to record from a microphone.

Note: ProjectSettings.audio/driver/enable_input must be true for audio input to work. See also that setting's description for caveats related to permissions and operating system privacy settings.

Recording with microphone

Audio Microphone Record Demo

get_recording() const

is_recording_active() const

set_recording_active(record: bool)

void set_format(value: Format)

Specifies the format in which the sample will be recorded.

AudioStreamWAV get_recording() const 

Returns the recorded sample.

bool is_recording_active() const 

Returns whether the recording is active or not.

void set_recording_active(record: bool) 

If true, the sound will be recorded. Note that restarting the recording will remove the previously recorded sample.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectReverb

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectreverb.html

**Contents:**
- AudioEffectReverb
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Adds a reverberation audio effect to an Audio bus.

Simulates the sound of acoustic environments such as rooms, concert halls, caverns, or an open spaces.

Third Person Shooter (TPS) Demo

float damping = 0.5 

void set_damping(value: float)

Defines how reflective the imaginary room's walls are. Value can range from 0 to 1.

void set_dry(value: float)

Output percent of original sound. At 0, only modified sound is outputted. Value can range from 0 to 1.

void set_hpf(value: float)

High-pass filter passes signals with a frequency higher than a certain cutoff frequency and attenuates signals with frequencies lower than the cutoff frequency. Value can range from 0 to 1.

float predelay_feedback = 0.4 

void set_predelay_feedback(value: float)

float get_predelay_feedback()

Output percent of predelay. Value can range from 0 to 1.

float predelay_msec = 150.0 

void set_predelay_msec(value: float)

float get_predelay_msec()

Time between the original signal and the early reflections of the reverb signal, in milliseconds.

float room_size = 0.8 

void set_room_size(value: float)

float get_room_size()

Dimensions of simulated room. Bigger means more echoes. Value can range from 0 to 1.

void set_spread(value: float)

Widens or narrows the stereo image of the reverb tail. 1 means fully widens. Value can range from 0 to 1.

void set_wet(value: float)

Output percent of modified sound. At 0, only original sound is outputted. Value can range from 0 to 1.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectSpectrumAnalyzerInstance

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectspectrumanalyzerinstance.html

**Contents:**
- AudioEffectSpectrumAnalyzerInstance
- Description
- Tutorials
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: AudioEffectInstance < RefCounted < Object

Queryable instance of an AudioEffectSpectrumAnalyzer.

The runtime part of an AudioEffectSpectrumAnalyzer, which can be used to query the magnitude of a frequency range on its host bus.

An instance of this class can be obtained with AudioServer.get_bus_effect_instance().

Audio Spectrum Visualizer Demo

get_magnitude_for_frequency_range(from_hz: float, to_hz: float, mode: MagnitudeMode = 1) const

enum MagnitudeMode: 

MagnitudeMode MAGNITUDE_AVERAGE = 0

Use the average value across the frequency range as magnitude.

MagnitudeMode MAGNITUDE_MAX = 1

Use the maximum value of the frequency range as magnitude.

Vector2 get_magnitude_for_frequency_range(from_hz: float, to_hz: float, mode: MagnitudeMode = 1) const 

Returns the magnitude of the frequencies from from_hz to to_hz in linear energy as a Vector2. The x component of the return value represents the left stereo channel, and y represents the right channel.

mode determines how the frequency range will be processed.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectSpectrumAnalyzer

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectspectrumanalyzer.html

**Contents:**
- AudioEffectSpectrumAnalyzer
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

Audio effect that can be used for real-time audio visualizations.

This audio effect does not affect sound output, but can be used for real-time audio visualizations.

This resource configures an AudioEffectSpectrumAnalyzerInstance, which performs the actual analysis at runtime. An instance can be obtained with AudioServer.get_bus_effect_instance().

See also AudioStreamGenerator for procedurally generating sounds.

Audio Spectrum Visualizer Demo

FFTSize FFT_SIZE_256 = 0

Use a buffer of 256 samples for the Fast Fourier transform. Lowest latency, but least stable over time.

FFTSize FFT_SIZE_512 = 1

Use a buffer of 512 samples for the Fast Fourier transform. Low latency, but less stable over time.

FFTSize FFT_SIZE_1024 = 2

Use a buffer of 1024 samples for the Fast Fourier transform. This is a compromise between latency and stability over time.

FFTSize FFT_SIZE_2048 = 3

Use a buffer of 2048 samples for the Fast Fourier transform. High latency, but stable over time.

FFTSize FFT_SIZE_4096 = 4

Use a buffer of 4096 samples for the Fast Fourier transform. Highest latency, but most stable over time.

FFTSize FFT_SIZE_MAX = 5

Represents the size of the FFTSize enum.

float buffer_length = 2.0 

void set_buffer_length(value: float)

float get_buffer_length()

The length of the buffer to keep (in seconds). Higher values keep data around for longer, but require more memory.

FFTSize fft_size = 2 

void set_fft_size(value: FFTSize)

FFTSize get_fft_size()

The size of the Fast Fourier transform buffer. Higher values smooth out the spectrum analysis over time, but have greater latency. The effects of this higher latency are especially noticeable with sudden amplitude changes.

float tap_back_pos = 0.01 

void set_tap_back_pos(value: float)

float get_tap_back_pos()

There is currently no description for this property. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffectStereoEnhance

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffectstereoenhance.html

**Contents:**
- AudioEffectStereoEnhance
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioEffect < Resource < RefCounted < Object

An audio effect that can be used to adjust the intensity of stereo panning.

An audio effect that can be used to adjust the intensity of stereo panning.

float pan_pullout = 1.0 

void set_pan_pullout(value: float)

float get_pan_pullout()

Amplifies the difference between stereo channels, increasing or decreasing existing panning. A value of 0.0 will downmix stereo to mono. Does not affect a mono signal.

float surround = 0.0 

void set_surround(value: float)

Widens sound stage through phase shifting in conjunction with time_pullout_ms. Just pans sound to the left channel if time_pullout_ms is 0.

float time_pullout_ms = 0.0 

void set_time_pullout(value: float)

float get_time_pullout()

Widens sound stage through phase shifting in conjunction with surround. Just delays the right channel if surround is 0.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioEffect

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioeffect.html

**Contents:**
- AudioEffect
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: AudioEffectAmplify, AudioEffectCapture, AudioEffectChorus, AudioEffectCompressor, AudioEffectDelay, AudioEffectDistortion, AudioEffectEQ, AudioEffectFilter, AudioEffectHardLimiter, AudioEffectLimiter, AudioEffectPanner, AudioEffectPhaser, AudioEffectPitchShift, AudioEffectRecord, AudioEffectReverb, AudioEffectSpectrumAnalyzer, AudioEffectStereoEnhance

Base class for audio effect resources.

The base Resource for every audio effect. In the editor, an audio effect can be added to the current bus layout through the Audio panel. At run-time, it is also possible to manipulate audio effects through AudioServer.add_bus_effect(), AudioServer.remove_bus_effect(), and AudioServer.get_bus_effect().

When applied on a bus, an audio effect creates a corresponding AudioEffectInstance. The instance is directly responsible for manipulating the sound, based on the original audio effect's properties.

Audio Microphone Record Demo

_instantiate() virtual required

AudioEffectInstance _instantiate() virtual required 

Override this method to customize the AudioEffectInstance created when this effect is applied on a bus in the editor's Audio panel, or through AudioServer.add_bus_effect().

Note: It is recommended to keep a reference to the original AudioEffect in the new instance. Depending on the implementation this allows the effect instance to listen for changes at run-time and be modified accordingly.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends AudioEffect

@export var strength = 4.0

func _instantiate():
    var effect = CustomAudioEffectInstance.new()
    effect.base = self

    return effect
```

---

## AudioSamplePlayback

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiosampleplayback.html

**Contents:**
- AudioSamplePlayback
- Description
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: RefCounted < Object

Meta class for playing back audio samples.

Meta class for playing back audio samples.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioSample

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiosample.html

**Contents:**
- AudioSample
- Description
- User-contributed notes

Experimental: This class may be changed or removed in future versions.

Inherits: RefCounted < Object

Base class for audio samples.

Base class for audio samples.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioServer

**URL:** https://docs.godotengine.org/en/stable/classes/class_audioserver.html

**Contents:**
- AudioServer
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Server interface for low-level audio access.

AudioServer is a low-level server interface for audio access. It is in charge of creating sample data (playable audio) as well as its playback via a voice interface.

Audio Device Changer Demo

Audio Microphone Record Demo

Audio Spectrum Visualizer Demo

add_bus(at_position: int = -1)

add_bus_effect(bus_idx: int, effect: AudioEffect, at_position: int = -1)

generate_bus_layout() const

get_bus_channels(bus_idx: int) const

get_bus_effect(bus_idx: int, effect_idx: int)

get_bus_effect_count(bus_idx: int)

get_bus_effect_instance(bus_idx: int, effect_idx: int, channel: int = 0)

get_bus_index(bus_name: StringName) const

get_bus_name(bus_idx: int) const

get_bus_peak_volume_left_db(bus_idx: int, channel: int) const

get_bus_peak_volume_right_db(bus_idx: int, channel: int) const

get_bus_send(bus_idx: int) const

get_bus_volume_db(bus_idx: int) const

get_bus_volume_linear(bus_idx: int) const

get_driver_name() const

get_input_device_list()

get_input_mix_rate() const

get_output_device_list()

get_output_latency() const

get_speaker_mode() const

get_time_since_last_mix() const

get_time_to_next_mix() const

is_bus_bypassing_effects(bus_idx: int) const

is_bus_effect_enabled(bus_idx: int, effect_idx: int) const

is_bus_mute(bus_idx: int) const

is_bus_solo(bus_idx: int) const

is_stream_registered_as_sample(stream: AudioStream)

move_bus(index: int, to_index: int)

register_stream_as_sample(stream: AudioStream)

remove_bus(index: int)

remove_bus_effect(bus_idx: int, effect_idx: int)

set_bus_bypass_effects(bus_idx: int, enable: bool)

set_bus_effect_enabled(bus_idx: int, effect_idx: int, enabled: bool)

set_bus_layout(bus_layout: AudioBusLayout)

set_bus_mute(bus_idx: int, enable: bool)

set_bus_name(bus_idx: int, name: String)

set_bus_send(bus_idx: int, send: StringName)

set_bus_solo(bus_idx: int, enable: bool)

set_bus_volume_db(bus_idx: int, volume_db: float)

set_bus_volume_linear(bus_idx: int, volume_linear: float)

set_enable_tagging_used_audio_streams(enable: bool)

swap_bus_effects(bus_idx: int, effect_idx: int, by_effect_idx: int)

bus_layout_changed() 

Emitted when an audio bus is added, deleted, or moved.

bus_renamed(bus_index: int, old_name: StringName, new_name: StringName) 

Emitted when the audio bus at bus_index is renamed from old_name to new_name.

SpeakerMode SPEAKER_MODE_STEREO = 0

Two or fewer speakers were detected.

SpeakerMode SPEAKER_SURROUND_31 = 1

A 3.1 channel surround setup was detected.

SpeakerMode SPEAKER_SURROUND_51 = 2

A 5.1 channel surround setup was detected.

SpeakerMode SPEAKER_SURROUND_71 = 3

A 7.1 channel surround setup was detected.

PlaybackType PLAYBACK_TYPE_DEFAULT = 0

Experimental: This constant may be changed or removed in future versions.

The playback will be considered of the type declared at ProjectSettings.audio/general/default_playback_type.

PlaybackType PLAYBACK_TYPE_STREAM = 1

Experimental: This constant may be changed or removed in future versions.

Force the playback to be considered as a stream.

PlaybackType PLAYBACK_TYPE_SAMPLE = 2

Experimental: This constant may be changed or removed in future versions.

Force the playback to be considered as a sample. This can provide lower latency and more stable playback (with less risk of audio crackling), at the cost of having less flexibility.

Note: Only currently supported on the web platform.

Note: AudioEffects are not supported when playback is considered as a sample.

PlaybackType PLAYBACK_TYPE_MAX = 3

Experimental: This constant may be changed or removed in future versions.

Represents the size of the PlaybackType enum.

void set_bus_count(value: int)

Number of available audio buses.

String input_device = "Default" 

void set_input_device(value: String)

String get_input_device()

Name of the current device for audio input (see get_input_device_list()). On systems with multiple audio inputs (such as analog, USB and HDMI audio), this can be used to select the audio input device. The value "Default" will record audio on the system-wide default audio input. If an invalid device name is set, the value will be reverted back to "Default".

Note: ProjectSettings.audio/driver/enable_input must be true for audio input to work. See also that setting's description for caveats related to permissions and operating system privacy settings.

String output_device = "Default" 

void set_output_device(value: String)

String get_output_device()

Name of the current device for audio output (see get_output_device_list()). On systems with multiple audio outputs (such as analog, USB and HDMI audio), this can be used to select the audio output device. The value "Default" will play audio on the system-wide default audio output. If an invalid device name is set, the value will be reverted back to "Default".

float playback_speed_scale = 1.0 

void set_playback_speed_scale(value: float)

float get_playback_speed_scale()

Scales the rate at which audio is played (i.e. setting it to 0.5 will make the audio be played at half its speed). See also Engine.time_scale to affect the general simulation speed, which is independent from playback_speed_scale.

void add_bus(at_position: int = -1) 

Adds a bus at at_position.

void add_bus_effect(bus_idx: int, effect: AudioEffect, at_position: int = -1) 

Adds an AudioEffect effect to the bus bus_idx at at_position.

AudioBusLayout generate_bus_layout() const 

Generates an AudioBusLayout using the available buses and effects.

int get_bus_channels(bus_idx: int) const 

Returns the number of channels of the bus at index bus_idx.

AudioEffect get_bus_effect(bus_idx: int, effect_idx: int) 

Returns the AudioEffect at position effect_idx in bus bus_idx.

int get_bus_effect_count(bus_idx: int) 

Returns the number of effects on the bus at bus_idx.

AudioEffectInstance get_bus_effect_instance(bus_idx: int, effect_idx: int, channel: int = 0) 

Returns the AudioEffectInstance assigned to the given bus and effect indices (and optionally channel).

int get_bus_index(bus_name: StringName) const 

Returns the index of the bus with the name bus_name. Returns -1 if no bus with the specified name exist.

String get_bus_name(bus_idx: int) const 

Returns the name of the bus with the index bus_idx.

float get_bus_peak_volume_left_db(bus_idx: int, channel: int) const 

Returns the peak volume of the left speaker at bus index bus_idx and channel index channel.

float get_bus_peak_volume_right_db(bus_idx: int, channel: int) const 

Returns the peak volume of the right speaker at bus index bus_idx and channel index channel.

StringName get_bus_send(bus_idx: int) const 

Returns the name of the bus that the bus at index bus_idx sends to.

float get_bus_volume_db(bus_idx: int) const 

Returns the volume of the bus at index bus_idx in dB.

float get_bus_volume_linear(bus_idx: int) const 

Returns the volume of the bus at index bus_idx as a linear value.

Note: The returned value is equivalent to the result of @GlobalScope.db_to_linear() on the result of get_bus_volume_db().

String get_driver_name() const 

Returns the name of the current audio driver. The default usually depends on the operating system, but may be overridden via the --audio-driver command line argument. --headless also automatically sets the audio driver to Dummy. See also ProjectSettings.audio/driver/driver.

PackedStringArray get_input_device_list() 

Returns the names of all audio input devices detected on the system.

Note: ProjectSettings.audio/driver/enable_input must be true for audio input to work. See also that setting's description for caveats related to permissions and operating system privacy settings.

float get_input_mix_rate() const 

Returns the sample rate at the input of the AudioServer.

float get_mix_rate() const 

Returns the sample rate at the output of the AudioServer.

PackedStringArray get_output_device_list() 

Returns the names of all audio output devices detected on the system.

float get_output_latency() const 

Returns the audio driver's effective output latency. This is based on ProjectSettings.audio/driver/output_latency, but the exact returned value will differ depending on the operating system and audio driver.

Note: This can be expensive; it is not recommended to call get_output_latency() every frame.

SpeakerMode get_speaker_mode() const 

Returns the speaker configuration.

float get_time_since_last_mix() const 

Returns the relative time since the last mix occurred.

float get_time_to_next_mix() const 

Returns the relative time until the next mix occurs.

bool is_bus_bypassing_effects(bus_idx: int) const 

If true, the bus at index bus_idx is bypassing effects.

bool is_bus_effect_enabled(bus_idx: int, effect_idx: int) const 

If true, the effect at index effect_idx on the bus at index bus_idx is enabled.

bool is_bus_mute(bus_idx: int) const 

If true, the bus at index bus_idx is muted.

bool is_bus_solo(bus_idx: int) const 

If true, the bus at index bus_idx is in solo mode.

bool is_stream_registered_as_sample(stream: AudioStream) 

Experimental: This method may be changed or removed in future versions.

If true, the stream is registered as a sample. The engine will not have to register it before playing the sample.

If false, the stream will have to be registered before playing it. To prevent lag spikes, register the stream as sample with register_stream_as_sample().

Locks the audio driver's main loop.

Note: Remember to unlock it afterwards.

void move_bus(index: int, to_index: int) 

Moves the bus from index index to index to_index.

void register_stream_as_sample(stream: AudioStream) 

Experimental: This method may be changed or removed in future versions.

Forces the registration of a stream as a sample.

Note: Lag spikes may occur when calling this method, especially on single-threaded builds. It is suggested to call this method while loading assets, where the lag spike could be masked, instead of registering the sample right before it needs to be played.

void remove_bus(index: int) 

Removes the bus at index index.

void remove_bus_effect(bus_idx: int, effect_idx: int) 

Removes the effect at index effect_idx from the bus at index bus_idx.

void set_bus_bypass_effects(bus_idx: int, enable: bool) 

If true, the bus at index bus_idx is bypassing effects.

void set_bus_effect_enabled(bus_idx: int, effect_idx: int, enabled: bool) 

If true, the effect at index effect_idx on the bus at index bus_idx is enabled.

void set_bus_layout(bus_layout: AudioBusLayout) 

Overwrites the currently used AudioBusLayout.

void set_bus_mute(bus_idx: int, enable: bool) 

If true, the bus at index bus_idx is muted.

void set_bus_name(bus_idx: int, name: String) 

Sets the name of the bus at index bus_idx to name.

void set_bus_send(bus_idx: int, send: StringName) 

Connects the output of the bus at bus_idx to the bus named send.

void set_bus_solo(bus_idx: int, enable: bool) 

If true, the bus at index bus_idx is in solo mode.

void set_bus_volume_db(bus_idx: int, volume_db: float) 

Sets the volume in decibels of the bus at index bus_idx to volume_db.

void set_bus_volume_linear(bus_idx: int, volume_linear: float) 

Sets the volume as a linear value of the bus at index bus_idx to volume_linear.

Note: Using this method is equivalent to calling set_bus_volume_db() with the result of @GlobalScope.linear_to_db() on a value.

void set_enable_tagging_used_audio_streams(enable: bool) 

If set to true, all instances of AudioStreamPlayback will call AudioStreamPlayback._tag_used_streams() every mix step.

Note: This is enabled by default in the editor, as it is used by editor plugins for the audio stream previews.

void swap_bus_effects(bus_idx: int, effect_idx: int, by_effect_idx: int) 

Swaps the position of two effects in bus bus_idx.

Unlocks the audio driver's main loop. (After locking it, you should always unlock it.)

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamGeneratorPlayback

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamgeneratorplayback.html

**Contents:**
- AudioStreamGeneratorPlayback
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

Inherits: AudioStreamPlaybackResampled < AudioStreamPlayback < RefCounted < Object

Plays back audio generated using AudioStreamGenerator.

This class is meant to be used with AudioStreamGenerator to play back the generated audio in real-time.

Godot 3.2 will get new audio features

can_push_buffer(amount: int) const

get_frames_available() const

push_buffer(frames: PackedVector2Array)

push_frame(frame: Vector2)

bool can_push_buffer(amount: int) const 

Returns true if a buffer of the size amount can be pushed to the audio sample data buffer without overflowing it, false otherwise.

void clear_buffer() 

Clears the audio sample data buffer.

int get_frames_available() const 

Returns the number of frames that can be pushed to the audio sample data buffer without overflowing it. If the result is 0, the buffer is full.

int get_skips() const 

Returns the number of times the playback skipped due to a buffer underrun in the audio sample data. This value is reset at the start of the playback.

bool push_buffer(frames: PackedVector2Array) 

Pushes several audio data frames to the buffer. This is usually more efficient than push_frame() in C# and compiled languages via GDExtension, but push_buffer() may be less efficient in GDScript.

bool push_frame(frame: Vector2) 

Pushes a single audio data frame to the buffer. This is usually less efficient than push_buffer() in C# and compiled languages via GDExtension, but push_frame() may be more efficient in GDScript.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamGenerator

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamgenerator.html

**Contents:**
- AudioStreamGenerator
- Description
- Tutorials
- Properties
- Enumerations
- Property Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

An audio stream with utilities for procedural sound generation.

AudioStreamGenerator is a type of audio stream that does not play back sounds on its own; instead, it expects a script to generate audio data for it. See also AudioStreamGeneratorPlayback.

Here's a sample on how to use it to generate a sine wave:

In the example above, the "AudioStreamPlayer" node must use an AudioStreamGenerator as its stream. The fill_buffer function provides audio data for approximating a sine wave.

See also AudioEffectSpectrumAnalyzer for performing real-time audio spectrum analysis.

Note: Due to performance constraints, this class is best used from C# or from a compiled language via GDExtension. If you still want to use this class from GDScript, consider using a lower mix_rate such as 11,025 Hz or 22,050 Hz.

AudioStreamGeneratorMixRate

enum AudioStreamGeneratorMixRate: 

AudioStreamGeneratorMixRate MIX_RATE_OUTPUT = 0

Current AudioServer output mixing rate.

AudioStreamGeneratorMixRate MIX_RATE_INPUT = 1

Current AudioServer input mixing rate.

AudioStreamGeneratorMixRate MIX_RATE_CUSTOM = 2

Custom mixing rate, specified by mix_rate.

AudioStreamGeneratorMixRate MIX_RATE_MAX = 3

Maximum value for the mixing rate mode enum.

float buffer_length = 0.5 

void set_buffer_length(value: float)

float get_buffer_length()

The length of the buffer to generate (in seconds). Lower values result in less latency, but require the script to generate audio data faster, resulting in increased CPU usage and more risk for audio cracking if the CPU can't keep up.

float mix_rate = 44100.0 

void set_mix_rate(value: float)

The sample rate to use (in Hz). Higher values are more demanding for the CPU to generate, but result in better quality.

In games, common sample rates in use are 11025, 16000, 22050, 32000, 44100, and 48000.

According to the Nyquist-Shannon sampling theorem, there is no quality difference to human hearing when going past 40,000 Hz (since most humans can only hear up to ~20,000 Hz, often less). If you are generating lower-pitched sounds such as voices, lower sample rates such as 32000 or 22050 may be usable with no loss in quality.

Note: AudioStreamGenerator is not automatically resampling input data, to produce expected result mix_rate_mode should match the sampling rate of input data.

Note: If you are using AudioEffectCapture as the source of your data, set mix_rate_mode to MIX_RATE_INPUT or MIX_RATE_OUTPUT to automatically match current AudioServer mixing rate.

AudioStreamGeneratorMixRate mix_rate_mode = 2 

void set_mix_rate_mode(value: AudioStreamGeneratorMixRate)

AudioStreamGeneratorMixRate get_mix_rate_mode()

Mixing rate mode. If set to MIX_RATE_CUSTOM, mix_rate is used, otherwise current AudioServer mixing rate is used.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var playback # Will hold the AudioStreamGeneratorPlayback.
@onready var sample_hz = $AudioStreamPlayer.stream.mix_rate
var pulse_hz = 440.0 # The frequency of the sound wave.
var phase = 0.0

func _ready():
    $AudioStreamPlayer.play()
    playback = $AudioStreamPlayer.get_stream_playback()
    fill_buffer()

func fill_buffer():
    var increment = pulse_hz / sample_hz
    var frames_available = playback.get_frames_available()

    for i in range(frames_available):
        playback.push_frame(Vector2.ONE * sin(phase * TAU))
        phase = fmod(phase + increment, 1.0)
```

Example 2 (csharp):
```csharp
[Export] public AudioStreamPlayer Player { get; set; }

private AudioStreamGeneratorPlayback _playback; // Will hold the AudioStreamGeneratorPlayback.
private float _sampleHz;
private float _pulseHz = 440.0f; // The frequency of the sound wave.
private double phase = 0.0;

public override void _Ready()
{
    if (Player.Stream is AudioStreamGenerator generator) // Type as a generator to access MixRate.
    {
        _sampleHz = generator.MixRate;
        Player.Play();
        _playback = (AudioStreamGeneratorPlayback)Player.GetStreamPlayback();
        FillBuffer();
    }
}

public void FillBuffer()
{
    float increment = _pulseHz / _sampleHz;
    int framesAvailable = _playback.GetFramesAvailable();

    for (int i = 0; i < framesAvailable; i++)
    {
        _playback.PushFrame(Vector2.One * (float)Mathf.Sin(phase * Mathf.Tau));
        phase = Mathf.PosMod(phase + increment, 1.0);
    }
}
```

---

## AudioStreamInteractive

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreaminteractive.html

**Contents:**
- AudioStreamInteractive
- Description
- Properties
- Methods
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

Audio stream that can playback music interactively, combining clips and a transition table.

This is an audio stream that can playback music interactively, combining clips and a transition table. Clips must be added first, and then the transition rules via the add_transition(). Additionally, this stream exports a property parameter to control the playback via AudioStreamPlayer, AudioStreamPlayer2D, or AudioStreamPlayer3D.

The way this is used is by filling a number of clips, then configuring the transition table. From there, clips are selected for playback and the music will smoothly go from the current to the new one while using the corresponding transition rule defined in the transition table.

add_transition(from_clip: int, to_clip: int, from_time: TransitionFromTime, to_time: TransitionToTime, fade_mode: FadeMode, fade_beats: float, use_filler_clip: bool = false, filler_clip: int = -1, hold_previous: bool = false)

erase_transition(from_clip: int, to_clip: int)

get_clip_auto_advance(clip_index: int) const

get_clip_auto_advance_next_clip(clip_index: int) const

get_clip_name(clip_index: int) const

get_clip_stream(clip_index: int) const

get_transition_fade_beats(from_clip: int, to_clip: int) const

get_transition_fade_mode(from_clip: int, to_clip: int) const

get_transition_filler_clip(from_clip: int, to_clip: int) const

get_transition_from_time(from_clip: int, to_clip: int) const

get_transition_list() const

get_transition_to_time(from_clip: int, to_clip: int) const

has_transition(from_clip: int, to_clip: int) const

is_transition_holding_previous(from_clip: int, to_clip: int) const

is_transition_using_filler_clip(from_clip: int, to_clip: int) const

set_clip_auto_advance(clip_index: int, mode: AutoAdvanceMode)

set_clip_auto_advance_next_clip(clip_index: int, auto_advance_next_clip: int)

set_clip_name(clip_index: int, name: StringName)

set_clip_stream(clip_index: int, stream: AudioStream)

enum TransitionFromTime: 

TransitionFromTime TRANSITION_FROM_TIME_IMMEDIATE = 0

Start transition as soon as possible, don't wait for any specific time position.

TransitionFromTime TRANSITION_FROM_TIME_NEXT_BEAT = 1

Transition when the clip playback position reaches the next beat.

TransitionFromTime TRANSITION_FROM_TIME_NEXT_BAR = 2

Transition when the clip playback position reaches the next bar.

TransitionFromTime TRANSITION_FROM_TIME_END = 3

Transition when the current clip finished playing.

enum TransitionToTime: 

TransitionToTime TRANSITION_TO_TIME_SAME_POSITION = 0

Transition to the same position in the destination clip. This is useful when both clips have exactly the same length and the music should fade between them.

TransitionToTime TRANSITION_TO_TIME_START = 1

Transition to the start of the destination clip.

FadeMode FADE_DISABLED = 0

Do not use fade for the transition. This is useful when transitioning from a clip-end to clip-beginning, and each clip has their begin/end.

Use a fade-in in the next clip, let the current clip finish.

FadeMode FADE_OUT = 2

Use a fade-out in the current clip, the next clip will start by itself.

FadeMode FADE_CROSS = 3

Use a cross-fade between clips.

FadeMode FADE_AUTOMATIC = 4

Use automatic fade logic depending on the transition from/to. It is recommended to use this by default.

enum AutoAdvanceMode: 

AutoAdvanceMode AUTO_ADVANCE_DISABLED = 0

Disable auto-advance (default).

AutoAdvanceMode AUTO_ADVANCE_ENABLED = 1

Enable auto-advance, a clip must be specified.

AutoAdvanceMode AUTO_ADVANCE_RETURN_TO_HOLD = 2

Enable auto-advance, but instead of specifying a clip, the playback will return to hold (see add_transition()).

This constant describes that any clip is valid for a specific transition as either source or destination.

void set_clip_count(value: int)

Amount of clips contained in this interactive player.

int initial_clip = 0 

void set_initial_clip(value: int)

int get_initial_clip()

Index of the initial clip, which will be played first when this stream is played.

void add_transition(from_clip: int, to_clip: int, from_time: TransitionFromTime, to_time: TransitionToTime, fade_mode: FadeMode, fade_beats: float, use_filler_clip: bool = false, filler_clip: int = -1, hold_previous: bool = false) 

Add a transition between two clips. Provide the indices of the source and destination clips, or use the CLIP_ANY constant to indicate that transition happens to/from any clip to this one.

* from_time indicates the moment in the current clip the transition will begin after triggered.

* to_time indicates the time in the next clip that the playback will start from.

* fade_mode indicates how the fade will happen between clips. If unsure, just use FADE_AUTOMATIC which uses the most common type of fade for each situation.

* fade_beats indicates how many beats the fade will take. Using decimals is allowed.

* use_filler_clip indicates that there will be a filler clip used between the source and destination clips.

* filler_clip the index of the filler clip.

* If hold_previous is used, then this clip will be remembered. This can be used together with AUTO_ADVANCE_RETURN_TO_HOLD to return to this clip after another is done playing.

void erase_transition(from_clip: int, to_clip: int) 

Erase a transition by providing from_clip and to_clip clip indices. CLIP_ANY can be used for either argument or both.

AutoAdvanceMode get_clip_auto_advance(clip_index: int) const 

Return whether a clip has auto-advance enabled. See set_clip_auto_advance().

int get_clip_auto_advance_next_clip(clip_index: int) const 

Return the clip towards which the clip referenced by clip_index will auto-advance to.

StringName get_clip_name(clip_index: int) const 

Return the name of a clip.

AudioStream get_clip_stream(clip_index: int) const 

Return the AudioStream associated with a clip.

float get_transition_fade_beats(from_clip: int, to_clip: int) const 

Return the time (in beats) for a transition (see add_transition()).

FadeMode get_transition_fade_mode(from_clip: int, to_clip: int) const 

Return the mode for a transition (see add_transition()).

int get_transition_filler_clip(from_clip: int, to_clip: int) const 

Return the filler clip for a transition (see add_transition()).

TransitionFromTime get_transition_from_time(from_clip: int, to_clip: int) const 

Return the source time position for a transition (see add_transition()).

PackedInt32Array get_transition_list() const 

Return the list of transitions (from, to interleaved).

TransitionToTime get_transition_to_time(from_clip: int, to_clip: int) const 

Return the destination time position for a transition (see add_transition()).

bool has_transition(from_clip: int, to_clip: int) const 

Returns true if a given transition exists (was added via add_transition()).

bool is_transition_holding_previous(from_clip: int, to_clip: int) const 

Return whether a transition uses the hold previous functionality (see add_transition()).

bool is_transition_using_filler_clip(from_clip: int, to_clip: int) const 

Return whether a transition uses the filler clip functionality (see add_transition()).

void set_clip_auto_advance(clip_index: int, mode: AutoAdvanceMode) 

Set whether a clip will auto-advance by changing the auto-advance mode.

void set_clip_auto_advance_next_clip(clip_index: int, auto_advance_next_clip: int) 

Set the index of the next clip towards which this clip will auto advance to when finished. If the clip being played loops, then auto-advance will be ignored.

void set_clip_name(clip_index: int, name: StringName) 

Set the name of the current clip (for easier identification).

void set_clip_stream(clip_index: int, stream: AudioStream) 

Set the AudioStream associated with the current clip.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamMicrophone

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreammicrophone.html

**Contents:**
- AudioStreamMicrophone
- Description
- Tutorials
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

Plays real-time audio input data.

When used directly in an AudioStreamPlayer node, AudioStreamMicrophone plays back microphone input in real-time. This can be used in conjunction with AudioEffectCapture to process the data or save it.

Note: ProjectSettings.audio/driver/enable_input must be true for audio input to work. See also that setting's description for caveats related to permissions and operating system privacy settings.

Recording with microphone

Audio Mic Record Demo

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamMP3

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreammp3.html

**Contents:**
- AudioStreamMP3
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

MP3 audio stream driver.

MP3 audio stream driver. See data if you want to load an MP3 file at run-time.

Note: This class can optionally support legacy MP1 and MP2 formats, provided that the engine is compiled with the minimp3_extra_formats=yes SCons option. These extra formats are not enabled by default.

load_from_buffer(stream_data: PackedByteArray) static

load_from_file(path: String) static

void set_bar_beats(value: int)

There is currently no description for this property. Please help us by contributing one!

void set_beat_count(value: int)

There is currently no description for this property. Please help us by contributing one!

void set_bpm(value: float)

There is currently no description for this property. Please help us by contributing one!

PackedByteArray data = PackedByteArray() 

void set_data(value: PackedByteArray)

PackedByteArray get_data()

Contains the audio data in bytes.

You can load a file without having to import it beforehand using the code snippet below. Keep in mind that this snippet loads the whole file into memory and may not be ideal for huge files (hundreds of megabytes or more).

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

void set_loop(value: bool)

If true, the stream will automatically loop when it reaches the end.

float loop_offset = 0.0 

void set_loop_offset(value: float)

float get_loop_offset()

Time in seconds at which the stream starts after being looped.

AudioStreamMP3 load_from_buffer(stream_data: PackedByteArray) static 

Creates a new AudioStreamMP3 instance from the given buffer. The buffer must contain MP3 data.

AudioStreamMP3 load_from_file(path: String) static 

Creates a new AudioStreamMP3 instance from the given file path. The file must be in MP3 format.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
func load_mp3(path):
    var file = FileAccess.open(path, FileAccess.READ)
    var sound = AudioStreamMP3.new()
    sound.data = file.get_buffer(file.get_length())
    return sound
```

Example 2 (julia):
```julia
public AudioStreamMP3 LoadMP3(string path)
{
    using var file = FileAccess.Open(path, FileAccess.ModeFlags.Read);
    var sound = new AudioStreamMP3();
    sound.Data = file.GetBuffer(file.GetLength());
    return sound;
}
```

---

## AudioStreamOggVorbis

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamoggvorbis.html

**Contents:**
- AudioStreamOggVorbis
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

A class representing an Ogg Vorbis audio stream.

The AudioStreamOggVorbis class is a specialized AudioStream for handling Ogg Vorbis file formats. It offers functionality for loading and playing back Ogg Vorbis files, as well as managing looping and other playback properties. This class is part of the audio stream system, which also supports WAV files through the AudioStreamWAV class.

Runtime file loading and saving

load_from_buffer(stream_data: PackedByteArray) static

load_from_file(path: String) static

void set_bar_beats(value: int)

There is currently no description for this property. Please help us by contributing one!

void set_beat_count(value: int)

There is currently no description for this property. Please help us by contributing one!

void set_bpm(value: float)

There is currently no description for this property. Please help us by contributing one!

void set_loop(value: bool)

If true, the audio will play again from the specified loop_offset once it is done playing. Useful for ambient sounds and background music.

float loop_offset = 0.0 

void set_loop_offset(value: float)

float get_loop_offset()

Time in seconds at which the stream starts after being looped.

OggPacketSequence packet_sequence 

void set_packet_sequence(value: OggPacketSequence)

OggPacketSequence get_packet_sequence()

Contains the raw Ogg data for this stream.

Dictionary tags = {} 

void set_tags(value: Dictionary)

Dictionary get_tags()

Contains user-defined tags if found in the Ogg Vorbis data.

Commonly used tags include title, artist, album, tracknumber, and date (date does not have a standard date format).

Note: No tag is guaranteed to be present in every file, so make sure to account for the keys not always existing.

AudioStreamOggVorbis load_from_buffer(stream_data: PackedByteArray) static 

Creates a new AudioStreamOggVorbis instance from the given buffer. The buffer must contain Ogg Vorbis data.

AudioStreamOggVorbis load_from_file(path: String) static 

Creates a new AudioStreamOggVorbis instance from the given file path. The file must be in Ogg Vorbis format.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlaybackInteractive

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplaybackinteractive.html

**Contents:**
- AudioStreamPlaybackInteractive
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: AudioStreamPlayback < RefCounted < Object

Playback component of AudioStreamInteractive.

Playback component of AudioStreamInteractive. Contains functions to change the currently played clip.

get_current_clip_index() const

switch_to_clip(clip_index: int)

switch_to_clip_by_name(clip_name: StringName)

int get_current_clip_index() const 

Return the index of the currently playing clip. You can use this to get the name of the currently playing clip with AudioStreamInteractive.get_clip_name().

Example: Get the currently playing clip name from inside an AudioStreamPlayer node.

void switch_to_clip(clip_index: int) 

Switch to a clip (by index).

void switch_to_clip_by_name(clip_name: StringName) 

Switch to a clip (by name).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var playing_clip_name = stream.get_clip_name(get_stream_playback().get_current_clip_index())
```

---

## AudioStreamPlaybackOggVorbis

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplaybackoggvorbis.html

**Contents:**
- AudioStreamPlaybackOggVorbis
- User-contributed notes

Inherits: AudioStreamPlaybackResampled < AudioStreamPlayback < RefCounted < Object

There is currently no description for this class. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlaybackPlaylist

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplaybackplaylist.html

**Contents:**
- AudioStreamPlaybackPlaylist
- User-contributed notes

Inherits: AudioStreamPlayback < RefCounted < Object

Playback class used for AudioStreamPlaylist.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlaybackPolyphonic

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplaybackpolyphonic.html

**Contents:**
- AudioStreamPlaybackPolyphonic
- Description
- Methods
- Constants
- Method Descriptions
- User-contributed notes

Inherits: AudioStreamPlayback < RefCounted < Object

Playback instance for AudioStreamPolyphonic.

Playback instance for AudioStreamPolyphonic. After setting the stream property of AudioStreamPlayer, AudioStreamPlayer2D, or AudioStreamPlayer3D, the playback instance can be obtained by calling AudioStreamPlayer.get_stream_playback(), AudioStreamPlayer2D.get_stream_playback() or AudioStreamPlayer3D.get_stream_playback() methods.

is_stream_playing(stream: int) const

play_stream(stream: AudioStream, from_offset: float = 0, volume_db: float = 0, pitch_scale: float = 1.0, playback_type: PlaybackType = 0, bus: StringName = &"Master")

set_stream_pitch_scale(stream: int, pitch_scale: float)

set_stream_volume(stream: int, volume_db: float)

stop_stream(stream: int)

Returned by play_stream() in case it could not allocate a stream for playback.

bool is_stream_playing(stream: int) const 

Returns true if the stream associated with the given integer ID is still playing. Check play_stream() for information on when this ID becomes invalid.

int play_stream(stream: AudioStream, from_offset: float = 0, volume_db: float = 0, pitch_scale: float = 1.0, playback_type: PlaybackType = 0, bus: StringName = &"Master") 

Play an AudioStream at a given offset, volume, pitch scale, playback type, and bus. Playback starts immediately.

The return value is a unique integer ID that is associated to this playback stream and which can be used to control it.

This ID becomes invalid when the stream ends (if it does not loop), when the AudioStreamPlaybackPolyphonic is stopped, or when stop_stream() is called.

This function returns INVALID_ID if the amount of streams currently playing equals AudioStreamPolyphonic.polyphony. If you need a higher amount of maximum polyphony, raise this value.

void set_stream_pitch_scale(stream: int, pitch_scale: float) 

Change the stream pitch scale. The stream argument is an integer ID returned by play_stream().

void set_stream_volume(stream: int, volume_db: float) 

Change the stream volume (in db). The stream argument is an integer ID returned by play_stream().

void stop_stream(stream: int) 

Stop a stream. The stream argument is an integer ID returned by play_stream(), which becomes invalid after calling this function.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlaybackResampled

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplaybackresampled.html

**Contents:**
- AudioStreamPlaybackResampled
- Methods
- Method Descriptions
- User-contributed notes

Inherits: AudioStreamPlayback < RefCounted < Object

Inherited By: AudioStreamGeneratorPlayback, AudioStreamPlaybackOggVorbis

There is currently no description for this class. Please help us by contributing one!

_get_stream_sampling_rate() virtual required const

_mix_resampled(dst_buffer: AudioFrame*, frame_count: int) virtual required

float _get_stream_sampling_rate() virtual required const 

There is currently no description for this method. Please help us by contributing one!

int _mix_resampled(dst_buffer: AudioFrame*, frame_count: int) virtual required 

There is currently no description for this method. Please help us by contributing one!

void begin_resample() 

There is currently no description for this method. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlaybackSynchronized

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplaybacksynchronized.html

**Contents:**
- AudioStreamPlaybackSynchronized
- User-contributed notes

Inherits: AudioStreamPlayback < RefCounted < Object

There is currently no description for this class. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlayback

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplayback.html

**Contents:**
- AudioStreamPlayback
- Description
- Tutorials
- Methods
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: AudioStreamPlaybackInteractive, AudioStreamPlaybackPlaylist, AudioStreamPlaybackPolyphonic, AudioStreamPlaybackResampled, AudioStreamPlaybackSynchronized

Meta class for playing back audio.

Can play, loop, pause a scroll through audio. See AudioStream and AudioStreamOggVorbis for usage.

_get_loop_count() virtual const

_get_parameter(name: StringName) virtual const

_get_playback_position() virtual const

_is_playing() virtual const

_mix(buffer: AudioFrame*, rate_scale: float, frames: int) virtual required

_seek(position: float) virtual

_set_parameter(name: StringName, value: Variant) virtual

_start(from_pos: float) virtual

_tag_used_streams() virtual

get_loop_count() const

get_playback_position() const

get_sample_playback() const

mix_audio(rate_scale: float, frames: int)

seek(time: float = 0.0)

set_sample_playback(playback_sample: AudioSamplePlayback)

start(from_pos: float = 0.0)

int _get_loop_count() virtual const 

Overridable method. Should return how many times this audio stream has looped. Most built-in playbacks always return 0.

Variant _get_parameter(name: StringName) virtual const 

Return the current value of a playback parameter by name (see AudioStream._get_parameter_list()).

float _get_playback_position() virtual const 

Overridable method. Should return the current progress along the audio stream, in seconds.

bool _is_playing() virtual const 

Overridable method. Should return true if this playback is active and playing its audio stream.

int _mix(buffer: AudioFrame*, rate_scale: float, frames: int) virtual required 

Override this method to customize how the audio stream is mixed. This method is called even if the playback is not active.

Note: It is not useful to override this method in GDScript or C#. Only GDExtension can take advantage of it.

void _seek(position: float) virtual 

Override this method to customize what happens when seeking this audio stream at the given position, such as by calling AudioStreamPlayer.seek().

void _set_parameter(name: StringName, value: Variant) virtual 

Set the current value of a playback parameter by name (see AudioStream._get_parameter_list()).

void _start(from_pos: float) virtual 

Override this method to customize what happens when the playback starts at the given position, such as by calling AudioStreamPlayer.play().

void _stop() virtual 

Override this method to customize what happens when the playback is stopped, such as by calling AudioStreamPlayer.stop().

void _tag_used_streams() virtual 

Overridable method. Called whenever the audio stream is mixed if the playback is active and AudioServer.set_enable_tagging_used_audio_streams() has been set to true. Editor plugins may use this method to "tag" the current position along the audio stream and display it in a preview.

int get_loop_count() const 

Returns the number of times the stream has looped.

float get_playback_position() const 

Returns the current position in the stream, in seconds.

AudioSamplePlayback get_sample_playback() const 

Experimental: This method may be changed or removed in future versions.

Returns the AudioSamplePlayback associated with this AudioStreamPlayback for playing back the audio sample of this stream.

bool is_playing() const 

Returns true if the stream is playing.

PackedVector2Array mix_audio(rate_scale: float, frames: int) 

Mixes up to frames of audio from the stream from the current position, at a rate of rate_scale, advancing the stream.

Returns a PackedVector2Array where each element holds the left and right channel volume levels of each frame.

Note: Can return fewer frames than requested, make sure to use the size of the return value.

void seek(time: float = 0.0) 

Seeks the stream at the given time, in seconds.

void set_sample_playback(playback_sample: AudioSamplePlayback) 

Experimental: This method may be changed or removed in future versions.

Associates AudioSamplePlayback to this AudioStreamPlayback for playing back the audio sample of this stream.

void start(from_pos: float = 0.0) 

Starts the stream from the given from_pos, in seconds.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlayer

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplayer.html

**Contents:**
- AudioStreamPlayer
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node < Object

A node for audio playback.

The AudioStreamPlayer node plays an audio stream non-positionally. It is ideal for user interfaces, menus, or background music.

To use this node, stream needs to be set to a valid AudioStream resource. Playing more than one sound at the same time is also supported, see max_polyphony.

If you need to play audio at a specific position, use AudioStreamPlayer2D or AudioStreamPlayer3D instead.

2D Dodge The Creeps Demo

Audio Device Changer Demo

Audio Microphone Record Demo

Audio Spectrum Visualizer Demo

get_playback_position()

get_stream_playback()

has_stream_playback()

play(from_position: float = 0.0)

seek(to_position: float)

Emitted when a sound finishes playing without interruptions. This signal is not emitted when calling stop(), or when exiting the tree while sounds are playing.

MixTarget MIX_TARGET_STEREO = 0

The audio will be played only on the first channel. This is the default.

MixTarget MIX_TARGET_SURROUND = 1

The audio will be played on all surround channels.

MixTarget MIX_TARGET_CENTER = 2

The audio will be played on the second channel, which is usually the center.

bool autoplay = false 

void set_autoplay(value: bool)

bool is_autoplay_enabled()

If true, this node calls play() when entering the tree.

StringName bus = &"Master" 

void set_bus(value: StringName)

The target bus name. All sounds from this node will be playing on this bus.

Note: At runtime, if no bus with the given name exists, all sounds will fall back on "Master". See also AudioServer.get_bus_name().

int max_polyphony = 1 

void set_max_polyphony(value: int)

int get_max_polyphony()

The maximum number of sounds this node can play at the same time. Calling play() after this value is reached will cut off the oldest sounds.

MixTarget mix_target = 0 

void set_mix_target(value: MixTarget)

MixTarget get_mix_target()

The mix target channels. Has no effect when two speakers or less are detected (see SpeakerMode).

float pitch_scale = 1.0 

void set_pitch_scale(value: float)

float get_pitch_scale()

The audio's pitch and tempo, as a multiplier of the stream's sample rate. A value of 2.0 doubles the audio's pitch, while a value of 0.5 halves the pitch.

PlaybackType playback_type = 0 

void set_playback_type(value: PlaybackType)

PlaybackType get_playback_type()

Experimental: This property may be changed or removed in future versions.

The playback type of the stream player. If set other than to the default value, it will force that playback type.

bool playing = false 

void set_playing(value: bool)

If true, this node is playing sounds. Setting this property has the same effect as play() and stop().

void set_stream(value: AudioStream)

AudioStream get_stream()

The AudioStream resource to be played. Setting this property stops all currently playing sounds. If left empty, the AudioStreamPlayer does not work.

bool stream_paused = false 

void set_stream_paused(value: bool)

bool get_stream_paused()

If true, the sounds are paused. Setting stream_paused to false resumes all sounds.

Note: This property is automatically changed when exiting or entering the tree, or this node is paused (see Node.process_mode).

float volume_db = 0.0 

void set_volume_db(value: float)

float get_volume_db()

Volume of sound, in decibels. This is an offset of the stream's volume.

Note: To convert between decibel and linear energy (like most volume sliders do), use volume_linear, or @GlobalScope.db_to_linear() and @GlobalScope.linear_to_db().

float volume_linear 

void set_volume_linear(value: float)

float get_volume_linear()

Volume of sound, as a linear value.

Note: This member modifies volume_db for convenience. The returned value is equivalent to the result of @GlobalScope.db_to_linear() on volume_db. Setting this member is equivalent to setting volume_db to the result of @GlobalScope.linear_to_db() on a value.

float get_playback_position() 

Returns the position in the AudioStream of the latest sound, in seconds. Returns 0.0 if no sounds are playing.

Note: The position is not always accurate, as the AudioServer does not mix audio every processed frame. To get more accurate results, add AudioServer.get_time_since_last_mix() to the returned position.

Note: This method always returns 0.0 if the stream is an AudioStreamInteractive, since it can have multiple clips playing at once.

AudioStreamPlayback get_stream_playback() 

Returns the latest AudioStreamPlayback of this node, usually the most recently created by play(). If no sounds are playing, this method fails and returns an empty playback.

bool has_stream_playback() 

Returns true if any sound is active, even if stream_paused is set to true. See also playing and get_stream_playback().

void play(from_position: float = 0.0) 

Plays a sound from the beginning, or the given from_position in seconds.

void seek(to_position: float) 

Restarts all sounds to be played from the given to_position, in seconds. Does nothing if no sounds are playing.

Stops all sounds from this node.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPlaylist

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamplaylist.html

**Contents:**
- AudioStreamPlaylist
- Properties
- Methods
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

AudioStream that includes sub-streams and plays them back like a playlist.

get_list_stream(stream_index: int) const

set_list_stream(stream_index: int, audio_stream: AudioStream)

Maximum amount of streams supported in the playlist.

float fade_time = 0.3 

void set_fade_time(value: float)

float get_fade_time()

Fade time used when a stream ends, when going to the next one. Streams are expected to have an extra bit of audio after the end to help with fading.

void set_loop(value: bool)

If true, the playlist will loop, otherwise the playlist will end when the last stream is finished.

bool shuffle = false 

void set_shuffle(value: bool)

If true, the playlist will shuffle each time playback starts and each time it loops.

int stream_count = 0 

void set_stream_count(value: int)

int get_stream_count()

Amount of streams in the playlist.

float get_bpm() const 

Returns the BPM of the playlist, which can vary depending on the clip being played.

AudioStream get_list_stream(stream_index: int) const 

Returns the stream at playback position index.

void set_list_stream(stream_index: int, audio_stream: AudioStream) 

Sets the stream at playback position index.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamPolyphonic

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreampolyphonic.html

**Contents:**
- AudioStreamPolyphonic
- Description
- Properties
- Property Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

AudioStream that lets the user play custom streams at any time from code, simultaneously using a single player.

AudioStream that lets the user play custom streams at any time from code, simultaneously using a single player.

Playback control is done via the AudioStreamPlaybackPolyphonic instance set inside the player, which can be obtained via AudioStreamPlayer.get_stream_playback(), AudioStreamPlayer2D.get_stream_playback() or AudioStreamPlayer3D.get_stream_playback() methods. Obtaining the playback instance is only valid after the stream property is set as an AudioStreamPolyphonic in those players.

void set_polyphony(value: int)

Maximum amount of simultaneous streams that can be played.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamRandomizer

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamrandomizer.html

**Contents:**
- AudioStreamRandomizer
- Description
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

Wraps a pool of audio streams with pitch and volume shifting.

Picks a random AudioStream from the pool, depending on the playback mode, and applies random pitch shifting and volume shifting during playback.

random_volume_offset_db

add_stream(index: int, stream: AudioStream, weight: float = 1.0)

get_stream(index: int) const

get_stream_probability_weight(index: int) const

move_stream(index_from: int, index_to: int)

remove_stream(index: int)

set_stream(index: int, stream: AudioStream)

set_stream_probability_weight(index: int, weight: float)

PlaybackMode PLAYBACK_RANDOM_NO_REPEATS = 0

Pick a stream at random according to the probability weights chosen for each stream, but avoid playing the same stream twice in a row whenever possible. If only 1 sound is present in the pool, the same sound will always play, effectively allowing repeats to occur.

PlaybackMode PLAYBACK_RANDOM = 1

Pick a stream at random according to the probability weights chosen for each stream. If only 1 sound is present in the pool, the same sound will always play.

PlaybackMode PLAYBACK_SEQUENTIAL = 2

Play streams in the order they appear in the stream pool. If only 1 sound is present in the pool, the same sound will always play.

PlaybackMode playback_mode = 0 

void set_playback_mode(value: PlaybackMode)

PlaybackMode get_playback_mode()

Controls how this AudioStreamRandomizer picks which AudioStream to play next.

float random_pitch = 1.0 

void set_random_pitch(value: float)

float get_random_pitch()

The intensity of random pitch variation. A value of 1 means no variation.

float random_volume_offset_db = 0.0 

void set_random_volume_offset_db(value: float)

float get_random_volume_offset_db()

The intensity of random volume variation. A value of 0 means no variation.

int streams_count = 0 

void set_streams_count(value: int)

int get_streams_count()

The number of streams in the stream pool.

void add_stream(index: int, stream: AudioStream, weight: float = 1.0) 

Insert a stream at the specified index. If the index is less than zero, the insertion occurs at the end of the underlying pool.

AudioStream get_stream(index: int) const 

Returns the stream at the specified index.

float get_stream_probability_weight(index: int) const 

Returns the probability weight associated with the stream at the given index.

void move_stream(index_from: int, index_to: int) 

Move a stream from one index to another.

void remove_stream(index: int) 

Remove the stream at the specified index.

void set_stream(index: int, stream: AudioStream) 

Set the AudioStream at the specified index.

void set_stream_probability_weight(index: int, weight: float) 

Set the probability weight of the stream at the specified index. The higher this value, the more likely that the randomizer will choose this stream during random playback modes.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamSynchronized

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamsynchronized.html

**Contents:**
- AudioStreamSynchronized
- Description
- Properties
- Methods
- Constants
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

Stream that can be fitted with sub-streams, which will be played in-sync.

This is a stream that can be fitted with sub-streams, which will be played in-sync. The streams begin at exactly the same time when play is pressed, and will end when the last of them ends. If one of the sub-streams loops, then playback will continue.

get_sync_stream(stream_index: int) const

get_sync_stream_volume(stream_index: int) const

set_sync_stream(stream_index: int, audio_stream: AudioStream)

set_sync_stream_volume(stream_index: int, volume_db: float)

Maximum amount of streams that can be synchronized.

int stream_count = 0 

void set_stream_count(value: int)

int get_stream_count()

Set the total amount of streams that will be played back synchronized.

AudioStream get_sync_stream(stream_index: int) const 

Get one of the synchronized streams, by index.

float get_sync_stream_volume(stream_index: int) const 

Get the volume of one of the synchronized streams, by index.

void set_sync_stream(stream_index: int, audio_stream: AudioStream) 

Set one of the synchronized streams, by index.

void set_sync_stream_volume(stream_index: int, volume_db: float) 

Set the volume of one of the synchronized streams, by index.

Please read the User-contributed notes policy before submitting a comment.

---

## AudioStreamWAV

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostreamwav.html

**Contents:**
- AudioStreamWAV
- Description
- Tutorials
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: AudioStream < Resource < RefCounted < Object

Stores audio data loaded from WAV files.

AudioStreamWAV stores sound samples loaded from WAV files. To play the stored sound, use an AudioStreamPlayer (for non-positional audio) or AudioStreamPlayer2D/AudioStreamPlayer3D (for positional audio). The sound can be looped.

This class can also be used to store dynamically-generated PCM audio data. See also AudioStreamGenerator for procedural audio generation.

Runtime file loading and saving

load_from_buffer(stream_data: PackedByteArray, options: Dictionary = {}) static

load_from_file(path: String, options: Dictionary = {}) static

save_to_wav(path: String)

Format FORMAT_8_BITS = 0

8-bit PCM audio codec.

Format FORMAT_16_BITS = 1

16-bit PCM audio codec.

Format FORMAT_IMA_ADPCM = 2

Audio is lossily compressed as IMA ADPCM.

Format FORMAT_QOA = 3

Audio is lossily compressed as Quite OK Audio.

LoopMode LOOP_DISABLED = 0

LoopMode LOOP_FORWARD = 1

Audio loops the data between loop_begin and loop_end, playing forward only.

LoopMode LOOP_PINGPONG = 2

Audio loops the data between loop_begin and loop_end, playing back and forth.

LoopMode LOOP_BACKWARD = 3

Audio loops the data between loop_begin and loop_end, playing backward only.

PackedByteArray data = PackedByteArray() 

void set_data(value: PackedByteArray)

PackedByteArray get_data()

Contains the audio data in bytes.

Note: If format is set to FORMAT_8_BITS, this property expects signed 8-bit PCM data. To convert from unsigned 8-bit PCM, subtract 128 from each byte.

Note: If format is set to FORMAT_QOA, this property expects data from a full QOA file.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedByteArray for more details.

void set_format(value: Format)

void set_loop_begin(value: int)

The loop start point (in number of samples, relative to the beginning of the stream).

void set_loop_end(value: int)

The loop end point (in number of samples, relative to the beginning of the stream).

LoopMode loop_mode = 0 

void set_loop_mode(value: LoopMode)

LoopMode get_loop_mode()

int mix_rate = 44100 

void set_mix_rate(value: int)

The sample rate for mixing this audio. Higher values require more storage space, but result in better quality.

In games, common sample rates in use are 11025, 16000, 22050, 32000, 44100, and 48000.

According to the Nyquist-Shannon sampling theorem, there is no quality difference to human hearing when going past 40,000 Hz (since most humans can only hear up to ~20,000 Hz, often less). If you are using lower-pitched sounds such as voices, lower sample rates such as 32000 or 22050 may be usable with no loss in quality.

bool stereo = false 

void set_stereo(value: bool)

If true, audio is stereo.

Dictionary tags = {} 

void set_tags(value: Dictionary)

Dictionary get_tags()

Contains user-defined tags if found in the WAV data.

Commonly used tags include title, artist, album, tracknumber, and date (date does not have a standard date format).

Note: No tag is guaranteed to be present in every file, so make sure to account for the keys not always existing.

Note: Only WAV files using a LIST chunk with an identifier of INFO to encode the tags are currently supported.

AudioStreamWAV load_from_buffer(stream_data: PackedByteArray, options: Dictionary = {}) static 

Creates a new AudioStreamWAV instance from the given buffer. The buffer must contain WAV data.

The keys and values of options match the properties of ResourceImporterWAV. The usage of options is identical to load_from_file().

AudioStreamWAV load_from_file(path: String, options: Dictionary = {}) static 

Creates a new AudioStreamWAV instance from the given file path. The file must be in WAV format.

The keys and values of options match the properties of ResourceImporterWAV.

Example: Load the first file dropped as a WAV and play it:

Error save_to_wav(path: String) 

Saves the AudioStreamWAV as a WAV file to path. Samples with IMA ADPCM or Quite OK Audio formats can't be saved.

Note: A .wav extension is automatically appended to path if it is missing.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
@onready var audio_player = $AudioStreamPlayer

func _ready():
    get_window().files_dropped.connect(_on_files_dropped)

func _on_files_dropped(files):
    if files[0].get_extension() == "wav":
        audio_player.stream = AudioStreamWAV.load_from_file(files[0], {
                "force/max_rate": true,
                "force/max_rate_hz": 11025
            })
        audio_player.play()
```

---

## AudioStream

**URL:** https://docs.godotengine.org/en/stable/classes/class_audiostream.html

**Contents:**
- AudioStream
- Description
- Tutorials
- Methods
- Signals
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Inherited By: AudioStreamGenerator, AudioStreamInteractive, AudioStreamMicrophone, AudioStreamMP3, AudioStreamOggVorbis, AudioStreamPlaylist, AudioStreamPolyphonic, AudioStreamRandomizer, AudioStreamSynchronized, AudioStreamWAV

Base class for audio streams.

Base class for audio streams. Audio streams are used for sound effects and music playback, and support WAV (via AudioStreamWAV) and Ogg (via AudioStreamOggVorbis) file formats.

Audio Microphone Record Demo

Audio Spectrum Visualizer Demo

_get_bar_beats() virtual const

_get_beat_count() virtual const

_get_bpm() virtual const

_get_length() virtual const

_get_parameter_list() virtual const

_get_stream_name() virtual const

_get_tags() virtual const

_has_loop() virtual const

_instantiate_playback() virtual const

_is_monophonic() virtual const

can_be_sampled() const

generate_sample() const

instantiate_playback()

is_meta_stream() const

is_monophonic() const

parameter_list_changed() 

Signal to be emitted to notify when the parameter list changed.

int _get_bar_beats() virtual const 

Override this method to return the bar beats of this stream.

int _get_beat_count() virtual const 

Overridable method. Should return the total number of beats of this audio stream. Used by the engine to determine the position of every beat.

Ideally, the returned value should be based off the stream's sample rate (AudioStreamWAV.mix_rate, for example).

float _get_bpm() virtual const 

Overridable method. Should return the tempo of this audio stream, in beats per minute (BPM). Used by the engine to determine the position of every beat.

Ideally, the returned value should be based off the stream's sample rate (AudioStreamWAV.mix_rate, for example).

float _get_length() virtual const 

Override this method to customize the returned value of get_length(). Should return the length of this audio stream, in seconds.

Array[Dictionary] _get_parameter_list() virtual const 

Return the controllable parameters of this stream. This array contains dictionaries with a property info description format (see Object.get_property_list()). Additionally, the default value for this parameter must be added tho each dictionary in "default_value" field.

String _get_stream_name() virtual const 

Override this method to customize the name assigned to this audio stream. Unused by the engine.

Dictionary _get_tags() virtual const 

Override this method to customize the tags for this audio stream. Should return a Dictionary of strings with the tag as the key and its content as the value.

Commonly used tags include title, artist, album, tracknumber, and date.

bool _has_loop() virtual const 

Override this method to return true if this stream has a loop.

AudioStreamPlayback _instantiate_playback() virtual const 

Override this method to customize the returned value of instantiate_playback(). Should return a new AudioStreamPlayback created when the stream is played (such as by an AudioStreamPlayer).

bool _is_monophonic() virtual const 

Override this method to customize the returned value of is_monophonic(). Should return true if this audio stream only supports one channel.

bool can_be_sampled() const 

Experimental: This method may be changed or removed in future versions.

Returns if the current AudioStream can be used as a sample. Only static streams can be sampled.

AudioSample generate_sample() const 

Experimental: This method may be changed or removed in future versions.

Generates an AudioSample based on the current stream.

float get_length() const 

Returns the length of the audio stream in seconds. If this stream is an AudioStreamRandomizer, returns the length of the last played stream. If this stream has an indefinite length (such as for AudioStreamGenerator and AudioStreamMicrophone), returns 0.0.

AudioStreamPlayback instantiate_playback() 

Returns a newly created AudioStreamPlayback intended to play this audio stream. Useful for when you want to extend _instantiate_playback() but call instantiate_playback() from an internally held AudioStream subresource. An example of this can be found in the source code for AudioStreamRandomPitch::instantiate_playback.

bool is_meta_stream() const 

Returns true if the stream is a collection of other streams, false otherwise.

bool is_monophonic() const 

Returns true if this audio stream only supports one channel (monophony), or false if the audio stream supports two or more channels (polyphony).

Please read the User-contributed notes policy before submitting a comment.

---

## Audio buses

**URL:** https://docs.godotengine.org/en/stable/tutorials/audio/audio_buses.html

**Contents:**
- Audio buses
- Introduction
- Decibel scale
- Audio buses
- Playback of audio through a bus
- Adding effects
- Automatic bus disabling
- Bus rearrangement
- Default bus layout
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Godot's audio processing code has been written with games in mind, with the aim of achieving an optimal balance between performance and sound quality.

Godot's audio engine allows any number of audio buses to be created and any number of effect processors can be added to each bus. Only the hardware of the device running your game will limit the number of buses and effects that can be used before performance starts to suffer.

Godot's sound interface is designed to meet the expectations of sound design professionals. To this end, it primarily uses the decibel scale.

For those unfamiliar with it, it can be explained with a few facts:

The decibel (dB) scale is a relative scale. It represents the ratio of sound power by using 20 times the base 10 logarithm of the ratio (20 × log10(P/P0)).

For every 6 dB, sound amplitude doubles or halves. 12 dB represents a factor of 4, 18 dB a factor of 8, 20 dB a factor of 10, 40 dB a factor of 100, etc.

Since the scale is logarithmic, true zero (no audio) can't be represented.

0 dB is the maximum amplitude possible in a digital audio system. This limit is not the human limit, but a limit from the sound hardware. Audio with amplitudes that are too high to be represented properly below 0 dB create a kind of distortion called clipping.

To avoid clipping, your sound mix should be arranged so that the output of the master bus (more on that later) never exceeds 0 dB.

Every 6 dB below the 0 dB limit, sound energy is halved. It means the sound volume at -6 dB is half as loud as 0dB. -12 dB is half as loud as -6 dB and so on.

When working with decibels, sound is considered no longer audible between -60 dB and -80 dB. This makes your working range generally between -60 dB and 0 dB.

This can take a bit getting used to, but it's friendlier in the end and will allow you to communicate better with audio professionals.

Audio buses can be found in the bottom panel of the Godot editor:

An audio bus (also called an audio channel) can be considered a place that audio is channeled through on the way to playback through a device's speakers. Audio data can be modified and re-routed by an audio bus. An audio bus has a VU meter (the bars that light up when sound is played) which indicates the amplitude of the signal passing through.

The leftmost bus is the master bus. This bus outputs the mix to your speakers so, as mentioned in the Decibel scale section above, make sure that your mix level doesn't reach 0 dB in this bus. The rest of the audio buses can be flexibly routed. After modifying the sound, they send it to another bus to the left. The destination bus can be specified for each of the non-master audio buses. Routing always passes audio from buses on the right to buses further to the left. This avoids infinite routing loops.

In the above image, the output of Bus 2 has been routed to the Master bus.

To test passing audio to a bus, create an AudioStreamPlayer node, load an AudioStream and select a target bus for playback:

Finally, toggle the Playing property to On and sound will flow.

You may also be interested in reading about Audio streams now.

This feature is not supported on the web platform if the AudioStreamPlayer's playback mode is set to Sample, which is the default. It will only work if the playback mode is set to Stream, at the cost of increased latency if threads are not enabled.

See Audio playback in the Exporting for the Web documentation for details.

Audio buses can contain all sorts of effects. These effects modify the sound in one way or another and are applied in order.

For information on what each effect does, see Audio effects.

There is no need to disable buses manually when not in use. Godot detects that the bus has been silent for a few seconds and disables it (including all effects).

Disabled buses have a blue VU meter instead of a red-green one.

Stream Players use bus names to identify a bus, which allows adding, removing and moving buses around while the reference to them is kept. However, if a bus is renamed, the reference will be lost and the Stream Player will output to Master. This system was chosen because rearranging buses is a more common process than renaming them.

The default bus layout is automatically saved to the res://default_bus_layout.tres file. Custom bus arrangements can be saved and loaded from disk.

Please read the User-contributed notes policy before submitting a comment.

---

## Audio effects

**URL:** https://docs.godotengine.org/en/stable/tutorials/audio/audio_effects.html

**Contents:**
- Audio effects
- Amplify
- BandLimit and BandPass
- Capture
- Chorus
- Compressor
- Delay
- Distortion
- EQ
- EQ6, EQ10, EQ21

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Godot includes several audio effects that can be added to an audio bus to alter every sound file that goes through that bus.

Try them all out to get a sense of how they alter sound. Here follows a short description of the available effects:

Amplify changes the volume of the signal. Some care needs to be taken, though: setting the level too high can make the sound digitally clip, which can produce unpleasant crackles and pops.

These are resonant filters which block frequencies around the Cutoff point. BandPass can be used to simulate sound passing through an old telephone line or megaphone. Modulating the BandPass frequency can simulate the sound of a wah-wah guitar pedal, think of the guitar in Jimi Hendrix's Voodoo Child (Slight Return).

The Capture effect copies the audio frames of the audio bus that it is on into an internal buffer. This can be used to capture data from the microphone or to transmit audio over the network in real-time.

As the name of the effect implies, the Chorus effect makes a single audio sample sound like an entire chorus. It does this by duplicating a signal and very slightly altering the timing and pitch of each duplicate, and varying that over time via an LFO (low frequency oscillator). The duplicate(s) are then mixed back together with the original signal, producing a lush, wide, and large sound. Although chorus is traditionally used for voices, it can be desirable with almost any type of sound.

A dynamic range compressor automatically attenuates (ducks) the level of the incoming signal when its amplitude exceeds a certain threshold. The level of attenuation applied is proportional to how far the incoming audio exceeds the threshold. The compressor's Ratio parameter controls the degree of attenuation. One of the main uses of a compressor is to reduce the dynamic range of signals with very loud and quiet parts. Reducing the dynamic range of a signal can make it fit more comfortably in a mix.

The compressor has many uses. For example:

It can be used in the Master bus to compress the whole output prior to being hit by a limiter, making the effect of the limiter much more subtle.

It can be used in voice channels to ensure they sound as even as possible.

It can be sidechained by another sound source. This means it can reduce the sound level of one signal using the level of another audio bus for threshold detection. This technique is very common in video game mixing to "duck" the level of music or sound effects when in-game or multiplayer voices need to be fully audible.

It can accentuate transients by using a slower attack. This can make sound effects more punchy.

If your goal is to prevent a signal from exceeding a given amplitude altogether, rather than to reduce the dynamic range of the signal, a limiter is likely a better choice than a compressor for this purpose. However, applying compression before a limiter is still good practice.

Digital delay essentially duplicates a signal and repeats it at a specified speed with a volume level that decays for each repeat. Delay is great for simulating the acoustic space of a canyon or large room, where sound bounces have a lot of delay between their repeats. This is in contrast to reverb, which has a more natural and blurred sound to it. Using this in conjunction with reverb can create very natural sounding environments!

Makes the sound distorted. Godot offers several types of distortion:

Overdrive sounds like a guitar distortion pedal or megaphone. Sounds distorted with this sound like they're coming through a low-quality speaker or device.

Tan sounds like another interesting flavor of overdrive.

Bit crushing clamps the amplitude of the signal, making it sound flat and crunchy.

All three types of distortion can add higher frequency sounds to an original sound, making it stand out better in a mix.

EQ is what all other equalizers inherit from. It can be extended with Custom scripts to create an equalizer with a custom number of bands.

Godot provides three equalizers with different numbers of bands, which are represented in the title (6, 10, and 21 bands, respectively). An equalizer on the Master bus can be useful for cutting low and high frequencies that the device's speakers can't reproduce well. For example, phone or tablet speakers usually don't reproduce low frequency sounds well, and could make a limiter or compressor attenuate sounds that aren't even audible to the user anyway.

Note: The equalizer effect can be disabled when headphones are plugged in, giving the user the best of both worlds.

Filter is what all other filters inherit from and should not be used directly.

A limiter is similar to a compressor, but it's less flexible and designed to prevent a signal's amplitude exceeding a given dB threshold. Adding a limiter to the final point of the Master bus is good practice, as it offers an easy safeguard against clipping.

Cuts frequencies below a specific Cutoff frequency. HighPassFilter is used to reduce the bass content of a signal.

Reduces all frequencies above a specific Cutoff frequency.

This is the old limiter effect, and it is recommended to use the new HardLimiter effect instead.

Here is an example of how this effect works, if the ceiling is set to -12 dB, and the threshold is 0 dB, all samples going through get reduced by 12dB. This changes the waveform of the sound and introduces distortion.

This effect is being kept to preserve compatibility, however it should be considered deprecated.

Cuts frequencies above a specific Cutoff frequency and can also resonate (boost frequencies close to the Cutoff frequency). Low pass filters can be used to simulate "muffled" sound. For instance, underwater sounds, sounds blocked by walls, or distant sounds.

Reduces all frequencies below a specific Cutoff frequency.

The opposite of the BandPassFilter, it removes a band of sound from the frequency spectrum at a given Cutoff frequency.

The Panner allows the stereo balance of a signal to be adjusted between the left and right channels. Headphones are recommended when configuring in this effect.

This effect is formed by de-phasing two duplicates of the same sound so they cancel each other out in an interesting way. Phaser produces a pleasant whooshing sound that moves back and forth through the audio spectrum, and can be a great way to create sci-fi effects or Darth Vader-like voices.

This effect allows the adjustment of the signal's pitch independently of its speed. All frequencies can be increased/decreased with minimal effect on transients. PitchShift can be useful to create unusually high or deep voices. Do note that altering pitch can sound unnatural when pushed outside of a narrow window.

The Record effect allows the user to record sound from a microphone.

Reverb simulates rooms of different sizes. It has adjustable parameters that can be tweaked to obtain the sound of a specific room. Reverb is commonly outputted from Area3Ds (see Reverb buses), or to apply a "chamber" feel to all sounds.

This effect doesn't alter audio, instead, you add this effect to buses you want a spectrum analysis of. This would typically be used for audio visualization. Visualizing voices can be a great way to draw attention to them without just increasing their volume. A demo project using this can be found here.

This effect uses a few algorithms to enhance a signal's stereo width.

Please read the User-contributed notes policy before submitting a comment.

---

## Audio streams

**URL:** https://docs.godotengine.org/en/stable/tutorials/audio/audio_streams.html

**Contents:**
- Audio streams
- Introduction
- AudioStream
- AudioStreamPlayer
- AudioStreamPlayer2D
- AudioStreamPlayer3D
  - Reverb buses
  - Doppler
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

As you might have already read in Audio buses, sound is sent to each bus via an AudioStreamPlayer node. There are different kinds of AudioStreamPlayers. Each one loads an AudioStream and plays it back.

An audio stream is an abstract object that emits sound. The sound can come from many places, but is most commonly loaded from the filesystem. Audio files can be loaded as AudioStreams and placed inside an AudioStreamPlayer. You can find information on supported formats and differences in Importing audio samples.

There are other types of AudioStreams, such as AudioStreamRandomizer. This one picks a different audio stream from a list of streams each time it's played back, and applies random pitch and volume shifting. This can be helpful for adding variation to sounds that are played back often.

This is the standard, non-positional stream player. It can play to any bus. In 5.1 sound setups, it can send audio to stereo mix or front speakers.

Playback Type is an experimental setting, and could change in future versions of Godot. It exists so Web exports use Web Audio-API based samples instead of streaming all sounds to the browser, unlike most platforms. This prevents the audio from being garbled in single-threaded Web exports. By default, only the Web platform will use samples. Changing this setting is not recommended, unless you have an explicit reason to. You can change the default playback type for the web and other platforms in the project settings under Audio > General (advanced settings must be turned on to see the setting).

This is a variant of AudioStreamPlayer, but emits sound in a 2D positional environment. When close to the left of the screen, the panning will go left. When close to the right side, it will go right.

Area2Ds can be used to divert sound from any AudioStreamPlayer2Ds they contain to specific buses. This makes it possible to create buses with different reverb or sound qualities to handle action happening in a particular parts of your game world.

This is a variant of AudioStreamPlayer, but emits sound in a 3D positional environment. Depending on the location of the player relative to the screen, it can position sound in stereo, 5.1 or 7.1 depending on the chosen audio setup.

Similar to AudioStreamPlayer2D, an Area3D can divert the sound to an audio bus.

Unlike for 2D, the 3D version of AudioStreamPlayer has a few more advanced options:

This feature is not supported on the web platform if the AudioStreamPlayer's playback mode is set to Sample, which is the default. It will only work if the playback mode is set to Stream, at the cost of increased latency if threads are not enabled.

See Audio playback in the Exporting for the Web documentation for details.

Godot allows for 3D audio streams that enter a specific Area3D node to send dry and wet audio to separate buses. This is useful when you have several reverb configurations for different types of rooms. This is done by enabling this type of reverb in the Reverb Bus section of the Area3D's properties:

At the same time, a special bus layout is created where each Area3D receives the reverb info from each Area3D. A Reverb effect needs to be created and configured in each reverb bus to complete the setup for the desired effect:

The Area3D's Reverb Bus section also has a parameter named Uniformity. Some types of rooms bounce sounds more than others (like a warehouse), so reverberation can be heard almost uniformly across the room even though the source may be far away. Playing around with this parameter can simulate that effect.

This feature is not supported on the web platform if the AudioStreamPlayer's playback mode is set to Sample, which is the default. It will only work if the playback mode is set to Stream, at the cost of increased latency if threads are not enabled.

See Audio playback in the Exporting for the Web documentation for details.

When the relative velocity between an emitter and listener changes, this is perceived as an increase or decrease in the pitch of the emitted sound. Godot can track velocity changes in the AudioStreamPlayer3D and Camera nodes. Both nodes have this property, which must be enabled manually:

Enable it by setting it depending on how objects will be moved: use Idle for objects moved using _process, or Physics for objects moved using _physics_process. The tracking will happen automatically.

Please read the User-contributed notes policy before submitting a comment.

---

## Importing audio samples

**URL:** https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_audio_samples.html

**Contents:**
- Importing audio samples
- Supported audio formats
- Importing audio samples
- Import options (WAV)
- Force > 8 Bit
- Force > Mono
- Force > Max Rate
- Edit > Trim
- Edit > Normalize
- Edit > Loop Mode

Godot provides 3 options to import your audio data: WAV, Ogg Vorbis and MP3.

Each format has different advantages:

WAV files use raw data or light compression (IMA ADPCM or Quite OK Audio). Currently they can only be imported in raw format, but Godot allows compression after import. They are lightweight to play back on the CPU (hundreds of simultaneous voices in this format are fine). The downside is that they take up a lot of disk space.

Ogg Vorbis files use a stronger compression that results in much smaller file size, but require significantly more processing power to play back.

MP3 files use better compression than WAV with IMA ADPCM or Quite OK Audio, but worse than Ogg Vorbis. This means that an MP3 file with roughly equal quality to Ogg Vorbis will be significantly larger. On the bright side, MP3 requires less CPU usage to play back compared to Ogg Vorbis.

If you've compiled the Godot editor from source with specific modules disabled, some formats may not be available.

Here is a comparative chart representing the file size of 1 second of audio with each format:

WAV 24-bit, 96 kHz, stereo

WAV 16-bit, 44 kHz, mono

WAV IMA ADPCM, 44 kHz, mono

Quite OK Audio, 44 kHz, mono

Ogg Vorbis 128 Kb/s, stereo

Ogg Vorbis 96 Kb/s, stereo

Note that the MP3 and Ogg Vorbis figures can vary depending on the encoding type. The above figures use CBR encoding for simplicity, but most Ogg Vorbis and MP3 files you can find online are encoded with VBR encoding which is more efficient. VBR encoding makes the effective audio file size depend on how "complex" the source audio is.

Consider using WAV for short and repetitive sound effects, and Ogg Vorbis for music, speech, and long sound effects. MP3 is useful for mobile and web projects where CPU resources are limited, especially when playing multiple compressed sounds at the same time (such as long ambient sounds).

Several options are available in the Import dock after selecting a WAV file in the FileSystem dock:

Import options in the Import dock after selecting a WAV file in the FileSystem dock

The set of options available after selecting an Ogg Vorbis or MP3 file is different:

Import options in the Import dock after selecting an MP3 file in the FileSystem dock. Options are identical for Ogg Vorbis files.

After importing a sound, you can play it back using the AudioStreamPlayer, AudioStreamPlayer2D or AudioStreamPlayer3D nodes. See Audio streams for more information.

If enabled, forces the imported audio to use 8-bit quantization if the source file is 16-bit or higher.

Enabling this is generally not recommended, as 8-bit quantization decreases audio quality significantly. If you need smaller file sizes, consider using Ogg Vorbis or MP3 audio instead.

If enabled, forces the imported audio to be mono if the source file is stereo. This decreases the file size by 50% by merging the two channels into one.

If set to a value greater than 0, forces the audio's sample rate to be reduced to a value lower than or equal to the value specified here.

This can decrease file size noticeably on certain sounds, without impacting quality depending on the actual sound's contents. See Best practices for more information.

The source audio file may contain long silences at the beginning and/or the end. These silences are inserted by DAWs when saving to a waveform, which increases their size unnecessarily and add latency to the moment they are played back.

Enabling Trim will automatically trim the beginning and end of the audio if it's lower than -50 dB after normalization (see Edit > Normalize below). A fade-in/fade-out period of 500 samples is also used during trimming to avoid audible pops.

If enabled, audio volume will be normalized so that its peak volume is equal to 0 dB. When enabled, normalization will make audio sound louder depending on its original peak volume.

Unlike Ogg Vorbis and MP3, WAV files can contain metadata to indicate whether they're looping (in addition to loop points). By default, Godot will follow this metadata, but you can choose to apply a specific loop mode:

Detect from WAV: Uses loop information from the WAV metadata.

Disabled: Don't loop audio, even if metadata indicates the file should be played back looping.

Forward: Standard audio looping. Plays the audio forward from the beginning to the loop end, then returns to the loop beginning and repeats.

Ping-Pong: Plays the audio forward until the loop end, then backwards to the loop beginning, repeating this cycle.

Backward: Plays the audio backwards from the loop end to the loop beginning, then repeats.

When choosing one of the Forward, Ping-Pong or Backward loop modes, loop points can also be defined to make only a specific part of the sound loop. Loop Begin is set in samples after the beginning of the audio file. Loop End is also set in samples after the beginning of the audio file, but will use the end of the audio file if set to -1.

In AudioStreamPlayer, the finished signal won't be emitted for looping audio when it reaches the end of the audio file, as the audio will keep playing indefinitely.

Three compression modes can be chosen from for WAV files: PCM (Uncompressed), IMA ADPCM, or Quite OK Audio (default). IMA ADPCM reduces file size and memory usage a little, at the cost of decreasing quality in an audible manner. Quite OK Audio reduces file size a bit more than IMA ADPCM and the quality decrease is much less noticeable, at the cost of slightly higher CPU usage (still much lower than MP3).

Ogg Vorbis and MP3 don't decrease quality as much and can provide greater file size reductions, at the cost of higher CPU usage during playback. This higher CPU usage is usually not a problem (especially with MP3), unless playing dozens of compressed sounds at the same time on mobile/web platforms.

If enabled, the audio will begin playing at the beginning after playback ends by reaching the end of the audio.

In AudioStreamPlayer, the finished signal won't be emitted for looping audio when it reaches the end of the audio file, as the audio will keep playing indefinitely.

The loop offset determines where audio will start to loop after playback reaches the end of the audio. This can be used to only loop a part of the audio file, which is useful for some ambient sounds or music. The value is determined in seconds relative to the beginning of the audio, so 0 will loop the entire audio file.

Only has an effect if Loop is enabled.

A more convenient editor for Loop Offset is provided in the Advanced import settings dialog, as it lets you preview your changes without having to reimport the audio.

The Beats Per Minute of the audio track. This should match the BPM measure that was used to compose the track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for BPM is provided in the Advanced import settings dialog, as it lets you preview your changes without having to reimport the audio.

The beat count of the audio track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for Beat Count is provided in the Advanced import settings dialog, as it lets you preview your changes without having to reimport the audio.

The number of bars within a single beat in the audio track. This is only relevant for music that wishes to make use of interactive music functionality , not sound effects.

A more convenient editor for Bar Beats is provided in the Advanced import settings dialog, as it lets you preview your changes without having to reimport the audio.

If you double-click an Ogg Vorbis or MP3 file in the FileSystem dock (or choose Advanced… in the Import dock), you will see a dialog appear:

Advanced dialog when double-clicking an Ogg Vorbis or MP3 file in the FileSystem dock

This dialog allows you to edit the audio's loop point with a real-time preview, in addition to the BPM, beat count and bar beats. These 3 settings are currently unused, but they will be used in the future for interactive music support (which allows smoothly transitioning between different music tracks).

Unlike WAV files, Ogg Vorbis and MP3 only support a "loop begin" loop point, not a "loop end" point. Looping can also be only be standard forward looping, not ping-pong or backward.

While keeping pristine-quality audio sources is important if you're performing editing, using the same quality in the exported project is not necessary. For WAV files, Godot offers several import options to reduce the final file size without modifying the source file on disk.

To reduce memory usage and file size, choose an appropriate quantization, sample rate and number of channels for your audio:

There's no audible benefit to using 24-bit audio, especially in a game where several sounds are often playing at the same time (which makes it harder to appreciate individual sounds).

Unless you are slowing down the audio at runtime, there's no audible benefit to using a sample rate greater than 48 kHz. If you wish to keep a source with a higher sample rate for editing, use the Force > Max Rate import option to limit the sample rate of the imported sound (only available for WAV files).

Many sound effects can generally be converted to mono as opposed to stereo. If you wish to keep a source with stereo for editing, use the Force > Mono import option to convert the imported sound to mono (only available for WAV files).

Voices can generally be converted to mono, but can also have their sample rate reduced to 22 kHz without a noticeable loss in quality (unless the voice is very high-pitched). This is because most human voices never go past 11 kHz.

Godot has an extensive bus system with built-in effects. This saves SFX artists the need to add reverb to the sound effects, reducing their size greatly and ensuring correct trimming.

As you can see above, sound effects become much larger in file size with reverb added.

Audio samples can be loaded and saved at runtime using runtime file loading and saving, including from an exported project.

Please read the User-contributed notes policy before submitting a comment.

---

## OggPacketSequencePlayback

**URL:** https://docs.godotengine.org/en/stable/classes/class_oggpacketsequenceplayback.html

**Contents:**
- OggPacketSequencePlayback
- User-contributed notes

Inherits: RefCounted < Object

There is currently no description for this class. Please help us by contributing one!

Please read the User-contributed notes policy before submitting a comment.

---

## Recording with microphone

**URL:** https://docs.godotengine.org/en/stable/tutorials/audio/recording_with_microphone.html

**Contents:**
- Recording with microphone
- The structure of the demo
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

Godot supports in-game audio recording for Windows, macOS, Linux, Android and iOS.

A simple demo is included in the official demo projects and will be used as support for this tutorial: https://github.com/godotengine/godot-demo-projects/tree/master/audio/mic_record.

You will need to enable audio input in the Audio > Driver > Enable Input project setting, or you'll just get empty audio files.

The demo consists of a single scene. This scene includes two major parts: the GUI and the audio.

We will focus on the audio part. In this demo, a bus named Record with the effect Record is created to handle the audio recording. An AudioStreamPlayer named AudioStreamRecord is used for recording.

The audio recording is handled by the AudioEffectRecord resource which has three methods: get_recording(), is_recording_active(), and set_recording_active().

At the start of the demo, the recording effect is not active. When the user presses the RecordButton, the effect is enabled with set_recording_active(true).

On the next button press, as effect.is_recording_active() is true, the recorded stream can be stored into the recording variable by calling effect.get_recording().

To playback the recording, you assign the recording as the stream of the AudioStreamPlayer and call play().

To save the recording, you call save_to_wav() with the path to a file. In this demo, the path is defined by the user via a LineEdit input box.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var effect
var recording


func _ready():
    # We get the index of the "Record" bus.
    var idx = AudioServer.get_bus_index("Record")
    # And use it to retrieve its first effect, which has been defined
    # as an "AudioEffectRecord" resource.
    effect = AudioServer.get_bus_effect(idx, 0)
```

Example 2 (gdscript):
```gdscript
private AudioEffectRecord _effect;
private AudioStreamSample _recording;

public override void _Ready()
{
    // We get the index of the "Record" bus.
    int idx = AudioServer.GetBusIndex("Record");
    // And use it to retrieve its first effect, which has been defined
    // as an "AudioEffectRecord" resource.
    _effect = (AudioEffectRecord)AudioServer.GetBusEffect(idx, 0);
}
```

Example 3 (typescript):
```typescript
func _on_record_button_pressed():
    if effect.is_recording_active():
        recording = effect.get_recording()
        $PlayButton.disabled = false
        $SaveButton.disabled = false
        effect.set_recording_active(false)
        $RecordButton.text = "Record"
        $Status.text = ""
    else:
        $PlayButton.disabled = true
        $SaveButton.disabled = true
        effect.set_recording_active(true)
        $RecordButton.text = "Stop"
        $Status.text = "Recording..."
```

Example 4 (json):
```json
private void OnRecordButtonPressed()
{
    if (_effect.IsRecordingActive())
    {
        _recording = _effect.GetRecording();
        GetNode<Button>("PlayButton").Disabled = false;
        GetNode<Button>("SaveButton").Disabled = false;
        _effect.SetRecordingActive(false);
        GetNode<Button>("RecordButton").Text = "Record";
        GetNode<Label>("Status").Text = "";
    }
    else
    {
        GetNode<Button>("PlayButton").Disabled = true;
        GetNode<Button>("SaveButton").Disabled = true;
        _effect.SetRecordingActive(true);
        GetNode<Button>("RecordButton").Text = "Stop";
        GetNode<Label>("Status").Text = "Recording...";
    }
}
```

---

## ResourceImporterMP3

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceimportermp3.html

**Contents:**
- ResourceImporterMP3
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: ResourceImporter < RefCounted < Object

Imports an MP3 audio file for playback.

MP3 is a lossy audio format, with worse audio quality compared to ResourceImporterOggVorbis at a given bitrate.

In most cases, it's recommended to use Ogg Vorbis over MP3. However, if you're using an MP3 sound source with no higher quality source available, then it's recommended to use the MP3 file directly to avoid double lossy compression.

MP3 requires more CPU to decode than ResourceImporterWAV. If you need to play a lot of simultaneous sounds, it's recommended to use WAV for those sounds instead, especially if targeting low-end devices.

Importing audio samples

The number of bars within a single beat in the audio track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for bar_beats is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

The beat count of the audio track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for beat_count is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

The beats per minute of the audio track. This should match the BPM measure that was used to compose the track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for bpm is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

If enabled, the audio will begin playing at the beginning after playback ends by reaching the end of the audio.

Note: In AudioStreamPlayer, the AudioStreamPlayer.finished signal won't be emitted for looping audio when it reaches the end of the audio file, as the audio will keep playing indefinitely.

float loop_offset = 0 

Determines where audio will start to loop after playback reaches the end of the audio. This can be used to only loop a part of the audio file, which is useful for some ambient sounds or music. The value is determined in seconds relative to the beginning of the audio. A value of 0.0 will loop the entire audio file.

Only has an effect if loop is true.

A more convenient editor for loop_offset is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

Please read the User-contributed notes policy before submitting a comment.

---

## ResourceImporterOggVorbis

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceimporteroggvorbis.html

**Contents:**
- ResourceImporterOggVorbis
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: ResourceImporter < RefCounted < Object

Imports an Ogg Vorbis audio file for playback.

Ogg Vorbis is a lossy audio format, with better audio quality compared to ResourceImporterMP3 at a given bitrate.

In most cases, it's recommended to use Ogg Vorbis over MP3. However, if you're using an MP3 sound source with no higher quality source available, then it's recommended to use the MP3 file directly to avoid double lossy compression.

Ogg Vorbis requires more CPU to decode than ResourceImporterWAV. If you need to play a lot of simultaneous sounds, it's recommended to use WAV for those sounds instead, especially if targeting low-end devices.

Importing audio samples

load_from_buffer(stream_data: PackedByteArray) static

load_from_file(path: String) static

The number of bars within a single beat in the audio track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for bar_beats is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

The beat count of the audio track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for beat_count is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

The beats per minute of the audio track. This should match the BPM measure that was used to compose the track. This is only relevant for music that wishes to make use of interactive music functionality, not sound effects.

A more convenient editor for bpm is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

If enabled, the audio will begin playing at the beginning after playback ends by reaching the end of the audio.

Note: In AudioStreamPlayer, the AudioStreamPlayer.finished signal won't be emitted for looping audio when it reaches the end of the audio file, as the audio will keep playing indefinitely.

float loop_offset = 0 

Determines where audio will start to loop after playback reaches the end of the audio. This can be used to only loop a part of the audio file, which is useful for some ambient sounds or music. The value is determined in seconds relative to the beginning of the audio. A value of 0.0 will loop the entire audio file.

Only has an effect if loop is true.

A more convenient editor for loop_offset is provided in the Advanced Import Settings dialog, as it lets you preview your changes without having to reimport the audio.

AudioStreamOggVorbis load_from_buffer(stream_data: PackedByteArray) static 

Deprecated: Use AudioStreamOggVorbis.load_from_buffer() instead.

Creates a new AudioStreamOggVorbis instance from the given buffer. The buffer must contain Ogg Vorbis data.

AudioStreamOggVorbis load_from_file(path: String) static 

Deprecated: Use AudioStreamOggVorbis.load_from_file() instead.

Creates a new AudioStreamOggVorbis instance from the given file path. The file must be in Ogg Vorbis format.

Please read the User-contributed notes policy before submitting a comment.

---

## ResourceImporterWAV

**URL:** https://docs.godotengine.org/en/stable/classes/class_resourceimporterwav.html

**Contents:**
- ResourceImporterWAV
- Description
- Tutorials
- Properties
- Property Descriptions
- User-contributed notes

Inherits: ResourceImporter < RefCounted < Object

Imports a WAV audio file for playback.

WAV is an uncompressed format, which can provide higher quality compared to Ogg Vorbis and MP3. It also has the lowest CPU cost to decode. This means high numbers of WAV sounds can be played at the same time, even on low-end devices.

By default, Godot imports WAV files using the lossy Quite OK Audio compression. You may change this by setting the compress/mode property.

Importing audio samples

int compress/mode = 2 

The compression mode to use on import.

PCM (Uncompressed): Imports audio data without any form of compression, preserving the highest possible quality. It has the lowest CPU cost, but the highest memory usage.

IMA ADPCM: Applies fast, lossy compression during import, noticeably decreasing the quality, but with low CPU cost and memory usage. Does not support seeking and only Forward loop mode is supported.

`Quite OK Audio <https://qoaformat.org/>`__: Also applies lossy compression on import, having a slightly higher CPU cost compared to IMA ADPCM, but much higher quality and the lowest memory usage.

int edit/loop_begin = 0 

The begin loop point to use when edit/loop_mode is Forward, Ping-Pong, or Backward. This is set in samples after the beginning of the audio file.

int edit/loop_end = -1 

The end loop point to use when edit/loop_mode is Forward, Ping-Pong, or Backward. This is set in samples after the beginning of the audio file. A value of -1 uses the end of the audio file as the end loop point.

int edit/loop_mode = 0 

Controls how audio should loop.

Detect From WAV: Uses loop information from the WAV metadata.

Disabled: Don't loop audio, even if the metadata indicates the file playback should loop.

Forward: Standard audio looping. Plays the audio forward from the beginning to edit/loop_end, then returns to edit/loop_begin and repeats.

Ping-Pong: Plays the audio forward until edit/loop_end, then backwards to edit/loop_begin, repeating this cycle.

Backward: Plays the audio backwards from edit/loop_end to edit/loop_begin, then repeats.

Note: In AudioStreamPlayer, the AudioStreamPlayer.finished signal won't be emitted for looping audio when it reaches the end of the audio file, as the audio will keep playing indefinitely.

bool edit/normalize = false 

If true, normalize the audio volume so that its peak volume is equal to 0 dB. When enabled, normalization will make audio sound louder depending on its original peak volume.

bool edit/trim = false 

If true, automatically trim the beginning and end of the audio if it's lower than -50 dB after normalization (see edit/normalize). This prevents having files with silence at the beginning or end, which increases their size unnecessarily and adds latency to the moment they are played back. A fade-in/fade-out period of 500 samples is also used during trimming to avoid audible pops.

bool force/8_bit = false 

If true, forces the imported audio to use 8-bit quantization if the source file is 16-bit or higher.

Enabling this is generally not recommended, as 8-bit quantization decreases audio quality significantly. If you need smaller file sizes, consider using Ogg Vorbis or MP3 audio instead.

bool force/max_rate = false 

If set to a value greater than 0, forces the audio's sample rate to be reduced to a value lower than or equal to the value specified in force/max_rate_hz.

This can decrease file size noticeably on certain sounds, without impacting quality depending on the actual sound's contents. See Best practices for more information.

float force/max_rate_hz = 44100 

The frequency to limit the imported audio sample to (in Hz). Only effective if force/max_rate is true.

bool force/mono = false 

If true, forces the imported audio to be mono if the source file is stereo. This decreases the file size by 50% by merging the two channels into one.

Please read the User-contributed notes policy before submitting a comment.

---

## Sync the gameplay with audio and music

**URL:** https://docs.godotengine.org/en/stable/tutorials/audio/sync_with_audio.html

**Contents:**
- Sync the gameplay with audio and music
- Introduction
- Using the system clock to sync
- Using the sound hardware clock to sync
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

In any application or game, sound and music playback will have a slight delay. For games, this delay is often so small that it is negligible. Sound effects will come out a few milliseconds after any play() function is called. For music this does not matter as in most games it does not interact with the gameplay.

Still, for some games (mainly, rhythm games), it may be required to synchronize player actions with something happening in a song (usually in sync with the BPM). For this, having more precise timing information for an exact playback position is useful.

Achieving very low playback timing precision is difficult. This is because many factors are at play during audio playback:

Audio is mixed in chunks (not continuously), depending on the size of audio buffers used (check latency in project settings).

Mixed chunks of audio are not played immediately.

Graphics APIs display two or three frames late.

When playing on TVs, some delay may be added due to image processing.

The most common way to reduce latency is to shrink the audio buffers (again, by editing the latency setting in the project settings). The problem is that when latency is too small, sound mixing will require considerably more CPU. This increases the risk of skipping (a crack in sound because a mix callback was lost).

This is a common tradeoff, so Godot ships with sensible defaults that should not need to be altered.

The problem, in the end, is not this slight delay but synchronizing graphics and audio for games that require it. Some helpers are available to obtain more precise playback timing.

As mentioned before, If you call AudioStreamPlayer.play(), sound will not begin immediately, but when the audio thread processes the next chunk.

This delay can't be avoided but it can be estimated by calling AudioServer.get_time_to_next_mix().

The output latency (what happens after the mix) can also be estimated by calling AudioServer.get_output_latency().

Add these two and it's possible to guess almost exactly when sound or music will begin playing in the speakers during _process():

In the long run, though, as the sound hardware clock is never exactly in sync with the system clock, the timing information will slowly drift away.

For a rhythm game where a song begins and ends after a few minutes, this approach is fine (and it's the recommended approach). For a game where playback can last a much longer time, the game will eventually go out of sync and a different approach is needed.

Using AudioStreamPlayer.get_playback_position() to obtain the current position for the song sounds ideal, but it's not that useful as-is. This value will increment in chunks (every time the audio callback mixed a block of sound), so many calls can return the same value. Added to this, the value will be out of sync with the speakers too because of the previously mentioned reasons.

To compensate for the "chunked" output, there is a function that can help: AudioServer.get_time_since_last_mix().

Adding the return value from this function to get_playback_position() increases precision:

To increase precision, subtract the latency information (how much it takes for the audio to be heard after it was mixed):

The result may be a bit jittery due how multiple threads work. Just check that the value is not less than in the previous frame (discard it if so). This is also a less precise approach than the one before, but it will work for songs of any length, or synchronizing anything (sound effects, as an example) to music.

Here is the same code as before using this approach:

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
var time_begin
var time_delay


func _ready():
    time_begin = Time.get_ticks_usec()
    time_delay = AudioServer.get_time_to_next_mix() + AudioServer.get_output_latency()
    $Player.play()


func _process(delta):
    # Obtain from ticks.
    var time = (Time.get_ticks_usec() - time_begin) / 1000000.0
    # Compensate for latency.
    time -= time_delay
    # May be below 0 (did not begin yet).
    time = max(0, time)
    print("Time is: ", time)
```

Example 2 (gdscript):
```gdscript
private double _timeBegin;
private double _timeDelay;

public override void _Ready()
{
    _timeBegin = Time.GetTicksUsec();
    _timeDelay = AudioServer.GetTimeToNextMix() + AudioServer.GetOutputLatency();
    GetNode<AudioStreamPlayer>("Player").Play();
}

public override void _Process(double delta)
{
    double time = (Time.GetTicksUsec() - _timeBegin) / 1000000.0d;
    time = Math.Max(0.0d, time - _timeDelay);
    GD.Print(string.Format("Time is: {0}", time));
}
```

Example 3 (gdscript):
```gdscript
var time = $Player.get_playback_position() + AudioServer.get_time_since_last_mix()
```

Example 4 (typescript):
```typescript
double time = GetNode<AudioStreamPlayer>("Player").GetPlaybackPosition() + AudioServer.GetTimeSinceLastMix();
```

---

## Text to speech

**URL:** https://docs.godotengine.org/en/stable/tutorials/audio/text_to_speech.html

**Contents:**
- Text to speech
- Basic Usage
- Requirements for functionality
  - Distro-specific one-liners
- Troubleshooting
- Best practices
- Caveats and Other Information
- User-contributed notes

Basic usage of text-to-speech involves the following one-time steps:

Enable TTS in the Godot editor for your project

Query the system for a list of usable voices

Store the ID of the voice you want to use

By default, the Godot project-level setting for text-to-speech is disabled, to avoid unnecessary overhead. To enable it:

Go to Project > Project Settings

Make sure the Advanced Settings toggle is enabled

Click on Audio > General

Ensure the Text to Speech option is checked

Restart Godot if prompted to do so.

Text-to-speech uses a specific voice. Depending on the user's system, they might have multiple voices installed. Once you have the voice ID, you can use it to speak some text:

Godot includes text-to-speech functionality. You can find these under the DisplayServer class.

Godot depends on system libraries for text-to-speech functionality. These libraries are installed by default on Windows, macOS, Web, Android and iOS, but not on all Linux distributions. If they are not present, text-to-speech functionality will not work. Specifically, the tts_get_voices() method will return an empty list, indicating that there are no usable voices.

Both Godot users on Linux and end-users on Linux running Godot games need to ensure that their system includes the system libraries for text-to-speech to work. Please consult the table below or your own distribution's documentation to determine what libraries you need to install.

If you get the error Invalid get index '0' (on base: 'PackedStringArray'). for the line var voice_id = voices[0], check if there are any items in voices. If not:

All users: make sure you enabled Text to Speech in project settings

Linux users: ensure you installed the system-specific libraries for text to speech

The best practices for text-to-speech, in terms of the ideal player experience for blind players, is to send output to the player's screen reader. This preserves the choice of language, speed, pitch, etc. that the user set, as well as allows advanced features like allowing players to scroll backward and forward through text. As of now, Godot doesn't provide this level of integration.

With the current state of the Godot text-to-speech APIs, best practices include:

Develop the game with text-to-speech enabled, and ensure that everything sounds correct

Allow players to control which voice to use, and save/persist that selection across game sessions

Allow players to control the speech rate, and save/persist that selection across game sessions

This provides your blind players with the most flexibility and comfort available when not using a screen reader, and minimizes the chance of frustrating and alienating them.

Expect delays when you call tts_speak and tts_stop. The actual delay time varies depending on both the OS and on your machine's specifications. This is especially critical on Android and Web, where some of the voices depend on web services, and the actual time to playback depends on server load, network latency, and other factors.

Non-English text works if the correct voices are installed and used. On Windows, you can consult the instructions in this article to enable additional language voices on Windows.

Non-ASCII characters, such as umlaut, are pronounced correctly if you select the correct voice.

Blind players use a number of screen readers, including JAWS, NVDA, VoiceOver, Narrator, and more.

Windows text-to-speech APIs generally perform better than their equivalents on other systems (e.g. tts_stop followed by tts_speak immediately speaks the new message).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
# One-time steps.
# Pick a voice. Here, we arbitrarily pick the first English voice.
var voices = DisplayServer.tts_get_voices_for_language("en")
var voice_id = voices[0]

# Say "Hello, world!".
DisplayServer.tts_speak("Hello, world!", voice_id)

# Say a longer sentence, and then interrupt it.
# Note that this method is asynchronous: execution proceeds to the next line immediately,
# before the voice finishes speaking.
var long_message = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur"
DisplayServer.tts_speak(long_message, voice_id)

# Immediately stop the current text mid-sentence and say goodbye instead.
DisplayServer.tts_stop()
DisplayServer.tts_speak("Goodbye!", voice_id)
```

Example 2 (csharp):
```csharp
// One-time steps.
// Pick a voice. Here, we arbitrarily pick the first English voice.
string[] voices = DisplayServer.TtsGetVoicesForLanguage("en");
string voiceId = voices[0];

// Say "Hello, world!".
DisplayServer.TtsSpeak("Hello, world!", voiceId);

// Say a longer sentence, and then interrupt it.
// Note that this method is asynchronous: execution proceeds to the next line immediately,
// before the voice finishes speaking.
string longMessage = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur";
DisplayServer.TtsSpeak(longMessage, voiceId);

// Immediately stop the current text mid-sentence and say goodbye instead.
DisplayServer.TtsStop();
DisplayServer.TtsSpeak("Goodbye!", voiceId);
```

Example 3 (unknown):
```unknown
pacman -S speech-dispatcher festival espeakup
```

---

## VideoStreamPlayback

**URL:** https://docs.godotengine.org/en/stable/classes/class_videostreamplayback.html

**Contents:**
- VideoStreamPlayback
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: Resource < RefCounted < Object

Internal class used by VideoStream to manage playback state when played from a VideoStreamPlayer.

This class is intended to be overridden by video decoder extensions with custom implementations of VideoStream.

_get_channels() virtual const

_get_length() virtual const

_get_mix_rate() virtual const

_get_playback_position() virtual const

_get_texture() virtual const

_is_paused() virtual const

_is_playing() virtual const

_seek(time: float) virtual

_set_audio_track(idx: int) virtual

_set_paused(paused: bool) virtual

_update(delta: float) virtual required

mix_audio(num_frames: int, buffer: PackedFloat32Array = PackedFloat32Array(), offset: int = 0)

int _get_channels() virtual const 

Returns the number of audio channels.

float _get_length() virtual const 

Returns the video duration in seconds, if known, or 0 if unknown.

int _get_mix_rate() virtual const 

Returns the audio sample rate used for mixing.

float _get_playback_position() virtual const 

Return the current playback timestamp. Called in response to the VideoStreamPlayer.stream_position getter.

Texture2D _get_texture() virtual const 

Allocates a Texture2D in which decoded video frames will be drawn.

bool _is_paused() virtual const 

Returns the paused status, as set by _set_paused().

bool _is_playing() virtual const 

Returns the playback state, as determined by calls to _play() and _stop().

void _play() virtual 

Called in response to VideoStreamPlayer.autoplay or VideoStreamPlayer.play(). Note that manual playback may also invoke _stop() multiple times before this method is called. _is_playing() should return true once playing.

void _seek(time: float) virtual 

Seeks to time seconds. Called in response to the VideoStreamPlayer.stream_position setter.

void _set_audio_track(idx: int) virtual 

Select the audio track idx. Called when playback starts, and in response to the VideoStreamPlayer.audio_track setter.

void _set_paused(paused: bool) virtual 

Set the paused status of video playback. _is_paused() must return paused. Called in response to the VideoStreamPlayer.paused setter.

void _stop() virtual 

Stops playback. May be called multiple times before _play(), or in response to VideoStreamPlayer.stop(). _is_playing() should return false once stopped.

void _update(delta: float) virtual required 

Ticks video playback for delta seconds. Called every frame as long as both _is_paused() and _is_playing() return true.

int mix_audio(num_frames: int, buffer: PackedFloat32Array = PackedFloat32Array(), offset: int = 0) 

Render num_frames audio frames (of _get_channels() floats each) from buffer, starting from index offset in the array. Returns the number of audio frames rendered, or -1 on error.

Please read the User-contributed notes policy before submitting a comment.

---

## VideoStreamPlayer

**URL:** https://docs.godotengine.org/en/stable/classes/class_videostreamplayer.html

**Contents:**
- VideoStreamPlayer
- Description
- Tutorials
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Control < CanvasItem < Node < Object

A control used for video playback.

A control used for playback of VideoStream resources.

Supported video formats are Ogg Theora (.ogv, VideoStreamTheora) and any format exposed via a GDExtension plugin.

Warning: On Web, video playback will perform poorly due to missing architecture-specific assembly optimizations.

get_stream_length() const

get_stream_name() const

get_video_texture() const

Emitted when playback is finished.

int audio_track = 0 

void set_audio_track(value: int)

int get_audio_track()

The embedded audio track to play.

bool autoplay = false 

void set_autoplay(value: bool)

If true, playback starts when the scene loads.

int buffering_msec = 500 

void set_buffering_msec(value: int)

int get_buffering_msec()

Amount of time in milliseconds to store in buffer while playing.

StringName bus = &"Master" 

void set_bus(value: StringName)

Audio bus to use for sound playback.

bool expand = false 

void set_expand(value: bool)

If true, the video scales to the control size. Otherwise, the control minimum size will be automatically adjusted to match the video stream's dimensions.

void set_loop(value: bool)

If true, the video restarts when it reaches its end.

bool paused = false 

void set_paused(value: bool)

If true, the video is paused.

float speed_scale = 1.0 

void set_speed_scale(value: float)

float get_speed_scale()

The stream's current speed scale. 1.0 is the normal speed, while 2.0 is double speed and 0.5 is half speed. A speed scale of 0.0 pauses the video, similar to setting paused to true.

void set_stream(value: VideoStream)

VideoStream get_stream()

The assigned video stream. See description for supported formats.

float stream_position 

void set_stream_position(value: float)

float get_stream_position()

The current position of the stream, in seconds.

void set_volume(value: float)

Audio volume as a linear value.

float volume_db = 0.0 

void set_volume_db(value: float)

float get_volume_db()

float get_stream_length() const 

The length of the current stream, in seconds.

String get_stream_name() const 

Returns the video stream's name, or "<No Stream>" if no video stream is assigned.

Texture2D get_video_texture() const 

Returns the current frame as a Texture2D.

bool is_playing() const 

Returns true if the video is playing.

Note: The video is still considered playing if paused during playback.

Starts the video playback from the beginning. If the video is paused, this will not unpause the video.

Stops the video playback and sets the stream position to 0.

Note: Although the stream position will be set to 0, the first frame of the video stream won't become the current frame.

Please read the User-contributed notes policy before submitting a comment.

---
