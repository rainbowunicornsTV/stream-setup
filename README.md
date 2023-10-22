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
- Game: Source ➔ VoiceMeeter (virtual input 3) ➔ OBS Studio (monitoring VoiceMeeter) (in Windows, I manually set games to send their audio to input 3, this is intended to prevent desktop audio from ever unintentionally ending up on stream)
- Voice communications: Source ➔ VoiceMeeter (virtual input 2) ➔ OBS Studio (monitoring VoiceMeeter)
- Excluded desktop audio (generally muted): Source ➔ VoiceMeeter (virtual input 1) ➔ OBS Studio (monitoring VoiceMeeter)

Video chain:
- Camera: Camera ➔ NVIDIA Broadcast ➔ OBS Studio (video capture device)
- Camera (if multiple consumers required): Camera ➔ NVIDIA Broadcast ➔ SplitCam ➔ OBS Studio (video capture device)
- Game: Source ➔ OBS Studio (game capture)

**OBS output to Twitch**

Due to no re-encoding/quality options, I am targeting 6,000Kbps video bitrate (Twitch recommended, better for poor connections/devices), trying to find a workable balance for quality.
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
- OBS NVIDIA background removal plugin: I found that this had noticeably more flickering around the edges than the NVIDIA Broadcast software.
