# deploy - dwani.ai - Document Analytics Platform

dwani.ai is a Document Analytics Platform

- Designed for Indian + European languages. 
- It can be self-hosted and provides multimodal inference, supporting
    - text
    - images 
    - documents
    - speech

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
| **vllm server**  | Text + image inference                       | [docs/v2/vllm_deplpy.md](docs/v2/vllm_deploy.md) |
| **docs-api-server** | Document extraction, translation, query   | [docs_setup.md](docs/docs_setup.md)              |
| **translate_server** | Indian language translation              | [translate_server.md](docs/translate_server.md)   |
| **tts-server**   | Text to speech (Indian languages)            | [tts-server.md](docs/tts-server.md)              |
| **asr-server**   | Automatic Speech Recognition                 | [asr_server.md](docs/asr_server.md)              |
| **api-server**   | API gateway & Swagger setup                  | [api_server_setup.md](docs/api_server_setup.md)   |
| **proxy-server** | Load balancer                                | [proxy_setup_vm.md](docs/proxy_setup_vm.md)       |

---

![dwani API](images/dwani-inference.drawio.png "Engine") 

---

- build vllm for arm64 / GH200/GB200
  - [docs/v2/README.md](docs/v2/README.md)

- deployment is optimised for arm64, VRAM > 80GB 

- vllm 
  - python wheel installation
    - 3.10
      - pip install https://github.com/dwani-ai/vllm-arm64/releases/download/v0.0.5/vllm-0.10.1.dev0+g6d8d0a24c.d20250726-cp310-cp310-linux_aarch64.whl
    - 3.12
      - pip install https://github.com/dwani-ai/vllm-arm64/releases/download/v.0.0.4/vllm-0.10.1.dev0+g6d8d0a24c.d20250726-cp312-cp312-linux_aarch64.whl
  - docker images
    - dwani/vllm-openai:latest
    -   sudo docker run --gpus all -p 8000:8000 vllm/vllm-openai --model Qwen/Qwen3-0.6B --port 8000

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
