Chatterbox Multilingual – Text-to-Speech (TTS) Evaluation
Overview

Chatterbox Multilingual is an open-source, neural, generative text-to-speech (TTS) model developed by Resemble AI. It supports multilingual speech synthesis and enables voice conditioning via reference audio, allowing flexible speaker control without relying on predefined speaker IDs.

This project evaluates Chatterbox Multilingual for offline, predetermined interview-style speech generation, with a focus on audio quality, controllability, and batch-oriented execution.

Base repository: https://github.com/resemble-ai/chatterbox

Modifications: Custom batch generation, voice conditioning, and audio merging logic were added strictly for evaluation purposes. The core model code remains unmodified.

Key Characteristics
Attribute	Details
Type	Generative neural TTS
Execution	Fully local (offline after model download)
Languages Supported	Multilingual (Japanese, English, etc.)
Voice Control	Reference audio (voice prompting)
Output Format	WAV audio
Hardware Requirement	CPU supported (GPU optional, faster)
Evaluation Focus

The evaluation concentrates on practical usage for controlled speech generation scenarios:

Offline batch audio generation

Predetermined interview or questionnaire scripts

Spoken-style Japanese input formatting

Female voice generation via reference audio

Restart-safe, reproducible execution

Observations & Issues
1. Audio Quality

Spoken-style input with phonetic (kana-based) numbering consistently produces clean, natural-sounding audio.

Written list-style input using Arabic numerals often introduces:

Breathing-like noise during pauses

Less stable prosody and rhythm

Overall, spoken-style formatting yields noticeably higher and more consistent audio quality.

2. Hallucination & Content Control

As a fully generative model, Chatterbox may occasionally:

Continue speaking beyond the intended text

Produce unintended words or short phrases

For strict, predetermined scripts, this behavior necessitates post-generation validation and trimming to ensure the spoken output matches the input text exactly.

3. Input Formatting Sensitivity

Chatterbox demonstrates strong sensitivity to input formatting:

Best results: Spoken-style, continuous sentences with natural punctuation

Poorer results: Written lists, symbolic numbering, excessive line breaks

In practice, input formatting has a greater impact on output quality than parameter tuning alone.

4. Performance & Resource Usage

Operates on CPU with acceptable performance for batch generation tasks

GPU acceleration significantly improves throughput but is not required

The model is loaded once and reused across all generations

5. Input Length Behavior

Speaking pace gradually increases as input length grows

This effect is caused by global prosody planning in single-pass generative TTS

Long-form text benefits from sentence-level chunking to maintain consistent pacing

Conclusion & Suitability Assessment

Chatterbox Multilingual delivers high-quality, natural-sounding speech when used with spoken-style input and reference audio for voice conditioning.

Although trailing hallucinated speech and pause-related noise may occur, these issues can be effectively mitigated through:

Sentence-level batch generation

Careful input formatting

Post-processing and audio merging logic

Overall, Chatterbox Multilingual is well-suited for offline, predetermined interview systems, provided the generation pipeline enforces structured input and validation.

Added / Modified Files

The following files were added to support evaluation and batch processing. No changes were made to the Chatterbox model architecture or training code.

chatterbox_api.py

Loads the Chatterbox Multilingual model once

Exposes a simplified generate_audio() interface

Supports:

Reference audio for voice conditioning

Language selection

Seed-based reproducibility

generate_batch.py

Reads a .txt input file

Splits text into spoken-style sentences

Generates one WAV file per sentence

Skips existing files (restart-safe execution)

Merges all generated audio into a single final.wav

How to Run
Environment

Python: 3.10–3.11 recommended

Operating System: Windows / Linux

Hardware: CPU supported, GPU optional

Setup
python -m venv cbm_env
cbm_env\Scripts\activate   # Windows

pip install torch numpy scipy
pip install git+https://github.com/resemble-ai/chatterbox.git

Run Batch Generation
python generate_batch.py \
  --input input.txt \
  --output outputs \
  --reference references/female.wav

Output Structure
outputs/
└── company_name_question_audios/
    ├── 1.wav
    ├── 2.wav
    ├── 3.wav
    ├── ...
    └── final.wav

Project Folder Structure
Chatterbox_MLM/
├── chatterbox/                     # Base Chatterbox repository
│   ├── chatterbox_api.py           # Wrapper API for Chatterbox audio generation
│   ├── generate_batch.py           # Batch TTS generation and audio merging script
│   └── ...                         # Other original Chatterbox files
├── inputs/                         # Input text files
│   ├── company_X.txt
│   └── ...
├── outputs/                        # Generated audio outputs
│   ├── company_X_question_audios/
│   │   ├── 1.wav
│   │   ├── 2.wav
│   │   ├── ...
│   │   └── final.wav
│   └── ...
├── references/                     # Reference voice audio files
│   ├── voiceF4.mp3
│   └── ...
└── README.md                       # Project documentation
