# stream-setup

If you like what you see (or hear), you can find my setup below. My microphone setup is kind of expensive because I wanted a microphone that was up and out of the way and could also reject noise from the room (very loud ambient in summer from air conditioner). My camera setup is just something with a reasonable price/quality balance that I did not spend much time researching.

## Hardware
Microphone hardware:
- Microphone: Deity S-Mic 2
- Shock mount: Rycote duo-lyre with pistol grip handle
- Preamplifier: TritonAudio FetHead Phantom In-Line
- XLR cable: Mogami Gold Studio XLR
- Audio interface: Scarlett Solo 3rd Gen

Camera hardware: Logitech Brio

## Software
- Open Broadcaster Software (OBS) Studio (microphone noise cancelling)
- OBS plugins: Move transition (first chat notification), Source Copy (in-game chat blur)
- Streamer.bot (first chat notification)
- NVIDIA Broadcast (camera background removal)
- VoiceMeeter Potato

## Audio chain
- Microphone: Microphone ➔ preamplifier ➔ audio interface ➔ OBS Studio
- Game: Source ➔ VoiceMeeter (virtual input 3) ➔ OBS Studio (monitoring VoiceMeeter) (in Windows, I manually set games to send their audio to input 3, this is intended to prevent desktop audio from ever unintentionally ending up on stream)
- Voice communications: Source ➔ VoiceMeeter (virtual input 2) ➔ OBS Studio (monitoring VoiceMeeter)
- Excluded desktop audio (generally muted): Source ➔ VoiceMeeter (virtual input 1) ➔ OBS Studio (monitoring VoiceMeeter)

## Video chain
- Camera: Camera ➔ NVIDIA Broadcast ➔ OBS Studio (video capture device)
- Game: Source ➔ OBS Studio (game capture)

## OBS output to Twitch
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

## OBS camera configuration
Consuming, processing, and reusing the camera source:
- Camera scene: All camera sources scaled down to canvas size (for me, NVIDIA Broadcast and Logitech BRIO), with only the desired camera visible.
- Virtual camera scene: Camera scene as a source (nested scene), media source backgrounds (only set one to visible), and a solid colour background as bottom source. Media source background properties as "Loop" enabled, "Restart playback […]" disabled, "Show nothing […]" disabled, and "Close file when inactive" enabled. The desirable attributes of the result is that the virtual camera scene will use the same camera as the stream (if streaming), we do not need to re-process the source for background removal (it happens in the camera scene if not externalised to NVIDIA Broadcast), we can have any number of animated/media backgrounds pre-configured but they do not need to waste resources, we have a fallback background if something goes wrong with the media source.
- Configure OBS virtual camera output type to scene and output selection to be the virtual camera scene.
- Stream scenes with camera: Camera scene as a source (nested scene).

We can now have nice backgrounds in other applications via the OBS virtual camera and a transparent background while we stream, and we only need to do background removal once.

Quick camera resize:
- Add Move Source (Move transition plugin) filter to the scene where the camera scene is nested. Set the transform to preferred big size. Set the start trigger to "None: […] use a hotkey or next move […]". Set the stop trigger to "None: stop only when the move is done […]". Set next move to "Reverse". Set next move on to "Hotkey".
- Settings ➔ Hotkeys ➔ Find the name of the Move source filter you created, and set a hotkey.

We can now resize the camera as a hotkey toggle. **However**, we do need to remember to **toggle back to the initial size/state before exiting OBS**, or both the size and toggle will be messed up on next OBS launch.

## Past setups
Rejected/failed setup
- NVIDIA Broadcast for microphone noise cancelling: I was getting occasional drops in the audio. I tried setting process priority set to "realtime", but that did not fix the issue.
- OBS NVIDIA background removal plugin: I found that this had noticeably more flickering around the edges than the NVIDIA Broadcast software.

Deprecated setup
- SplitCam to allow camera as source for multiple consumers: I have switched to having a camera scene and virtual camera scene in OBS. There was nothing wrong with SplitCam, I just think this more convenient from a video chain perspective (only one path), fixes the "issue" of SplitCam's output not having a transparent background (assuming it received one by having NVIDIA Broadcast as its source), and allows me to control my background in video calls.
