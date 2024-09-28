## Requirement

1. Install `python 3.10` from [Python Releases for Windows](https://www.python.org/downloads/windows/). I test on `3.10.11`.
2. Install `CUDA` from [CUDA Toolkit - Downloads](https://developer.nvidia.com/cuda-downloads)`. I used `CUDA 12.1.0`.
3. Check [PyTorch - Start Locally](https://pytorch.org/get-started/locally/).

Check it:

```
python --version
nvcc -V
echo %CUDA_PATH%
# echo %CUDA_PATH_V12_1%
```

## [Ollama](https://ollama.com/)

```sh
ollama pull codellama 
ollama pull starcoder2:3b
ollama pull starcoder2:7b
ollama pull nomic-embed-text
ollama list
```

VSCode → Sidebar → Continue → Configure Continue:

```sh
{
  "models": [
    {
      "apiBase": "http://127.0.0.1:11434/",
      "model": "codellama",
      "provider": "ollama",
      "title": "CodeLlama"
    }
  ]
}
```

↪ [Configuring Ollama and Continue VS Code Extension for Local Coding Assistant](https://dev.to/manjushsh/configuring-ollama-and-continue-vs-code-extension-for-local-coding-assistant-48li)

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `ollama-linux-arm64.tgz` from [Ollama - Releases](https://github.com/ollama/ollama/releases).

```sh
chmod +x ollama-linux-arm64
sudo mv ollama-linux-arm64 /usr/bin/ollama
ollama serve
```

In new session:

```sh
ollama pull tinyllama
ollama run tinyllama
```

↪ [Running Ollama on the Raspberry Pi](https://pimylifeup.com/raspberry-pi-ollama)  
↪ [Run LLMs Locally on Raspberry Pi Using Ollama AI](https://itsfoss.com/raspberry-pi-ollama-ai-setup/)
<!-- --8<-- [end:ubuntu-22-arm] -->

## [LM Studio](https://lmstudio.ai/)

↪ [LM Studio有魔法加持依然无法连网的解决办法](https://juejin.cn/post/7373961220585603124)

Discover → Select the LLM → Choose a download option → Check `Full GPU Offload Possible`, recommend `Q4_0` → Download

I have tried:

```
Meta Llama 3.1 8B
Mistral 7B v0.3
```

For translating subtitle, I download `q4_k_m` from [Qwen2.5-7B-Instruct-GGUF](https://huggingface.co/Qwen/Qwen2.5-7B-Instruct-GGUF/tree/main). Put them into `C:\Users\<User>\.cache\lm-studio\models\lmstudio-community\Qwen2.5-7B-Instruct-GGUF`.

Chat → Select a model to load → Select the LLM

As server:

Developer → Enable CORS (On) → Serve on Local Network (on) → Select a model to load → Start Server

## [Text generation web UI](https://github.com/oobabooga/text-generation-webui)

```sh
git clone --depth=1 https://github.com/oobabooga/text-generation-webui
cd text-generation-webui
```

Download models, liked [Meta-Llama-3.1-8B-Instruct-GGUF](https://huggingface.co/lmstudio-community/Meta-Llama-3.1-8B-Instruct-GGUF).

```sh
mklink /D text-generation-webui\models\models--lmstudio-community--Meta-Llama-3.1-8B-Instruct-GGUF models--lmstudio-community--Meta-Llama-3.1-8B-Instruct-GGUF
```

```sh
start_windows.bat
```

Visit `localhost:7860` → Model → Select `Model` → Select `Model loader` → load

If there is no problem, you will see:

## [SakuraLLM](https://github.com/SakuraLLM/SakuraLLM)

```sh
git clone --depth=1 https://github.com/SakuraLLM/SakuraLLM
cd SakuraLLM
pip install torch torchvision torchaudio xformers --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.llamacpp.txt
pip install llama-cpp-python --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cu121
```

I used `q2k` of [Sakura-14B-Qwen2beta-v0.9.2-GGUF](https://huggingface.co/SakuraLLM/Sakura-14B-Qwen2beta-v0.9.2-GGUF). Put it into `./models/`.

Used as API:

```sh
python server.py --trust_remote_code --model_name_or_path ./models/sakura-14b-qwen2beta-v0.9.2-q2k.gguf --model_version 0.9 --no-auth --llama_cpp --use_gpu --log debug
```

Used as command:

```sh
python translate_novel.py --trust_remote_code --model_name_or_path ./models/sakura-14b-qwen2beta-v0.9.2-q2k.gguf --model_version 0.9 --no-auth --llama_cpp --use_gpu --log debug --text_length 512 --data_path <novel.txt> --output_path <novel_translated.txt>
```

```sh
python translate_epub.py --trust_remote_code --model_name_or_path ./models/sakura-14b-qwen2beta-v0.9.2-q2k.gguf --model_version 0.9 --no-auth --llama_cpp --use_gpu --log debug --text_length 512 --data_path <novel.epub> --output_folder <novel_epub>
```

↪ [各种推理引擎的使用说明](https://github.com/SakuraLLM/SakuraLLM/blob/main/usage.md)  
↪ [Sakura模型部署教程-本地运行-Transformers模型](https://github.com/SakuraLLM/tutorial/blob/main/tutorial-local-transformers.md)

## [Lobe Chat](https://github.com/lobehub/lobe-chat)

↪ [Deploy LobeChat with Vercel](https://lobehub.com/docs/self-hosting/platform/vercel)  
↪ [Deploying Server Database Version on Vercel](https://lobehub.com/docs/self-hosting/server-database/vercel)

## [GPT-Subtrans](https://github.com/machinewrapped/gpt-subtrans)

```sh
git clone --depth=1 https://github.com/machinewrapped/gpt-subtrans
python.exe -m venv venv
venv\Scripts\activate.bat
pip install -r requirements.txt
scripts\generate-cmd.bat gui-subtrans
scripts\generate-cmd.bat llm-subtrans
```

With GUI:

```sh
gui-subtrans
```

Settings → Processing:

```
Preprocess Subtitles (On)
Postprocess Translation (On)
Save Preprocessed Subtitles (On)
```

Open file → Select <Subtitle> → Project Settings → Entry `Movie Name`, `Target Language` → Start

## [ChatGPT API SRT Subtitle Translator](https://github.com/Cerlancism/chatgpt-subtitle-translator)

```sh
git clone --depth=1 https://github.com/Cerlancism/chatgpt-subtitle-translator
cd chatgpt-subtitle-translator
cd web
npm ci
npm run build
npm run dev
```

Visit `localhost:3000/chatgpt-subtitle-translator`.

## [Langflow](https://github.com/langflow-ai/langflow)

```sh
git clone --depth=1 https://github.com/langflow-ai/langflow
cd langflow
make backend
```

And:

```sh
make frontend
```

↪ [Contributing to Langflow](https://github.com/langflow-ai/langflow/blob/main/CONTRIBUTING.md)

## [faster-whisper-webui](//huggingface.co/spaces/aadnk/faster-whisper-webui)

```sh
git clone https://huggingface.co/spaces/aadnk/faster-whisper-webui
cd faster-whisper-webui
python -m venv venv
venv\Scripts\activate.bat
pip install .../torch-2.2.2+cu121-cp310-cp310-win_amd64.whl
pip install -r requirements-fasterWhisper.txt 
```

```sh
git clone https://github.com/Temmie-Flakes/Simple_Speech_Recognition
cd Simple_Speech_Recognition
```

Imitate `RunBaseModel.bat` and Write your `.bat` liked:

```
venv\Scripts\python.exe Open_WebUI.py --cache-dir "modelsCache" --repo-id "guillaumekln/faster-whisper-medium"

PAUSE
```

Run your `.bat`. Then wait for the download to complete.

Add local-models into `config.json5` liked:

```json
"models": [
  {
    "name": "local-medium",
    "url": "...\\Simple_Speech_Recognition\\modelsCache\\faster-whisper-medium",
    "type": "filesystem"
  },
]
```

According to your needs, edit some arguments of `config.json5` liked:

```
"input_audio_max_duration": 600, // → -1
"server_port": 7860,
"whisper_implementation": "faster-whisper",
"default_model_name": "medium", // → "local-medium"
"vad_parallel_devices": "", // → "0"
"auto_parallel": false, // → true
"output_dir": null, // → "D:/home"
"language": null, // → "Chinese"
```

Used as cli liked:

```sh
python cli.py --whisper_implementation "faster-whisper" --vad "silero-vad" --auto_parallel true --vad_parallel_devices "0" --model "local-medium" --language "Chinese" --initial_prompt="对于普通话句子，以中文简体输出" --diarization_num_speakers 1 --output_dir "D:\home" yourvoice.mp3
```

Start with webui:

```sh
python.exe app.py --input_audio_max_duration -1 --server_name 127.0.0.1 --server_port 7830 --whisper_implementation "faster-whisper" --default_model_name "local-medium" --vad_parallel_devices "0" --auto_parallel true --output_dir "D:/home" 
```

Visit `localhost:7830/`.

Refer to [whisper_VAD模型的区别及用途](https://sharegpt.com/c/VzJhWpV), the Coding Wizard(gpt-3.5-turbo)'s suggestion——You can try transcribing audiobook with `Silero-VAD-Expand-Into-Gaps`. And try transcribing with `Silero-VAD-Skip-Gaps`.

- [Running Locally](https://huggingface.co/spaces/aadnk/faster-whisper-webui/blob/main/README.md#running-locally)  
- [Enabling custom Japanese model](https://huggingface.co/spaces/aadnk/faster-whisper-webui/discussions/5)  
- [services.py](https://github.com/usoonees/logseq-whisper-subtitles-server/blob/main/logseq_whisper_subtitles_server/services.py)

↪ [Segmentation Fault when loading pyannote/speaker-diarization-3.0 in rockylinux9/python3 environment](https://github.com/pyannote/pyannote-audio/issues/1499)

## [Whishper](https://github.com/pluja/whishper)

## [AudioCraft](https://github.com/facebookresearch/audiocraft)

## [TTS](https://github.com/coqui-ai/TTS)

Get and install `espeak-ng-X64.msi` from [espeak-ng - Releases](https://github.com/espeak-ng/espeak-ng/releases).

```sh
git clone --depth=1 https://github.com/coqui-ai/TTS
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install -e .
```

```sh
tts --list_models
tts --model_name "tts_models/multilingual/multi-dataset/xtts_v2" --list_speaker_idxs
tts --model_name "tts_models/multilingual/multi-dataset/xtts_v2" --list_language_idxs
tts --device cuda --model_name "tts_models/multilingual/multi-dataset/xtts_v2" --speaker_idx "Claribel Dervla" --language_idx "en" --text "<Text>" --out_path temp.wav
ffplay -autoexit temp.wav
```

↪ [How can I run Mozilla TTS/Coqui TTS training with CUDA on a Windows system?](https://stackoverflow.com/questions/66726331/how-can-i-run-mozilla-tts-coqui-tts-training-with-cuda-on-a-windows-system)

## [MeloTTS](https://github.com/myshell-ai/MeloTTS)

```sh
git clone --depth=1 https://github.com/myshell-ai/MeloTTS
python -m venv venv
venv\Scripts\activate.bat
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install -e .
python -m unidic download
```

```sh
melo "Hello" temp.wav --language EN
melo --device cuda --language EN "<Text>" temp.wav && ffplay -autoexit temp.wav
```

Start with Web UI:

```sh
pip install gradio==4.21.0
python melo/app.py
```

↪ [运行web_demo_gradio.py报gbk解码错误，cli和streamlit则可以正常运行](https://github.com/THUDM/ChatGLM3/discussions/1009)

## [Bark](https://github.com/suno-ai/bark)

```sh
git lfs install
git clone https://huggingface.co/spaces/suno/bark
cd bark
pyenv install -l | findstr 3.7
pyenv install 3.8.10
pyenv local 3.8.10
pip install git+https://github.com/suno-ai/bark.git
pip install numpy gradio hf_transfer
pip install torch torchvision torchaudio gradio --index-url https://download.pytorch.org/whl/cu121
python app.py
```

```sh
python -m bark --text "<Text>" --output_filename "temp.wav"
ffplay -autoexit temp.wav
```

## [Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

```sh
git clone --depth=1 https://github.com/AUTOMATIC1111/stable-diffusion-webui
cd stable-diffusion-webui
python -m venv venv
venv\Scripts\activate.bat
pip install torch torchvision torchaudio xformers --index-url https://download.pytorch.org/whl/cu121
pip install hf_transfer
```

Edit `webui-user.bat`:

```sh
set COMMANDLINE_ARGS=--xformers --port 7050
set XFORMERS_MORE_DETAILS=1
```

Download and put checkpoint the `.safetensors` into `models/Stable-diffusion`. Liked [Voxel XL](https://civitai.com/models/118536/voxel-xl).

```sh
webui-user.bat
```

↪ [Manual Installation](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-NVidia-GPUs#manual-installation)  
↪ [How on earth can I install xformers?](https://github.com/AUTOMATIC1111/stable-diffusion-webui/discussions/9802#discussioncomment-5894895)  
↪ [Installing xFormers](https://github.com/facebookresearch/xformers#installing-xformers)  
↪ [Command Line Arguments and Settings](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings)

### [Lobe Theme](https://github.com/canisminor1990/sd-webui-lobe-theme)

1. Extensions → Available → Load from → Search `lobe` → Install `Lobe Theme`
2. Extensions → Installed → Apply and restartUI

## [IOPaint](https://github.com/Sanster/IOPaint)

```sh
git clone --depth=1 https://github.com/Sanster/IOPaint.git
cd IOPaint/web_app
nvm install 20.17.0
nvm use 20.17.0
npm install
npm run build
cp -r dist/ ../iopaint/web_app
```

Create `.env.local`:

```
VITE_BACKEND=http://127.0.0.1:7840
```

```sh
npm run dev
```

```sh
cd ..
python -m venv venv
venv\Scripts\activate.bat
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
python main.py start --model lama --port 7840
```

With [Interactive Segmentation](https://www.iopaint.com/plugins/interactive_seg):

```sh
iopaint start --model=lama --device=cpu --port=7840 --enable-interactive-seg --interactive-seg-device=cuda
```

With [GFPGAN](https://www.iopaint.com/plugins/GFPGAN):

```sh
pip install gfpgan
iopaint start --model=lama --device=cpu --port=7840 --enable-gfpgan --gfpgan-device cuda
```

With [RealESRGAN](https://www.iopaint.com/plugins/RealESRGAN):

```sh
pip install realesrgan
iopaint start --model=lama --device=cpu --port=7840 --enable-realesrgan --realesrgan-model RealESRGAN_x4plus --realesrgan-device cuda
```

With [Remove Background](https://www.iopaint.com/plugins/rembg):

```sh
pip install rembg
iopaint start --model=lama --device=cpu --port=7840 --enable-remove-bg
```

With [RestoreFormer](https://www.iopaint.com/plugins/RestoreFormer):

```sh
pip install realesrgan
iopaint start --model=lama --device=cpu --port=7840 --enable-restoreformer --restoreformer-device cuda
```

With [Anime Segmentation](https://www.iopaint.com/plugins/anime_seg):

```sh
iopaint start --model=lama --device=cpu --port=7840 --enable-anime-seg
```

## [RapidVideOCR](https://github.com/SWHL/RapidVideOCR) (TBD)

↪ [VideoSubFinder提取字幕关键帧教程](https://juejin.cn/post/7203362527082053691)  
↪ [在线demo](https://swhl.github.io/RapidVideOCR/docs/online_demo/)

## [docTR](https://github.com/mindee/doctr)

```sh
git clone --depth=1 https://github.com/mindee/doctr
cd doctr
python -m venv venv
venv\Scripts\activate.bat
pip install "python-doctr[torch]"
pip install -r demo/pt-requirements.txt
```

```sh
set USE_TORCH=1
streamlit run demo/app.py
```

Or edit `demo/app.py`:

```py
import os
os.environ["USE_TORCH"] = "1"
```

```sh
streamlit run demo/app.py
```