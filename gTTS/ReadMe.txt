gTTS (Google Text-to-Speech) – Model Overview
Description

gTTS (Google Text-to-Speech) is a lightweight, Python-based text-to-speech library that converts text into natural-sounding speech using Google’s online TTS service. It is easy to use, language-flexible, and suitable for quick prototyping or simple TTS requirements.

Key Characteristics

Type: Rule-based / API-driven TTS (non-generative)

Languages Supported: Multiple (including English and Japanese)

Output Format: MP3 audio

Latency: Fast for short and medium-length text

Hardware Requirement: CPU only

Strengths

Simple and reliable speech generation

Minimal setup and dependencies

No hallucination or extra spoken content

Consistent and predictable outputs

Suitable for offline evaluation of interview scripts (once audio is generated)

Limitations

Requires an active internet connection

Limited control over voice style, pitch, and emotion

Cannot generate expressive or conversational speech

No speaker variation or voice cloning support

Use Case Suitability

gTTS is well-suited for:

Predefined interview questions

Static prompts and instructions

Prototyping TTS pipelines

Baseline comparison against generative TTS models

It is not suitable for:

Fully offline deployment

Highly expressive or interactive dialogue systems

Reference Files

The project includes a folder of generated audio files created using gTTS for reference.
These files demonstrate:

Pronunciation clarity

Output consistency

Timing and pacing for predefined interview questions

The generated samples can be used for:

Audio quality comparison

Integration testing

Baseline evaluation against other TTS models
