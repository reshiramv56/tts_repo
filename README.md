# Chatterbox-TTS-Extended – TTS Evaluation & Observations

## Description
Chatterbox-TTS-Extended is a customizable text-to-speech system that offers extensive control over **voice selection, pitch, speaking rate, and other prosodic parameters**.  
It is designed for fast generation and experimentation, making it attractive for interactive or prototyping use cases.

This document summarizes observations made while evaluating Chatterbox-TTS-Extended for **Japanese text-to-speech generation**, particularly in the context of a **predetermined interview automation system**.

**Base repository:** https://github.com/petermg/Chatterbox-TTS-Extended  
**Modification:** One small compatibility fix was applied to the original codebase. All other files and logic remain unchanged.

---

## Key Characteristics

| Attribute | Details |
|--------|---------|
| **TTS Type** | Neural TTS |
| **Customization** | High (voice, pitch, speed, style) |
| **Generation Speed** | Fast |
| **Execution** | Online / Internet-dependent |
| **Language Handling** | Automatic language detection |
| **Japanese Support** | Limited / not native |

---

## Strengths
- High degree of customization (voice, pitch, speaking rate, etc.)
- Fast audio generation compared to large generative models
- Suitable for experimentation and interactive demos
- Flexible configuration options

---

## Installation

### Prerequisites
- **Python:** 3.9 – 3.10 recommended  
- **Internet connection:** Required  
- **OS:** Windows / Linux / macOS  

### Setup
```bash
python -m venv cb_env
source cb_env/bin/activate        # Linux / macOS
cb_env\Scripts\activate         # Windows
```

### Install Dependencies
```bash
pip install -r requirements.txt
```
> Note: Internet access is required during execution.

---

## Code Modification Note

### Change Summary
A **minor compatibility fix** was applied to the original repository to resolve a runtime error during audio generation.  
No architectural changes, model changes, or generation logic changes were made.

### Issue Identified
During audio generation, the application failed with:
```
TypeError: ChatterboxTTS.generate() got an unexpected keyword argument 'apply_watermark'
```

This occurred even though:
- The Gradio UI launched successfully
- The model loaded without errors

### Root Cause
The UI code (`Chatter.py`) passed the parameter `apply_watermark` to:
- `ChatterboxTTS.generate()`
- `ChatterboxVC.generate()`

However, the installed backend version:
```
chatterbox-tts == 0.1.6
```
does **not define or accept** the `apply_watermark` argument.

This API mismatch caused all generation attempts to fail before synthesis.

### Resolution Implemented
- Removed the unsupported keyword argument:
  ```python
  apply_watermark=not disable_watermark
  ```
- The removal was applied to:
  - All `model.generate(...)` calls (TTS)
  - All `vc_model.generate(...)` calls (Voice Conversion)

No other parameters or logic were modified.

### Modified File
- `Chatter.py` (updated and added to this repository)

---

## Observations & Issues

### 1. Language Misinterpretation (Japanese)
- The model frequently fails to correctly interpret Japanese text written in kanji.
- Generated speech does not resemble natural or correct Japanese pronunciation.
- This issue occurs regardless of input formatting or pronunciation guidance.

---

### 2. No Strict Language Selection
- No manual language lock or explicit language parameter.
- Automatic language detection cannot be overridden.

---

### 3. Limited Multilingual Training Data
- Japanese support is not native.
- Multilingual handling is inconsistent and unreliable.

---

### 4. Internet Dependency
- Requires an active internet connection.
- Not suitable for fully offline environments.

---

### 5. Output Quality for Japanese
- Generated audio is **not intelligible Japanese**.
- Guiding pronunciation using kana does not resolve the issue.

---

## Input Variations Tested

### A. Standard Kanji Input
```
1. 協力し合うことで成果が出ると感じる。
2. 約束の時間に遅れることが多い。
```

### B. Kana-Guided Input
```
1. きょうりょくし合うことで成果が出ると感じる。
2. 約束（やくそく）の時間に遅れることが多い。
```

### C. Full Kana Input
```
いち、きょうりょくしあうことで せいかがでるとかんじる。
に、やくそくのじかんに おくれることがおおい。
```

**Result:**  
All input strategies failed to produce intelligible Japanese output.


### D. Full Romaji Input
```
Ichi, kyōryoku shiau koto de seika ga deru to kanjiru.
Ni, yakusoku no jikan ni okureru koto ga ōi.
```

**Result:**  
The model is able to generate audio when the input is provided in romaji.  
However, the pronunciation and prosody are **not natural-sounding Japanese**, and the output quality remains unsuitable for production or interview use.


---

## Suitability Assessment

| Requirement | Suitability |
|-----------|------------|
| Japanese Language Accuracy | ❌ |
| Language Control | ❌ |
| Offline Deployment | ❌ |
| Fast Generation | ✅ |
| Voice Customization | ✅ |

---

## Conclusion
Despite strong customization and fast generation, Chatterbox-TTS-Extended is **not suitable for Japanese TTS** due to unreliable language detection and unintelligible output.

It is therefore **not suitable for a predetermined interview automation system**, where language accuracy and consistency are critical.

---

## Summary Statement
> Chatterbox-TTS-Extended offers strong customization and speed, but due to limited Japanese support and lack of language control, it is not viable for Japanese TTS use cases.
