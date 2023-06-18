# stream-setup

If you like what you see (or hear), you can find my setup below. My microphone setup is kind of expensive because I wanted a microphone that was up and out of the way and could also reject noise from the room (very loud ambient in summer from air conditioner). My camera setup is just something with a reasonable price/quality balance that I did not spend much time researching.

Microphone hardware:
- Microphone: Deity S-Mic 2
- Shock mount: Rycote duo-lyre with pistol grip handle
- Preamplifier: TritonAudio FetHead Phantom In-Line
- XLR cable: Mogami Gold Studio XLR
- Audio interface: Scarlett Solo 3rd Gen

Camera hardware: Logitech Brio

Software:
- Open Broadcaster Software (OBS) Studio (microphone noise cancelling)
- OBS plugins: Move transition (first chat notification), Source Copy (in-game chat blur)
- Streamer.bot (first chat notification)
- NVIDIA Broadcast (camera background removal)
- SplitCam (allow camera as source for multiple consumers)
- VoiceMeeter Potato

Audio chain:
- Microphone: Microphone ➔ preamplifier ➔ audio interface ➔ OBS Studio
- Desktop/game: Source ➔ VoiceMeeter (virtual input 1) ➔ OBS Studio (monitoring VoiceMeeter)
- Voice communications: Source ➔ VoiceMeeter (virtual input 2) ➔ OBS Studio (monitoring VoiceMeeter)
- Excluded desktop audio (generally muted): Source ➔ VoiceMeeter (virtual input 3) ➔ OBS Studio (monitoring VoiceMeeter)

Video chain:
- Camera: Camera ➔ NVIDIA Broadcast ➔ OBS Studio (video capture device)
- Camera (if multiple consumers required): Camera ➔ NVIDIA Broadcast ➔ SplitCam ➔ OBS Studio (video capture device)
- Desktop/game: Source ➔ OBS Studio (game capture if working, otherwise display capture)

**OBS output to Twitch**

Twitch's maximum video bitrate (6,000Kbps for plebeians like me) is what dictates most settings, trying to find a workable balance for quality.
- Output (scaled) resolution: 1536x864 (bicubic)
- FPS: 48
- Video encoder: NVIDIA NVENC H.264
- Bitrate: 6,000Kbps (constant bitrate)
- Keyframe interval: 2s
- Quality preset: P6: Slower (better quality)
- Tuning: High quality
- Multipass mode: Two passes (quarter resolution)
- Profile: High
- "Look-ahead" and "Psycho visual tuning" enabled
- Max B-frames: 4
- Audio bitrate: 320Kbps

**Rejected/failed setup**
- NVIDIA Broadcast for microphone noise cancelling: I was getting occasional drops in the audio. I tried setting process priority set to "realtime", but that did not fix the issue.
