Setup

- vllm + gemma3 Setup
    - Add daemon.json to /etc/docker
    - https://github.com/dwani-ai/deploy/blob/main/files/daemon.json

    - sudo systemctl restart docker

    - sudo docker run --runtime nvidia -it --rm -p 9000:9000 slabstech/dwani-vllm

    - export HF_TOKEN='my-nsma-is-what'

    - vllm serve google/gemma-3-4b-it --served-model-name gemma3 --host 0.0.0.0 --port 9000 --gpu-memory-utilization 0.9 --tensor-parallel-size 1 --max-model-len 16384     --dtype bfloat16 


- docs-indic-server
  -- ### Documents 
  - https://github.com/dwani-ai/docs-indic-server.git
```bash
git clone https://github.com/dwani-ai/docs-indic-server.git
cd docs-indic-server

python -m venv --system-site-packages venv

source venv/bin/activate

pip install -r requirements.txt
pip install "numpy<2.0"

python src/server/docs_api.py  --host 0.0.0.0 --port 7861
```

- Dependencies
  - decord
  - olmocr
  - ffmpeg

- ffmpeg
  - sudo apt update
  - sudo apt install ffmpeg
  - ffmpeg -version

sudo apt update
sudo apt install cmake ffmpeg build-essential python3-dev

sudo apt install pkg-config libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libswresample-dev  libavfilter-dev 

sudo apt-get install poppler-utils

find /usr/lib* -name libavformat.so



sudo ln -s /usr/lib/aarch64-linux-gnu/libavformat.so /usr/lib/libavformat.so
sudo ln -s /usr/lib/aarch64-linux-gnu/libavcodec.so /usr/lib/libavcodec.so
sudo ln -s /usr/lib/aarch64-linux-gnu/libavutil.so /usr/lib/libavutil.so
sudo ln -s /usr/lib/aarch64-linux-gnu/libavfilter.so /usr/lib/libavfilter.so
sudo ln -sf /usr/lib/aarch64-linux-gnu/libavdevice.so.58 /usr/lib/libavdevice.so

sudo ln -s /usr/lib/aarch64-linux-gnu/libswresample.so  /usr/lib/libswresample.so

sudo ldconfig
# Add other FFmpeg libs as 

cmake .. -DUSE_CUDA=1 -DCMAKE_BUILD_TYPE=Release -DFFMPEG_LIB_DIR=/usr/lib/aarch64-linux-gnu -DFFMPEG_INCLUDE_DIR=/usr/include


```bash
cd
mkdir external
cd external
git clone --recursive https://github.com/dmlc/decord

cd decord

mkdir build && cd build

export CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda
export CUDACXX=/usr/local/cuda/bin/nvcc

nvcc --version

cmake .. -DUSE_CUDA=1 -DCMAKE_BUILD_TYPE=Release -DFFMPEG_DIR=/usr

cmake .. -DUSE_CUDA=1 -DCMAKE_BUILD_TYPE=Release

make

cd ../python
python3 setup.py install --user
pip install "numpy<2.0"

```
<!-- 
// pwd=$PWD
// echo "PYTHONPATH=$PYTHONPATH:$pwd" >> ~/.bashrc
// source ~/.bashrc
### option 2: install with setuptools
-->

- olmocr

```bash
cd ../../
git clone  https://github.com/allenai/olmocr.git

cd olmocr

pip install --upgrade pip setuptools wheel packaging

 // copy ppyproject.toml
pip install -e .
cd ../../dwani_org/gh-200-docs-indic-server/
pip install "numpy<2.0"
```
in olmocr :  pyproject.toml - remove sql-kernem and sglang
set python version to 3.10


python src/server/docs_api.py  --host 0.0.0.0 --port 7861


--

- dwani-api-server

git clone https://github.com/dwani-ai/dwani-api-server.git
cd dwani-api-server

python -m venv venv
source venv/bin/activate

pip install -r requirements.txt
docker build -t dwani/api-server-arm64:latest -f Dockerfile .


---

Proxy Server

sudo apt install nano
Install [docker in VM](docker_setup_vm.md) - 

docker build -t dwani/proxy-server:latest -f Dockerfile .


docker push dwani/proxy-server:latest

docker run --env-file .env -p 80:80 dwani/proxy-server:latest


--

Translate Server

- https://github.com/dwani-ai/indic-translate-server.git
```bash
git clone https://github.com/dwani-ai/indic-translate-server.git
cd indic-translate-server

python -m venv --system-site-packages venv

source venv/bin/activate
pip install --upgrade pip setuptools wheel packaging cython

pip install torch==2.7.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

#pip install -r requirements.txt

pip install -e git+https://github.com/VarunGumma/IndicTransToolkit.git@main#egg=IndicTransToolkit

pip install fastapi uvicorn  "numpy<2.0"
python src/server/translate_api.py --host 0.0.0.0 --port 7862 --device cpu
```



- ### ASR - Automatic Speech Recognition / Speech to Text
    - https://github.com/dwani-ai/asr-indic-server.git
```bash
git clone https://github.com/dwani-ai/asr-indic-server.git
cd asr-indic-server
    
python -m venv --system-site-packages venv
source venv/bin/activate

pip install -r requirements.txt


python src/multilingual/asr_api.py --host 0.0.0.0 --port 7863 --device cuda

```

ASR - English

curl --silent --remote-name https://raw.githubusercontent.com/speaches-ai/speaches/master/compose.yaml
curl --silent --remote-name https://raw.githubusercontent.com/speaches-ai/speaches/master/compose.cuda.yaml
export COMPOSE_FILE=compose.cuda.yaml

sudo docker compose -f compose.cuda.yaml up -d

curl -X 'POST' \
  'http://localhost:8000/v1/models/Systran/faster-whisper-large-v3' \
  -H 'accept: application/json' \
  -d ''


  curl -X 'POST' \
  'http://localhost:8000/v1/models/speaches-ai/Kokoro-82M-v1.0-ONNX' \
  -H 'accept: application/json' \
  -d ''


  -

- ### TTS - Text to Speech 
- https://github.com/dwani-ai/tts-indic-server
```bash
git clone https://github.com/dwani-ai/tts-indic-server
cd tts-indic-server
git checkout gh-200
export HF_TOKEN='this-my-token'
python -m venv  venv
source venv/bin/activate
pip install wheel packaging

pip install -r requirements.txt

 pip uninstall torch torchaudio torchvision

pip install torch==2.7.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128

python src/gh200/main.py --host 0.0.0.0 --port 7864 --config config_two
```

