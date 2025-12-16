# Chatterbox-TTS-Extended – TTS Evaluation & Observations

## Description
Chatterbox-TTS-Extended is a customizable text-to-speech system that offers extensive control over **voice selection, pitch, speaking rate, and other prosodic parameters**.  
It is designed for fast generation and experimentation, making it attractive for interactive or prototyping use cases.

This document summarizes observations made while evaluating Chatterbox-TTS-Extended for **Japanese text-to-speech generation**, particularly in the context of a **predetermined interview automation system**.

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

## Observations & Issues

### 1. Language Misinterpretation (Japanese → Mandarin)
- Japanese text written in kanji is frequently misinterpreted as **Mandarin Chinese**.
- Generated speech often contains phonetics resembling Mandarin (e.g., Chinese pronunciations rather than Japanese).
- This issue persists across multiple input formats.

---

### 2. No Strict Language Selection
- The system does **not provide a strict language lock or manual language switch**.
- Language detection is automatic and cannot be overridden by the user.
- This makes it unsuitable for scenarios where **language correctness is critical**.

---

### 3. Limited Multilingual Training Data
- Japanese support is **not native** and appears to be weakly supported.
- The model is not trained or optimized specifically for Japanese phonetics.
- Multilingual handling is inconsistent and unreliable.

---

### 4. Internet Dependency
- The model requires an **active internet connection**.
- This limits its use in fully offline environments.
- Network dependency introduces latency and deployment constraints.

---

### 5. Output Quality for Japanese
- Generated audio for Japanese inputs is **not intelligible**.
- Speech does not resemble natural or correct Japanese pronunciation.
- Output quality remains poor even when attempts are made to guide pronunciation.

---

## Input Variations Tested

The same Japanese content was tested using three different input strategies:

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
In all three cases, the generated audio failed to correctly recognize the text as Japanese.  
The output remained non-Japanese and largely unintelligible.

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

Although Chatterbox-TTS-Extended offers **fast generation and extensive voice customization**, its **lack of strict language control**, **poor Japanese support**, and **frequent misinterpretation of Japanese text as Mandarin** make it unsuitable for Japanese TTS applications.

In particular, it is **not suitable for a predetermined interview automation system**, where:
- Language correctness is critical
- Output must be intelligible and consistent
- Offline or controlled deployment is required

Chatterbox-TTS-Extended may be better suited for:
- English-centric applications
- Experimental or demo systems
- Scenarios where language precision is not critical

---

## Summary Statement

> Despite strong customization and performance advantages, Chatterbox-TTS-Extended is not viable for Japanese TTS due to unreliable language detection and unintelligible output.
