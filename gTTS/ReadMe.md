# gTTS (Google Text-to-Speech)

## Description
gTTS (Google Text-to-Speech) is a lightweight, Python-based text-to-speech library that converts text into natural-sounding speech using Google’s online TTS service.  
It is easy to use, language-flexible, and suitable for quick prototyping or simple TTS requirements.

---

## Key Characteristics

| Attribute | Details |
|---------|--------|
| **Type** | Rule-based / API-driven TTS (non-generative) |
| **Languages Supported** | Multiple (including English and Japanese) |
| **Output Format** | wav audio |
| **Latency** | Fast for short and medium-length text |
| **Hardware Requirement** | CPU only |

---

## Strengths
- Simple and reliable speech generation  
- Minimal setup and dependencies  
- No hallucination or extra spoken content  
- Predictable and consistent output  
- Suitable for predefined interview scripts  

---

## Limitations
- Requires an active internet connection  
- Limited control over voice style, pitch, and emotion  
- No speaker variation or voice cloning  
- Not suitable for fully offline deployment  

---

## Reference Files

The `generated_audio/` folder contains sample MP3 files generated using gTTS.

These samples are provided for:
- Audio quality reference  
- Pronunciation clarity checks  
- Baseline comparison with other TTS models  

---

## Use Case Note
gTTS is best suited for **static and predetermined speech generation**, such as interview questions or instructional prompts, and serves as a reliable baseline model for evaluation.
