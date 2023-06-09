---
title: 通过docker安装使用gpt-llama.cpp的LLM自主代理Auto-GPT
date: '2023-06-07'
slug: install-autogpt-in-docker-with-llama.cpp
tags:
  - LLMs
  - LLaMA
  - Paper
---

## 下载并配置llama.cpp项目

### 下载llama.cpp项目
```bash
git clone https://github.com/ggerganov/llama.cpp && cd llama.cpp
```

### 下载LLaMa权重文件
根据脚本`https://github.com/Elyah2035/llama-dl`使用以下磁力链接下载：
```
magnet:?xt=urn:btih:b8287ebfa04f879b048d4d4404108cf3e8014352&dn=LLaMA&tr=udp%3a%2f%2ftracker.opentrackr.org%3a1337%2fannounce
```
这里我只下载了13B的模型。
下载完成后，将权重文件放在`llama.cpp/models/LLaMA`目录下。
如下：
```bash
in ~/LLMs/llama.cpp on git:master o [21:06:43]
$ ls models/LLaMA
13B  7B  llama.sh  tokenizer.model
```
### 编译llama.cpp
在`llama.cpp`目录下执行：
```bash
make
# or make LLAMA_CUBLAS=1 # to enable cuBLAS
```
### 创建conda虚拟环境并安装依赖包
```bash
conda create -n llamacpp python=3.10
conda activate llama
pip install -r requirements.txt

```

### 生成量化版本模型

```bash
# 这里可以选择自己需要的模型，我这里选择了13B的模型。
# convert the 13B model to ggml FP16 format
python convert.py models/LLaMA/13B/

# quantize the model to 4-bits (using q4_0 method)
./quantize ./models/LLaMA/13B/ggml-model-f16.bin ./models/LLaMA/13B/ggml-model-q4_0.bin q4_0

```
### 执行测试一下能不能运行
```bash
./main -m ./models/LLaMA/13B/ggml-model-q4_0.bin -n 128
```
如果能够正常运行，会出现如下提示：
```bash
main: build = 623 (590250f)
main: seed  = 1686232798
llama.cpp: loading model from ./models/LLaMA/13B/ggml-model-q4_0.bin
llama_model_load_internal: format     = ggjt v3 (latest)
llama_model_load_internal: n_vocab    = 32000
llama_model_load_internal: n_ctx      = 512
llama_model_load_internal: n_embd     = 5120
llama_model_load_internal: n_mult     = 256
llama_model_load_internal: n_head     = 40
llama_model_load_internal: n_layer    = 40
llama_model_load_internal: n_rot      = 128
llama_model_load_internal: ftype      = 2 (mostly Q4_0)
llama_model_load_internal: n_ff       = 13824
llama_model_load_internal: n_parts    = 1
llama_model_load_internal: model size = 13B
llama_model_load_internal: ggml ctx size =    0.09 MB
llama_model_load_internal: mem required  = 2264.17 MB (+ 1608.00 MB per state)
.
llama_init_from_file: kv self size  =  400.00 MB

system_info: n_threads = 6 / 12 | AVX = 1 | AVX2 = 1 | AVX512 = 0 | AVX512_VBMI = 0 | AVX512_VNNI = 0 | FMA = 1 | NEON = 0 | ARM_FMA = 0 | F16C = 1 | FP16_VA = 0 | WASM_SIMD = 0 | BLAS = 0 | SSE3 = 1 | VSX = 0 |
sampling: repeat_last_n = 64, repeat_penalty = 1.100000, presence_penalty = 0.000000, frequency_penalty = 0.000000, top_k = 40, tfs_z = 1.000000, top_p = 0.950000, typical_p = 1.000000, temp = 0.800000, mirostat = 0, mirostat_lr = 0.100000, mirostat_ent = 5.000000
generate: n_ctx = 512, n_batch = 512, n_predict = 128, n_keep = 0


 2019 is the year for a new look, and what better way to start than with a fresh haircut? Whether you are looking for your own personalized cut or something a little more modern, we have the right stylist to achieve your desired look.
If you're looking for a hair style that can really bring out the best in you, look no further than the expertise of our stylists at Fresh Ideas Hair Salon. With over 30 years of experience, you can be certain we will give you a cut that is just right for your face shape and skin tone. We
llama_print_timings:        load time = 26628.92 ms
llama_print_timings:      sample time =    49.99 ms /   128 runs   (    0.39 ms per token)
llama_print_timings: prompt eval time =   353.32 ms /     2 tokens (  176.66 ms per token)
llama_print_timings:        eval time = 32074.79 ms /   127 runs   (  252.56 ms per token)
llama_print_timings:       total time = 58777.76 ms
```
至此llama.cpp项目配置完成。

## 下载并配置gpt-llama.cpp项目
### 下载gpt-llama.cpp项目
```bash
git clone https://github.com/keldenl/gpt-llama.cpp.git && cd gpt-llama.cpp
```
官方建议为如下的目录结构：
```bash
   dir
   ├── llama.cpp
   │   ├── models
   │   │   └── <YOUR_.BIN_MODEL_FILES_HERE>
   │   └── main
   └── gpt-llama.cpp
```
### 安装依赖
```bash
npm install
# 注意node版本应在18.0.0以上，否则会抱错：ReferenceError: ReadableStream is not defined。
```
### 运行
```bash
PORT=8000 npm start
```
### 测试
通过官方文档中的方式测试：
`https://github.com/keldenl/gpt-llama.cpp#running-a-gpt-powered-app`

修改应用中的`BASE_URL`为`http://192.168.1.115:8000`，API密钥为模型路径（相对路径，绝对路径都可）。
如果配置成功，那么应用会成功回复。

## 下载并配置Auto-GPT项目
### 下载Auto-GPT项目

```bash
git clone https://github.com/DGdev91/Auto-GPT.git DGdev91-Auto-GPT # clone DGdev91's fork
cd DGdev91-Auto-GPT
git checkout b349f2144f4692de7adb9458a8888839f48bd95c # checkout the PR change
```
DGdev91的PR #2594 https://github.com/Significant-Gravitas/Auto-GPT/pull/2594 可以使用LLaMa，该项目目前master分支能否正常使用还没有试。

### 安装依赖
```bash
pip install --upgrade pip
pip install -r requirements.txt
```
### 修改配置
```
cp .env.template .env

vim .env
```

```
OPENAI_API_BASE_URL=http://192.168.1.115:8000/v1
EMBED_DIM=5120
#OPENAI_API_KEY= ../llama.cpp/models/vicuna/13B/ggml-vicuna-unfiltered-13b-4bit.bin
OPENAI_API_KEY= /home/star5o/LLMs/llama.cpp/models/LLaMA/13B/ggml-model-q4_0.bin
```
### 运行
```bash
./run.sh