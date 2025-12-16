# Suno Bark – Text-to-Speech (TTS) Evaluation

## Description
Bark is an open-source, transformer-based **generative text-to-speech (TTS)** model developed by Suno AI.  
Unlike rule-based or API-driven TTS systems, Bark generates speech in a fully generative manner, enabling expressive prosody, emotion, and speaker variation.

This repository evaluates Bark specifically for **offline, predetermined interview-style speech generation**.

**Base repository:** https://github.com/suno-ai/bark  
**Modification:** A single evaluation script (`run_bark.py`) was added for controlled testing.

---

## Key Characteristics

| Attribute | Details |
|---------|--------|
| **Type** | Generative neural TTS |
| **Execution** | Fully local (offline after model download) |
| **Languages Supported** | Multilingual (including Japanese) |
| **Output Format** | WAV audio |
| **Hardware Requirement** | GPU recommended (CPU extremely slow) |

---

## Observations & Issues

### 1. Audio Quality Issues
- Background noise and echo are present in many available voice presets.
- Noise characteristics vary between speakers, leading to inconsistent audio quality.
- Post-processing (noise reduction, trimming) is often required to reach acceptable quality.

### 2. Hallucination & Content Control
Bark is a **fully generative model**, which results in:
- Unintended additional words or phrases not present in the input text.
- Changes in intonation or emphasis that were not explicitly specified.

This behavior makes Bark unsuitable for **strict, predetermined scripts**, where exact wording is critical.

### 3. Performance & Resource Constraints
- **Extremely slow on CPU** (≈4–5 minutes per sentence).
- GPU acceleration is strongly recommended.
- High computational cost limits scalability for offline or batch generation.

### 4. Input Length Limitations
- The model struggles with long-form text.
- Audio generation frequently cuts off mid-sentence.
- Longer inputs require manual chunking.
- No reliable guarantee of complete output for multi-sentence prompts.

### 5. Audio Timing Issues
- Generated audio frequently contains long trailing silence (**silence tail**).
- Spoken content is often much shorter than the total audio duration.
- Requires trimming and fade-out logic as part of post-processing.

---

## Conclusion & Suitability Assessment
While Bark demonstrates strong expressive capabilities and natural prosody, its **generative nature introduces unpredictability** in content, timing, and audio quality.

Due to audio artifacts, hallucinations, silence tails, slow CPU performance, and poor handling of long text, **Bark is not suitable for an offline, predetermined interview system** where consistency and accuracy are critical.

---

## Recommended Use Cases
Bark is better suited for:
- Conversational agents
- Storytelling systems
- Creative or exploratory voice applications

where expressive variation is more important than strict control.

---

## Added File

### `run_bark.py`
A custom evaluation script added for:
- Controlled text input
- Runtime measurement
- Post-processing (trailing silence trimming and fade-out)
- Japanese voice preset evaluation

The script does **not modify the Bark model itself**, only the execution workflow.

---

## How to Run

### Environment
- **Python:** 3.9 – 3.10 recommended
- **Hardware:** CUDA-enabled GPU strongly recommended

### Setup
```bash
python -m venv bark_env
source bark_env/bin/activate   # Linux / macOS
bark_env\Scripts\activate    # Windows
```

### Install
```bash
pip install torch numpy scipy
pip install git+https://github.com/suno-ai/bark.git
```

### Run
```bash
python run_bark.py
```

The script generates audio, applies trimming and fade-out, and saves `out.wav`.

---

## Reference
Official Bark repository:  
https://github.com/suno-ai/bark
