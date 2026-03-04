# Real-Time Multilingual Captioning for Deaf/Hard-of-Hearing Users via LLMs

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/colabre2020/multilingual-captioning/blob/main/Multilingual_Captioning_Demo.ipynb)
[![Paper](https://img.shields.io/badge/Paper-Web4All%202026-blue)](https://www.w4a.info/2026/)

**Authors:** Bhumika Shah, Satya Narayana Panda

---

## Overview

This repository contains the implementation and demonstration code for our Web4All 2026 communication paper on real-time multilingual captioning for deaf and hard-of-hearing (D/HoH) users using Large Language Models (LLMs).

Current captioning systems predominantly operate within monolingual frameworks, creating barriers for D/HoH individuals in multilingual environments. Our system addresses these limitations by leveraging LLMs for context-aware multilingual translation, code-switching support, and real-time caption generation.

## System Architecture

The pipeline integrates four key components:

1. **Audio Capture & Preprocessing** - 16 kHz sampling with voice activity detection
2. **ASR Transcription** - Whisper-based multilingual speech recognition with timestamps
3. **LLM-based Translation** - Context-aware multilingual translation and caption refinement
4. **Caption Rendering** - WebVTT-formatted output with latency-aware synchronization

## Key Features

- **Multilingual Support** - English, Spanish, French, Hindi, Chinese, Arabic
- **Code-Switching Detection** - Handles alternating languages within discourse
- **Real-Time Processing** - End-to-end latency 2.4s - 3.5s
- **WebVTT Compatible** - Standard format for web platform integration
- **Context-Aware Translation** - Maintains terminology consistency
- **Evaluation Framework** - BLEU scores and latency analysis

## Interactive Demo

**[Open Interactive Notebook in Google Colab](https://colab.research.google.com/github/colabre2020/multilingual-captioning/blob/main/Multilingual_Captioning_Demo.ipynb)**

The Colab notebook provides a complete implementation including:
- ASR pipeline setup
- **OpenRouter API integration** for accessing multiple LLMs (GPT-4, Claude, Gemini, Llama)
- LLM translation with context awareness
- Local translation model fallback
- Code-switching detection
- WebVTT caption generation
- Performance evaluation metrics
- Visualization tools

## Quick Start

### Option 1: Google Colab (Recommended)

Click the "Open in Colab" badge above to run the notebook directly in your browser. No installation required!

### Option 2: Local Setup

```bash
# Clone the repository
git clone https://github.com/colabre2020/multilingual-captioning.git
cd multilingual-captioning

# Install dependencies
pip install openai-whisper transformers torch torchaudio
pip install openai anthropic webvtt-py
pip install evaluate sacrebleu nltk

# Open the notebook
jupyter notebook Multilingual_Captioning_Demo.ipynb
```

## Preliminary Results

### Translation Quality (BLEU Scores)
- English → Spanish: 0.52 - 0.68
- English → French: 0.48 - 0.61
- English → Hindi: 0.42 - 0.55

### Latency Performance
- Mean end-to-end: **2.4s** (English-Spanish)
- 95th percentile: **< 3.5s**
- Within real-time threshold: **~85%** of segments

### Code-Switching
- Successfully handles English-Spanish code-switching
- Maintains contextual coherence across language boundaries
- Rapid transitions (multiple per sentence) require further refinement

## Repository Structure

```
multilingual-captioning/
├── Multilingual_Captioning_Demo.ipynb    # Interactive demo notebook
├── README.md                              # This file
├── ACM_Conference_Proceedings_Primary_Article_Template/
│   ├── paper.tex                         # LaTeX source
│   ├── paper.pdf                         # Compiled paper
│   └── refs.bib                          # Bibliography
└── ResearchDetails.txt                   # Project notes
```

## Hardware Requirements & Platform Support

This implementation has been tested and optimized for multiple hardware accelerators:

- **Google Cloud TPU** - Optimal for Colab TPU runtime
- **NVIDIA GPU (CUDA)** - Tested on various CUDA-enabled GPUs
- **Apple Silicon (M1/M2/M3)** - Native MPS acceleration support
- **CPU Fallback** - Works on any system (slower performance)

The notebook automatically detects and configures the best available accelerator. For optimal real-time performance, we recommend:
- Google Colab with T4 GPU or TPU v2
- Local GPU with ≥8GB VRAM
- Apple M1 Pro/Max or M2 for local development

## Requirements

- Python 3.8+
- PyTorch 2.0+
- OpenAI Whisper
- Transformers (HuggingFace)
- **OpenRouter API** - Integrated for accessing multiple LLMs (GPT-4, Claude, Gemini, Llama)
  - API key included in demo notebook
  - Supports switching between different LLM providers
- Local translation models as fallback

## Usage Example

```python
from multilingual_captioning import MultilingualCaptioningPipeline

# Initialize pipeline with OpenRouter API
pipeline = MultilingualCaptioningPipeline(
    source_lang="en",
    target_langs=["es", "fr"],
    use_api=True  # Uses OpenRouter API for better translation
)

# Process audio file
results = pipeline.process_audio("lecture.wav")

# Generate WebVTT captions
webvtt_content = results['webvtt']

# Analyze performance
print(f"Total latency: {results['latencies']['total_pipeline']:.2f}s")
```

## Citation

If you use this code or build upon this work, please cite:

```bibtex
@inproceedings{shah2026multilingual,
  title={Real-Time Multilingual Captioning for Deaf/Hard-of-Hearing Users via Large Language Models},
  author={Shah, Bhumika and Panda, Satya Narayana},
  booktitle={Proceedings of the 23rd International Web for All Conference},
  year={2026},
  
}
```

## Future Work

- [ ] Enhanced error correction mechanisms
- [ ] Expanded language support (20+ languages)
- [ ] Adaptive quality-latency trade-offs
- [ ] User-specific personalization
- [ ] Integration with streaming platforms
- [ ] Mobile/edge deployment optimization

## Acknowledgments

We thank the D/HoH community members who provided feedback on early system prototypes and contributed to the development of this research.

## Contact

**Bhumika Shah**  
Email: Bhumishah000.bs@gmail.com  
Institution: University of Cumberlands

**Satya Narayana Panda**  
Email: spand14@unh.newhaven.edu  
Institution: University of New Haven

## Conference

**Web4All 2026**  
23rd International Web for All Conference  
April 13-14, 2026   
[https://www.w4a.info/2026/](https://www.w4a.info/2026/)

## License

This project is released for academic research purposes. Please cite our paper if you use this code.

---

**Note:** This is a work-in-progress system. User evaluation with D/HoH participants is planned to assess comprehension, usability, and perceived accessibility across multiple languages.
