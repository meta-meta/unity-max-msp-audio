# unity-max-msp-audio
This will be a Max external which sends audio to Unity AudioSource(s) for spatialized generative audio.

## Very early planning stages

[Unity Native Audio Plugin](https://docs.unity3d.com/Manual/AudioMixerNativeAudioPlugin.html)

[Max Devkit](https://github.com/Cycling74/max-devkit)

[Max SDK](https://github.com/cycling74/max-sdk) (deprecated?)

* in Max, [UnityAudioSend audioSourceId] object
* in Unity, MaxAudioReceiver component
  - implements AudioSource
  - takes audioSourceId to receive individual audio stream from max
* communication
  - https://www.boost.org/doc/libs/1_68_0/doc/html/interprocess.html
  - https://www.boost.org/doc/libs/1_68_0/doc/html/circular_buffer.html
 
## Demo Goal - dynamic instantiation/destruction of generative audio objects
* Unity sends OSC message at instantiation of Gameobject with MaxAudioReceiver component
  - some type indicating what instrument/patch to instantiate in Max
  - some uniqueId to send/receive messages about the state of this shared object
  - send an OSC message to destroy the object
* Max recieves OSC
  - dynamically instantiates patch connected to [UnityAudioSend uniqueId]
  - subsequent OSC messages are routed to this instance based on uniqueId
  - destroys the patch when receiving OSC message to destroy
