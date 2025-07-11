# deploy - dwani.ai - Multimodal Inference API

dwani.ai is a self-hosted GenAI platform for multimodal inference, supporting text, images, documents, and speech in Indian languages. 

---

## Table of Contents

- [Overview](#overview)
- [Component Setup](#component-setup)
- [Model Dependencies](#model-dependencies)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

**dwani.ai** enables:
- Text and image inference
- Document extraction, translation, and querying
- Speech-to-text (ASR) and text-to-speech (TTS) for Indian languages
- Translation across major Indian languages
- Load balancing and API orchestration

---

## Component Setup

Each service is modular and can be set up independently. See linked docs for detailed instructions.

| Component        | Description                                  | Setup Guide                                      |
|------------------|----------------------------------------------|--------------------------------------------------|
| **vllm server**  | Text + image inference                       | [vllm_setup.md](docs/vllm_setup.md)              |
| **docs-api-server** | Document extraction, translation, query   | [docs_setup.md](docs/docs_setup.md)              |
| **translate_server** | Indian language translation              | [translate_server.md](docs/translate_server.md)   |
| **tts-server**   | Text to speech (Indian languages)            | [tts-server.md](docs/tts-server.md)              |
| **asr-server**   | Automatic Speech Recognition                 | [asr_server.md](docs/asr_server.md)              |
| **api-server**   | API gateway & Swagger setup                  | [api_server_setup.md](docs/api_server_setup.md)   |
| **proxy-server** | Load balancer                                | [proxy_setup_vm.md](docs/proxy_setup_vm.md)       |

---

![dwani API](images/dwani-inference.drawio.png "Engine") 

---

## Model Dependencies

The following models are required for full functionality:

| Task                                     | Models Used                                     |
|-------------------------------------------|-------------------------------------------------|
| **Text + Vision**                        | `google/gemma-3-27b-it`, `google/gemma-3-12b-it`, `google/gemma-3-4b-it` |
| **Text**                                 | `Qwen/Qwen3-32B`, `Qwen/Qwen3-14B`              |
| **Vision**                               | `vikhyatk/moondream2`                           |
| **Speech Synthesis / Text to Speech**     | `ai4bharat/IndicF5`, `onnx-community/Kokoro-82M-v1.0-ONNX` |
| **Translation**                          | `ai4bharat/IndicTrans3-beta`, `ai4bharat/indictrans2-indic-indic-1B`, `ai4bharat/indictrans2-en-indic-1B`, `ai4bharat/indictrans2-indic-en-1B` |
| **Automatic Speech Recognition / ASR**    | `ai4bharat/indic-conformer-600m-multilingual`, `Systran/faster-whisper-large-v3` |
| **Text Analysis**                        | `ai4bharat/Cadence`                             |

---

## Contributing

Contributions are welcome! Please open issues or submit pull requests for improvements.

---

## License

This project is licensed under the [MIT License](LICENSE).

---
