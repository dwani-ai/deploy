GPT OSS - arm64

pip install https://github.com/dwani-ai/vllm-arm64/releases/download/v0.0.6/vllm-0.10.1.dev398+g9edd1db02.d20250806-cp312-cp312-linux_aarch64.whl


 export VLLM_USE_FLASHINFER_MXFP4_BF16_MOE=1

 export VLLM_USE_TRTLLM_ATTENTION=1
export VLLM_USE_TRTLLM_DECODE_ATTENTION=1
export VLLM_USE_TRTLLM_CONTEXT_ATTENTION=1

vllm serve openai/gpt-oss-20b

vllm serve openai/gpt-oss-120b



- Steps to build 
git clone https://github.com/vllm-project/vllm.git

cd vllm

pip install torch==2.7.1 torchaudio==2.7.1 torchvision --index-url https://download.pytorch.org/whl/cu128


python use_existing_torch.py 

pip install --upgrade setuptools twine setuptools-scm


pip install -r requirements/cuda.txt

export MAX_JOBS=16
export NVCC_THREADS=4
export TORCH_CUDA_ARCH_LIST=""
export VLLM_TARGET_DEVICE=cuda

python setup.py bdist_wheel

pip install dist/*.whl

GptOssForCausalLM
--- 

https://blog.vllm.ai/2025/08/05/gpt-oss.html


https://docs.vllm.ai/projects/recipes/en/latest/OpenAI/GPT-OSS.html



docker run --gpus all \
    -p 8000:8000 \
    --ipc=host \
    vllm/vllm-openai:gptoss \
    --model openai/gpt-oss-20b

uv pip install --pre vllm==0.10.1+gptoss \
    --extra-index-url https://wheels.vllm.ai/gpt-oss/ \
    --extra-index-url https://download.pytorch.org/whl/nightly/cu128 \
    --index-strategy unsafe-best-match

vllm serve openai/gpt-oss-120b

https://huggingface.co/blog/welcome-openai-gpt-oss


RoPe - https://arxiv.org/abs/2104.09864

MoE - https://arxiv.org/abs/1701.06538


GPT3- https://arxiv.org/abs/2005.14165

GPT 2 - 
https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf


https://cookbook.openai.com/articles/run-nvidia


https://developer.nvidia.com/blog/delivering-1-5-m-tps-inference-on-nvidia-gb200-nvl72-nvidia-accelerates-openai-gpt-oss-models-from-cloud-to-edge/

