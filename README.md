# Chatterbox Multilingual – Text-to-Speech (TTS) Evaluation

## Overview

Chatterbox Multilingual is an open-source, neural, generative text-to-speech (TTS) model developed by **Resemble AI**. It supports multilingual speech synthesis and enables **voice conditioning via reference audio**, allowing flexible speaker control without relying on predefined speaker IDs.

This project evaluates Chatterbox Multilingual for **offline, predetermined interview-style speech generation**, with a focus on **audio quality, controllability, and batch-oriented execution**.

**Base repository:** https://github.com/resemble-ai/chatterbox  
**Modifications:** Custom batch generation, voice conditioning, and audio merging logic were added strictly for evaluation purposes. The core model code remains unmodified.

## Key Characteristics

| Attribute            | Details                                    |
| -------------------- | ------------------------------------------ |
| Type                 | Generative neural TTS                      |
| Execution            | Fully local (offline after model download) |
| Languages Supported  | Multilingual (Japanese, English, etc.)     |
| Voice Control        | Reference audio (voice prompting)          |
| Output Format        | WAV audio                                  |
| Hardware Requirement | CPU supported (GPU optional, faster)       |

## Evaluation Focus

- Offline batch audio generation  
- Predetermined interview or questionnaire scripts  
- Spoken-style Japanese input formatting  
- Female voice generation via reference audio  
- Restart-safe, reproducible execution  

## Observations & Issues

### 1. Audio Quality

- Spoken-style input with phonetic (kana-based) numbering consistently produces **clean, natural-sounding audio**.
- Written list-style input using Arabic numerals often introduces breathing-like noise during pauses and less stable prosody and rhythm.

Overall, spoken-style formatting yields noticeably higher and more consistent audio quality.

### 2. Hallucination & Content Control

As a fully generative model, Chatterbox may occasionally continue speaking beyond the intended text or produce unintended words or short phrases. For strict, predetermined scripts, this behavior necessitates **post-generation validation and trimming** to ensure the spoken output matches the input text exactly.

### 3. Input Formatting Sensitivity

Chatterbox demonstrates strong sensitivity to input formatting. Spoken-style, continuous sentences with natural punctuation yield the best results, while written lists, symbolic numbering, and excessive line breaks result in poorer output. In practice, input formatting has a greater impact on output quality than parameter tuning alone.

### 4. Performance & Resource Usage

The model operates on CPU with acceptable performance for batch generation tasks. GPU acceleration significantly improves throughput but is not required. The model is loaded once and reused across all generations.

### 5. Input Length Behavior

Speaking pace gradually increases as input length grows. This effect is caused by global prosody planning in single-pass generative TTS. Long-form text benefits from sentence-level chunking to maintain consistent pacing.

## Conclusion & Suitability Assessment

Chatterbox Multilingual delivers **high-quality, natural-sounding speech** when used with spoken-style input and reference audio for voice conditioning. Although trailing hallucinated speech and pause-related noise may occur, these issues can be effectively mitigated through sentence-level batch generation, careful input formatting, and post-processing and audio merging logic. Overall, Chatterbox Multilingual is well-suited for offline, predetermined interview systems, provided the generation pipeline enforces structured input and validation.

## Added / Modified Files

The following files were added to support evaluation and batch processing. No changes were made to the Chatterbox model architecture or training code.

### chatterbox_api.py

This file loads the Chatterbox Multilingual model once and exposes a simplified `generate_audio()` interface. It supports reference audio for voice conditioning, language selection, and seed-based reproducibility.

### generate_batch.py

This script reads a `.txt` input file, splits text into spoken-style sentences, generates one WAV file per sentence, skips existing files for restart-safe execution, and merges all generated audio into a single `final.wav`.

## How to Run

### Environment

Python 3.10–3.11 is recommended. The project supports Windows and Linux. CPU execution is supported, with optional GPU acceleration.

### Setup

```bash
python -m venv cbm_env
cbm_env\Scripts\activate
pip install torch numpy scipy
pip install git+https://github.com/resemble-ai/chatterbox.git
```

### Run Batch Generation

```bash
python generate_batch.py --input input.txt --output outputs --reference references/female.wav
```

### Output Structure

```text
outputs/
└── company_name_question_audios/
    ├── 1.wav
    ├── 2.wav
    ├── 3.wav
    ├── ...
    └── final.wav
```

## Project Folder Structure

```text
Chatterbox_MLM/
├── chatterbox/
│   ├── chatterbox_api.py
│   ├── generate_batch.py
│   └── ...
├── inputs/
│   ├── company_X.txt
│   └── ...
├── outputs/
│   ├── company_X_question_audios/
│   │   ├── 1.wav
│   │   ├── 2.wav
│   │   ├── ...
│   │   └── final.wav
│   └── ...
├── references/
│   ├── voiceF4.mp3
│   └── ...
└── README.md
```