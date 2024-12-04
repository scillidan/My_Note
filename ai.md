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

## Update

```sh
git pull
```

Or:

```sh
git reset --hard
git merge <branch>
git pull
```

## [Ollama](https://ollama.com/)

```sh
ollama pull codellama 
ollama pull starcoder2:3b
# ollama pull starcoder2:7b
ollama pull nomic-embed-text
# ollama pull mxbai-embed-large
# ollama pull jina/jina-embeddings-v2-base-en
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

```sh
ollama pull qwen2.5:7b
ollama run qwen2.5:7b
```

1. Immersive Translate → Developer settings → Enable Beta Testing Features
2. Translation Services → Custom API → Edit → API URL → `http://127.0.0.1:11434` → Verify service

↪ [Immersive Translate - Custom Interface Translation](https://immersivetranslate.com/en/docs/services/custom/)

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

Used on local network, Add these into PATH:

- `OLLAMA_HOST=0.0.0.0`
- `OLLAMA_ORIGINES=*`

↪ [Ollama Connection issues FAQ help](https://github.com/Mintplex-Labs/anything-llm/issues/1640)

## [LM Studio](https://lmstudio.ai/)

1. Install LM Studio
2. Go to `C:\Users\<User>\AppData\Local\LM-Studio\app-*\resources\app\.webpack\main`
3. Find in folder, replace `huggingface.co` to `hf-mirror.com`

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

I used `q2k` of [Sakura-14B-Qwen2beta-v0.9.2-GGUF](https://huggingface.co/SakuraLLM/Sakura-14B-Qwen2beta-v0.9.2-GGUF). Put it into `models/`.

Used as API:

```sh
python server.py --trust_remote_code --model_name_or_path models/sakura-13b-lnovel-v0.9b-Q2_K.gguf --model_version 0.9 --no-auth --llama_cpp --use_gpu --log debug
```

Used as command:

```sh
python translate_novel.py --trust_remote_code --model_name_or_path models/sakura-13b-lnovel-v0.9b-Q2_K.gguf --model_version 0.9 --no-auth --llama_cpp --use_gpu --log debug --text_length 512 --data_path <novel.txt> --output_path <novel_translated.txt>
```

```sh
python translate_epub.py --trust_remote_code --model_name_or_path models/sakura-13b-lnovel-v0.9b-Q2_K.gguf --model_version 0.9 --no-auth --llama_cpp --use_gpu --log debug --text_length 512 --data_path <novel.epub> --output_folder <novel_epub>
```

↪ [各种推理引擎的使用说明](https://github.com/SakuraLLM/SakuraLLM/blob/main/usage.md)  
↪ [Sakura模型部署教程-本地运行-Transformers模型](https://github.com/SakuraLLM/tutorial/blob/main/tutorial-local-transformers.md)

## [Lobe Chat](https://github.com/lobehub/lobe-chat)

↪ [Deploy LobeChat with Vercel](https://lobehub.com/docs/self-hosting/platform/vercel)  
↪ [Deploying Server Database Version on Vercel](https://lobehub.com/docs/self-hosting/server-database/vercel)

<!-- --8<-- [start:docker-arm] -->
```sh
sudo docker run -d -p 3210:3210 -e ACCESS_CODE=lobe66 --name lobe-chat lobehub/lobe-chat
docker ps
```

Crontab Automatic Update Script (Optional):

```sh
vim ~/auto-update-lobe-chat.sh
```

```
#!/bin/bash
# auto-update-lobe-chat.sh

# Set up proxy (optional)
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890

# Pull the latest image and store the output in a variable
output=$(docker pull lobehub/lobe-chat:latest 2>&1)

# Check if the pull command was executed successfully
if [ $? -ne 0 ]; then
  exit 1
fi

# Check if the output contains a specific string
echo "$output" | grep -q "Image is up to date for lobehub/lobe-chat:latest"

# If the image is already up to date, do nothing
if [ $? -eq 0 ]; then
  exit 0
fi

echo "Detected Lobe-Chat update"

# Remove the old container
echo "Removed: $(docker rm -f Lobe-Chat)"

# Run the new container
echo "Started: $(docker run -d --network=host --env-file /path/to/lobe.env --name=Lobe-Chat --restart=always lobehub/lobe-chat)"

# Print the update time and version
echo "Update time: $(date)"
echo "Version: $(docker inspect lobehub/lobe-chat:latest | grep 'org.opencontainers.image.version' | awk -F'"' '{print $4}')"

# Clean up unused images
docker images | grep 'lobehub/lobe-chat' | grep -v 'lobehub/lobe-chat-database' | grep -v 'latest' | awk '{print $3}' | xargs -r docker rmi > /dev/null 2>&1
echo "Removed old images."
```

```sh
crontab -e
```

```
0 * * * * /home/<username>/auto-update-lobe-chat.sh >> /home/<username>/auto-update-lobe-chat.log 2>&1
```

↪ [Lobe Chat - Docker Deployment Guide](https://lobehub.com/docs/self-hosting/platform/docker)  
↪ [[Bug] Ollama service is unavailable](https://github.com/lobehub/lobe-chat/issues/2337)  
↪ [Hitting a Wall Trying to get Ollama to work with LobeChat or any other app (works fine in CLI in the container)](https://www.reddit.com/r/unRAID/comments/1ccxqu6/hitting_a_wall_trying_to_get_ollama_to_work_with/)
<!-- --8<-- [end:docker-arm] -->

## [Next.js AI Chatbot](https://github.com/vercel/ai-chatbot) (Cache)

Fork it.

```sh
git clone --depth=1 https://github.com/<user>/ai-chatbot
cd ai-chatbot
npm install -g vercel
vercel link
vercel env pull
pnpm install
pnpm dev
```

## [Khoj](https://github.com/khoj-ai/khoj) (Cache)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir ~/.khoj
cd ~/.khoj
wget https://raw.githubusercontent.com/khoj-ai/khoj/master/docker-compose.yml
podman-compose up -d
podman ps
```

↪ [Khoj - Self-Host](https://docs.khoj.dev/get-started/setup/?server=docker&os=linux)
<!-- --8<-- [end:docker-arm] -->

## [autoflow](https://github.com/pingcap/autoflow) (Cache)

<!-- --8<-- [start:docker-arm] -->
↪ [Deploy with Docker & Docker Compose](https://tidb.ai/docs/deploy-with-docker)
<!-- --8<-- [end:docker-arm] -->

## [Verba](https://github.com/weaviate/Verba) (Cache)

<!-- --8<-- [start:docker-arm] -->
```sh
git clone --depth=1 https://github.com/weaviate/Verba
cd Verba
vim .env
```

```
OLLAMA_URL=http://<ollama_host>:11434
OLLAMA_MODEL=llama3.1
OLLAMA_EMBED_MODEL=mxbai-embed-large
```

```sh
sudo docker compose --env-file .env up -d --build
```
<!-- --8<-- [end:docker-arm] -->

## [AutoRAG](https://github.com/Marker-Inc-Korea/AutoRAG) (Cache)

<!-- --8<-- [start:docker-arm] -->
↪ [Run AutoRAG with 🐳 Docker](https://github.com/Marker-Inc-Korea/AutoRAG/blob/main/docs/source/install.md#1-build-the-docker-image)
<!-- --8<-- [end:docker-arm] -->

## [Perplexica](https://github.com/ItzCrazyKns/Perplexica)

```sh
git clone --depth=1 https://github.com/ItzCrazyKns/Perplexica
cd Perplexica/ui
cp .env.example .env
npm install
npm run build
cd ..
cp sample.config.toml config.toml
npm install
npm run build
```

You can edit `config.toml` to fill some fields liked:

```
[API_ENDPOINTS]
OLLAMA = "http://127.0.0.1:11434"
```

Create `start.bat`:

```sh
@echo off

cd "C:\Users\User\Git\Perplexica\ui"
start npm run start
cd "C:\Users\User\Git\Perplexica"
start npm run start

pause
```

↪ [How to Contribute to Perplexica](https://github.com/ItzCrazyKns/Perplexica/blob/master/CONTRIBUTING.md)

## [Dify](https://github.com/langgenius/dify)

<!-- --8<-- [start:docker-arm] -->
```sh
git clone --depth=1 https://github.com/langgenius/dify
cd dify/docker
cp .env.example .env
docker compose up -d
```

Update:

```sh
cd dify/docker
docker compose down
git pull origin main
docker compose pull
docker compose up -d
```

↪ [Deploy with Docker Compose](https://docs.dify.ai/getting-started/install-self-hosted/docker-compose)
<!-- --8<-- [end:docker-arm] -->

1. Dify → <user> → Settings → Model Provider
2. Ollama → Setup
    ```
    Model Name `llama3.1:8b`
    Base URL `http://<host>:11434`
    ```
3. Ollama → Add Model
    ```
    Model Type `Text Embedding`
    Model Name `mxbai-embed-large:latest`
    Base URL `http://<host>:11434`
    ```
    ```
    Model Type `Text Embedding`
    Model Name `jina/jina-embeddings-v2-base-en`
    Base URL `http://<host>:11434`
    ```
4. OpenAI → Setup
    ```
    API Key `<api_key>`
    API base `https://api.openai.com`
    ```
5. OpenAI → Show Models
6. Dify → Studio → Chatbot → Create from Blank
    ```
    APP icon & name `llama 3.1`
    ```
7. Studio → llama 3.1 → `<model>` CHAT → `llama3.1:8b`
8. Dify → Knowledge → Create Knowledge → Upload files → Save & Process → Go to Documents
    ```
    Index mode `Economical`
    ```
9. Studio → llama 3.1 → Context → Add → <knowledge>

↪ [本地部署Dify基于Llama 3.1和OpenAI创建聊天机器人与知识库](https://dify101.com/market/marketing-copy-clone-machine)

### More

- [Content Editing](https://dify101.com/market/claude-thinking-Content-Editing)
- [E-commerce Specialist](https://dify101.com/market/claude-thinking-E-commerce-Specialist)
- [ai-stemm-writing-supervisor](https://dify101.com/market/ai-stemm-writing-supervisor)
- [Data Analyst](https://dify101.com/market/claude-thinking-Data-Analyst)
- [Technical Support](https://dify101.com/market/claude-thinking-Technical-Support)
- [Translator](https://dify101.com/market/claude-thinking-Translator)
- [Educator](https://dify101.com/market/claude-thinking-Educator)
- [Child Psychotherapist](https://dify101.com/market/claude-thinking-Child-Psychotherapist)
- [Legal Assistant](https://dify101.com/market/claude-thinking-Legal-Assistant)
- [Insurance Claims Specialist](https://dify101.com/market/claude-thinking-Insurance-Claims-Specialist)
- [Cross-Platform Copywriting with Dify](https://dify101.com/market/url-to-cross-platform-copywriting-with-dify)
- [Wordplay](https://dify101.com/market/wordplay)
- [Claude Prompt: 汉语新解](https://dify101.com/market/hanyuxinjie)
- [Ancient Script Scholar](https://dify101.com/market/claude-thinking-Ancient-Script-Scholar)

## [Langflow](https://github.com/langflow-ai/langflow) (Cache, noARM)

```sh
mkdir langflow
cd langflow
python.exe -m venv venv
venv\Scripts\activate.bat
pip install langflow
```

↪ [Install Langflow](https://docs.langflow.org/get-started-installation)

## [Local RAG Chatbot](https://github.com/datvodinh/rag-chatbot)

Install [Ollama](https://ollama.com/), [ngrok](https://ngrok.com/).

```sh
git clone --depth=1 https://github.com/datvodinh/rag-chatbot
cd rag-chatbot
python.exe -m venv venv
venv\Scripts\activate.bat
pip install .
pip install hf_transfer
python -m rag_chatbot --host localhost & ngrok http 4321
```

## [phidata](https://github.com/phidatahq/phidata) (Cache)

```sh
git clone --depth=1 https://github.com/phidatahq/phidata
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
pip install -e .
pip install ollama
```

Create `rag_agent.py`:

```py
from phi.agent import Agent
# from phi.model.openai import OpenAIChat
from phi.model.ollama import Ollama
from phi.knowledge.pdf import PDFUrlKnowledgeBase
from phi.vectordb.lancedb import LanceDb, SearchType

db_uri = "tmp/lancedb"
# Create a knowledge base from a PDF
knowledge_base = PDFUrlKnowledgeBase(
    # urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"],
    urls=["https://raw.githubusercontent.com/scillidan/file/main/pdf/%E7%BA%A2%E6%A5%BC%E6%A2%A6%E8%84%82%E8%AF%84%E6%B1%87%E6%A0%A1%E6%9C%AC_Kolistan%E6%B1%87%E6%A0%A1.pdf"],
    # Use LanceDB as the vector database
    vector_db=LanceDb(table_name="recipes", uri=db_uri, search_type=SearchType.vector),
)
# Load the knowledge base: Comment out after first run
knowledge_base.load(upsert=True)

agent = Agent(
    # model=OpenAIChat(id="gpt-4o"),
    model=Ollama(id="llama3"),
    # Add the knowledge base to the agent
    knowledge=knowledge_base,
    show_tool_calls=True,
    markdown=True,
)
agent.print_response("How do I make chicken and galangal in coconut milk soup")
```

```sh
pip install lancedb tantivy pypdf sqlalchemy pgvector psycopg[binary] openai
python rag_agent.py
```

↪ [RAG Agent](https://docs.phidata.com/agents#rag-agent)

Create `playground.py`:

```py
from phi.agent import Agent
# from phi.model.openai import OpenAIChat
from phi.model.ollama import Ollama
from phi.storage.agent.sqlite import SqlAgentStorage
from phi.tools.duckduckgo import DuckDuckGo
from phi.tools.yfinance import YFinanceTools
from phi.playground import Playground, serve_playground_app

web_agent = Agent(
    name="Web Agent",
    role="Search the web for information",
    # model=OpenAIChat(id="gpt-4o"),
    model=Ollama(id="llama3"),
    tools=[DuckDuckGo()],
    storage=SqlAgentStorage(table_name="web_agent", db_file="agents.db"),
    add_history_to_messages=True,
    markdown=True,
)

finance_agent = Agent(
    name="Finance Agent",
    role="Get financial data",
    model=Ollama(id="llama3"),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True, company_news=True)],
    instructions=["Always use tables to display data"],
    storage=SqlAgentStorage(table_name="finance_agent", db_file="agents.db"),
    add_history_to_messages=True,
    markdown=True,
)

app = Playground(agents=[finance_agent, web_agent]).get_app()

if __name__ == "__main__":
    serve_playground_app("playground:app", reload=True)
```

```sh
phi auth
pip install fastapi[standard] sqlalchemy duckduckgo-search yfinance
python playground.py
```

↪ [Agent UI](https://docs.phidata.com/ui)

## [GraphRAG Local](https://github.com/severian42/GraphRAG-Local-UI) (Cache)

## GraphRAG-Scrapy-FastAPI-Chainlit (Cache)

↪ [GraphRAG高级用法:GraphRAG+scrapy爬虫构建GitHub项目智能知识库！AI赋能程序员:FastAPI+Chainlit打造代码助手](https://www.youtube.com/watch?v=CvCVFH7bsAk)  
↪ [GraphRAG+chainlit实现跨文档智能检索分析](https://blog.stoeng.site/20240704.html)

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

## [PDFMathTranslate](https://github.com/Byaidu/PDFMathTranslate) (TBD)

## [TinyTroupe](https://github.com/microsoft/TinyTroupe) (Cache)

## [Whishper](https://github.com/openai/whisper)

```sh
git clone --depth=1 https://github.com/openai/whisper
cd whisper
python -m venv venv
venv\Scripts\activate.bat
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install .
C:\Users\<User>\Git\whisper\venv\Scripts\whisper.exe --model large-v3 --device cuda --language Chinese --output_format srt <input>
```

## [Insanely Fast Whisper (CLI)](https://github.com/ochen1/insanely-fast-whisper-cli)

```sh
git clone --depth=1 https://github.com/ochen1/insanely-fast-whisper-cli
cd insanely-fast-whisper-cli
```

Edit `requirements.txt`:

```
# git+https://github.com/huggingface/transformers
```

```sh
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch>=2.1.1 torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
pip install transformers>=4.36 hf_transfer
python insanely-fast-whisper.py <audio>
python insanely-fast-whisper.py --model openai/whisper-large-v3-turbo --device cuda:0 --dtype float32 --batch-size 8 --chunk-length 30 <audio>
```

## [whisply](https://github.com/tsmdt/whisply) (Cache)

```sh
git clone --depth=1 https://github.com/tsmdt/whisply
cd whisply
```

Edit `setup.py`:

```py
with open("README.md", "r") as fh:
    long_description = fh.read()
```

To:

```py
with open("README.md", "r", encoding='utf-8') as fh:
    long_description = fh.read()
```

```sh
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install .
pip uninstall numpy
pip install numpy==1.26.3
pip install hf_transfer
whisply --hf_token <token> --translate --subtitle --annotate --model large-v3 --lang zh --device gpu --files <input>
```

↪ [Incompatible with NumPy 2.0...](https://github.com/Vaibhavs10/insanely-fast-whisper/issues/233)

## [Simple_Speech_Recognition](https://github.com/Temmie-Flakes/Simple_Speech_Recognition)

```sh
git clone --depth=1 https://github.com/Temmie-Flakes/Simple_Speech_Recognition
cd Simple_Speech_Recognition
python -m venv venv
venv\Scripts\activate.bat
pip install torch --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
pip install hf_transfer
```

1. Read `RunBaseModel.bat`.
2. Create other `.bat` you need liked `RunMediumModel.bat`.
3. Run `.bat`.

## [faster-whisper-webui](https://huggingface.co/spaces/aadnk/faster-whisper-webui)

```sh
git clone https://huggingface.co/spaces/aadnk/faster-whisper-webui
cd faster-whisper-webui
python -m venv venv
venv\Scripts\activate.bat
set "CUDA_PATH=C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8"
echo %CUDA_PATH%
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu118
pip install -r requirements-fasterWhisper.txt
pip install -r requirements.txt
pip install hf_transfer
cp config.json5 config.json5.bak
```

Edit `config.json5` liked:

```json
"models": [
  {
    "name": "medium",
    "url": "Simple_Speech_Recognition/modelsCache/faster-whisper-medium",
    "type": "filesystem"
  },
  {
    "name": "large-v2",
    "url": "Simple_Speech_Recognition/modelsCache/faster-whisper-large-v2",
    "type": "filesystem"
  },
  {
    "name": "large-v3",
    "url": "Simple_Speech_Recognition/modelsCache/faster-whisper-large-v3",
    "type": "filesystem"
  },
]
"input_audio_max_duration": -1,
"server_port": 7830,
"whisper_implementation": "faster-whisper",
"default_model_name": "medium",
"vad_parallel_devices": 0,
"auto_parallel": true,
"output_dir": "<OutputDir>",
"language": "Chinese",
```

Used with command liked:

```sh
python cli.py --whisper_implementation "faster-whisper" --vad "silero-vad-skip-gaps" --auto_parallel true --vad_parallel_devices 0 --model "large-v2" --language "Chinese" --initial_prompt="对于普通话句子，以中文简体输出" --diarization_num_speakers 1 --auth_token <hf_token> --output_dir "C:/Users/User/Downloads" <input>
```

Used with webui:

```sh
python.exe app.py --input_audio_max_duration -1 --server_name 127.0.0.1 --server_port 7830 --whisper_implementation "faster-whisper" --default_model_name "large-v2" --vad_parallel_devices 0 --auto_parallel true --auth_token <hf_token> --output_dir "C:/Users/User/Downloads"
```

Visit `localhost:7830`.

Refer to [whisper_VAD模型的区别及用途](https://sharegpt.com/c/VzJhWpV), you can try `Silero-VAD-Skip-Gaps` for transcribing, and try `Silero-VAD-Expand-Into-Gaps` for transcribing audiobook.

Start with command:

```
open-cli http://127.0.0.1:7820 && cd faster-whisper-webui && venv\Scripts\python.exe app.py --server_name 127.0.0.1 --server_port 7830 --input_audio_max_duration -1 --whisper_implementation "faster-whisper" --default_model_name "large-v2" --vad_parallel_devices "0" --auto_parallel true --output_dir "<OptputDir>"
```

↪ [Running Locally](https://huggingface.co/spaces/aadnk/faster-whisper-webui/blob/main/README.md#running-locally)  
↪ [Enabling custom Japanese model](https://huggingface.co/spaces/aadnk/faster-whisper-webui/discussions/5)  
↪ [services.py](https://github.com/usoonees/logseq-whisper-subtitles-server/blob/main/logseq_whisper_subtitles_server/services.py)  
↪ [Segmentation Fault when loading pyannote/speaker-diarization-3.0 in rockylinux9/python3 environment](https://github.com/pyannote/pyannote-audio/issues/1499)

## [faster-whisper-GUI](https://github.com/CheshireCC/faster-whisper-GUI) (Cache)

## [Whisper-WebUI](https://github.com/jhj0517/Whisper-WebUI)

```sh
git clone --depth=1 https://github.com/jhj0517/Whisper-WebUI
cd Whisper-WebUI
python -m venv venv
venv\Scripts\activate.bat
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
pip install hf_transfer
user-start-webui.bat
```

## [Whishper](https://github.com/pluja/whishper)

## [Voice-Pro](https://github.com/abus-aikorea/voice-pro) (Cache)

```sh
git clone --depth=1 https://github.com/abus-aikorea/voice-pro
cd voice-pro
python -m venv venv
venv\Scripts\activate.bat
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
pip install hf_transfer
start.bat
```

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

## [F5-TTS](https://github.com/SWivid/F5-TTS)

```sh
git clone --depth=1 https://github.com/SWivid/F5-TTS
cd F5-TTS
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install -e .
pip install hf_transfer
f5-tts_infer-gradio
```

## [Bark](https://github.com/suno-ai/bark)

```sh
git lfs install
git clone https://huggingface.co/spaces/suno/bark
cd bark
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch --index-url https://download.pytorch.org/whl/cu121
pip install hf_transfer
pip install -e .
python -m bark --text "<Text>" --output_filename "temp.wav"
ffplay -autoexit temp.wav
```

## [Bark Web UI](https://github.com/makawy7/bark-webui)

```sh
git clone --depth=1 https://github.com/makawy7/bark-webui
cd bark-webui
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch --index-url https://download.pytorch.org/whl/cu121
pip install .
pip install gradio
python webui.py
```

## [Fish Speech](https://github.com/fishaudio/fish-speech) (Cache)

Edit `API_FLAGS.txt`:

```
--listen 0.0.0.0:<port> \
```

```sh
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install https://github.com/AnyaCoder/fish-speech/releases/download/v0.1.0/triton_windows-0.1.0-py3-none-any.whl
pip install hf_transfer
pip install -e .
start.bat
```

## [AudioCraft](https://github.com/facebookresearch/audiocraft) (Cache)

```sh
git clone --depth=1 https://github.com/facebookresearch/audiocraft
cd audiocraft
vim requirements_user.txt
```

```
aiofiles==23.2.1
annotated-types==0.7.0
antlr4-python3-runtime==4.9.3
anyio==3.7.1
audiocraft==1.3.0
audioread==3.0.1
av==11.0.0
blis==0.7.11
catalogue==2.0.10
certifi==2024.8.30
cffi==1.17.1
charset-normalizer==3.4.0
click==8.1.7
cloudpathlib==0.20.0
cloudpickle==3.1.0
colorlog==6.8.2
confection==0.1.5
cymem==2.0.8
decorator==4.4.2
demucs==4.0.1
docopt==0.6.2
dora_search==0.1.12
einops==0.8.0
encodec==0.1.1
exceptiongroup==1.2.2
fastapi==0.115.2
ffmpy==0.4.0
filelock==3.16.1
flashy==0.0.2
fsspec==2024.6.1
gradio==5.1.0
gradio_client==1.4.0
h11==0.14.0
httpcore==1.0.6
httpx==0.27.2
huggingface-hub==0.26.0
hydra-colorlog==1.2.0
hydra-core==1.3.2
idna==3.10
Jinja2==3.1.4
joblib==1.4.2
julius==0.2.7
lameenc==1.7.0
langcodes==3.4.1
language_data==1.2.0
lazy_loader==0.4
librosa==0.10.2.post1
lightning-utilities==0.11.8
llvmlite==0.43.0
marisa-trie==1.2.1
markdown-it-py==3.0.0
MarkupSafe==2.1.5
mdurl==0.1.2
mpmath==1.3.0
msgpack==1.1.0
murmurhash==1.0.10
networkx==3.4.1
num2words==0.5.13
numba==0.60.0
numpy==1.26.4
nvidia-cublas-cu12==12.1.3.1
nvidia-cuda-cupti-cu12==12.1.105
nvidia-cuda-nvrtc-cu12==12.1.105
nvidia-cuda-runtime-cu12==12.1.105
nvidia-cudnn-cu12
nvidia-cufft-cu12==11.0.2.54
nvidia-curand-cu12==10.3.2.106
nvidia-cusolver-cu12==11.4.5.107
nvidia-cusparse-cu12==12.1.0.106
# nvidia-nccl-cu12==2.18.1
nvidia-nvjitlink-cu12==12.6.77
nvidia-nvtx-cu12==12.1.105
omegaconf==2.3.0
openunmix==1.3.0
orjson==3.10.9
packaging==24.1
pandas==2.2.2
pillow==10.4.0
platformdirs==4.3.6
pooch==1.8.2
preshed==3.0.9
protobuf==3.20.3
pycparser==2.22
pydantic==2.9.2
pydantic_core==2.23.4
pydub==0.25.1
Pygments==2.18.0
python-dateutil==2.9.0.post0
python-multipart==0.0.12
pytz==2024.2
PyYAML==6.0.2
regex==2024.9.11
requests==2.32.3
retrying==1.3.4
rich==13.9.2
ruff==0.7.0
safetensors==0.4.5
scikit-learn==1.5.2
scipy==1.10.1
semantic-version==2.10.0
sentencepiece==0.2.0
shellingham==1.5.4
six==1.16.0
smart-open==7.0.5
sniffio==1.3.1
soundfile==0.12.1
soxr==0.5.0.post1
spacy==3.7.5
spacy-legacy==3.0.12
spacy-loggers==1.0.5
srsly==2.4.8
starlette==0.40.0
submitit==1.5.2
sympy==1.13.3
thinc==8.2.5
threadpoolctl==3.5.0
tokenizers==0.19.1
tomlkit==0.12.0
torch==2.1.0
torchaudio==2.1.0
torchdata==0.7.0
torchmetrics==1.5.0
torchtext==0.16.0
torchvision==0.16.0
tqdm==4.66.5
transformers==4.44.2
treetable==0.2.5
# triton==2.1.0
typer==0.12.5
typing_extensions==4.12.2
tzdata==2024.2
urllib3==2.2.3
uvicorn==0.32.0
wasabi==1.1.3
weasel==0.4.1
websockets==12.0
wrapt==1.16.0
xformers==0.0.22.post7
```

```sh
python -m pip install -e .
```

↪ [pip dependencies](https://github.com/facebookresearch/audiocraft/issues/493)

## [epub2tts](https://github.com/aedocw/epub2tts) (Cache)

```sh
git clone --depth=1 https://github.com/aedocw/epub2tts
cd epub2tts
```

Edit `requirements.txt`:

```
# deepspeed
```

```sh
pyenv local 3.11.9
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch torchaudio --index-url https://download.pytorch.org/whl/cu121
pip install coqui-tts --only-binary spacy && pip install .
epub2tts <epub> --export txt
epub2tts <txt> --engine tts --speaker "<Speaker>" --cover cover-image.jpg --sayparts
```

↪ ["Unable to import torch" error on Windows](https://github.com/aedocw/epub2tts/issues/218)

## [EPUB to Audiobook Converter](https://github.com/p0n1/epub_to_audiobook) (Cache)

```sh
git clone --depth=1 https://github.com/p0n1/epub_to_audiobook
cd epub_to_audiobook
python.exe -m venv venv
venv\Scripts\activate.bat
pip install -r requirements.txt
python main.py --tts edge --language en-US <epub> <output_folder>
```

## [ebook2audiobook](https://github.com/DrewThomasson/ebook2audiobook) (Cache)

```sh
git clone --depth=1 https://github.com/DrewThomasson/ebook2audiobook
cd ebook2audiobook
python.exe -m venv venv
venv\Scripts\activate.bat
pip install coqui-tts==0.24.2 pydub nltk beautifulsoup4 ebooklib tqdm gradio==4.44.0
python -m nltk.downloader punkt
python -m nltk.downloader punkt_tab
pip install mecab mecab-python3 unidic
python -m unidic download
python app.py
```

```sh
python app.py --headless True --use_custom_model True --ebook <ebook_file_path> --voice <target_voice_file_path> --language <language> --custom_model <custom_model_path> --custom_config <custom_config_path> --custom_vocab <custom_vocab_path>
```

## [VoxNovel](https://github.com/DrewThomasson/VoxNovel) (TBD)

## [ToonCrafter](https://github.com/Doubiiu/ToonCrafter)

```sh
git clone --depth=1 https://github.com/sdbds/ToonCrafter-for-windows
pyenv install 3.8.10
pyenv shell 3.8.10
python.exe -m venv venv
venv\Scripts\activate.bat
pip install -r requirements-windows.txt
```

1. Get `model.ckpt` from [Doubiiu/ToonCrafter](https://huggingface.co/Doubiiu/ToonCrafter/tree/main).
2. Put it into `checkpoints\tooncrafter_512_interp_v1\model.ckpt`.

```sh
set XFORMERS_FORCE_DISABLE_TRITON="1"
python gradio_app.py
```

↪ [[bug]: Error caught was: No module named 'triton'](https://github.com/invoke-ai/InvokeAI/issues/2611)

## [BallonsTranslator](https://github.com/dmMaze/BallonsTranslator)

```sh
git clone --depth=1 https://github.com/dmMaze/BallonsTranslator
cd BallonsTranslator
python -m venv venv
venv\Scripts\activate.bat
```

1. Install [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit), I used `CUDA 12.1.0`.
2. Read [PyTorch - Start Locally](https://pytorch.org/get-started/locally/).

```sh
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
python launch.py
```

BallonsTranslator → Setting → DL Module → Translator.

## [Image/Manga Translator](https://github.com/zyddnys/manga-image-translator)

![](https://img.shields.io/github/license/zyddnys/manga-image-translator?label=&style=flat-square)[![](https://img.shields.io/github/last-commit/scillidan/manga-image-translator/main?label=&style=flat-square)](https://github.com/scillidan/manga-image-translator)

```sh
git clone --depth=1 https://github.com/zyddnys/manga-image-translator
python -m venv venv
venv\Scripts\activate.bat
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121
pip install -r requirements.txt
```

Create `.env`:

```
SAKURA_API_BASE=http://127.0.0.1:5000
```

```sh
python -m manga_translator -v --mode web --use-gpu
```

## [video-subtitle-master](https://github.com/buxuku/video-subtitle-master)

```sh
git clone --depth=1 https://github.com/buxuku/video-subtitle-master
cd video-subtitle-master
yarn
yarn build:local
```

1. Get Large-v3 model from [Hugging Face](https://huggingface.co/ggerganov/whisper.cpp/resolve/main/ggml-large-v3.bin?download=true) or [HF-Mirror](https://hf-mirror.com/ggerganov/whisper.cpp/resolve/main/ggml-large-v3.bin?download=true).
2. Move it into `C:\Users\<User>\AppData\Roaming\video-subtitle-master\whisper.cpp\models`

```sh
ollama pull qwen2.5
ollama pull llama3.1
ollama serve llama3.1
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

Start with command:

```sh
open-cli http://127.0.0.1:7850/?__theme=dark && cd stable-diffusion-webui && webui-user.bat
```

### [Lobe Theme](https://github.com/canisminor1990/sd-webui-lobe-theme)

1. Extensions → Available → Load from → Search `lobe` → Install `Lobe Theme`
2. Extensions → Installed → Apply and restartUI

### Extensions

For example, Extensions → Available:

```
System Info
sd-webui-prompt_history
Model Mixer
Danbooru Prompt
Regional Prompter
Neutral Prompt
Prompt Fusion
NegPiP
SD Webui Vectorscope CC
CLIP Interrogator
ComfyUI
sd-webui-controlnet
```

Extensions → Install from URL:

```
https://github.com/bandifiu/sd-webui-prompt-style
https://github.com/DominikDoom/a1111-sd-webui-tagcomplete
https://github.com/hallatore/stable-diffusion-webui-prompt-utilities
https://github.com/ArtVentureX/sd-webui-agent-scheduler
```

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

## [SmartDoc](https://github.com/rsharvesh16/SmartDoc-Document-Processing-With-LLM) (Cache)

## [RapidVideOCR](https://github.com/SWHL/RapidVideOCR) (Cache)

1. Get `VideoSubFinder` form [SourceForge](https://sourceforge.net/projects/videosubfinder/).
2. Decompress `VideoSubFinder_*.zip` to `VideoSubFinder`.
3. Run `VideoSubFinderWXW.exe`.
4. Settings → Parameters Influencing Image Processing (Optional):
  ```
  Use CUDA GPU Acceleration `On`
  ```
5. File → Open Video
6. Run Search → When shows subtitle, Stop Search → Modify the ScanBox
7. Begin Time → `00:00:00:000` → Run Search
8. Output will be on `.\RGBImages\` 

Power by CPU:

```sh
pip install rapid_videocr
rapid_videocr -o srt -i <RGBImagesDir>
```

↪ [RapidVideOCR - 高级教程](https://swhl.github.io/RapidVideOCR/docs/tutorial/senior/)

Power by GPU:

```sh
git clone --depth=1 https://github.com/SWHL/RapidVideOCR
pip install paddlepaddle-gpu==3.0.0b1 -i https://www.paddlepaddle.org.cn/packages/stable/cu123/
pip install get-pypi-latest-version
python setup.py install
# pip uninstall onnxruntime
# pip install onnxruntime-directml
pip install rapidocr_paddle
rapid_videocr --use_cuda -o srt -i <RGBImagesDir> -s <SaveDir>
```

↪ [飞桨 - 快速安装](https://www.paddlepaddle.org.cn/install/quick)  
↪ [rapidocr_paddle - 安装及使用](https://rapidai.github.io/RapidOCRDocs/install_usage/rapidocr_paddle/usage/)

## [RapidOCR](https://github.com/RapidAI/RapidOCR) (Cache)

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

## [DocETL](https://github.com/ucbepic/docetl) (TBD)

<!-- 
https://github.com/lamm-mit/PDF2Audio
 -->