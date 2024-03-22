# Quantization- Mistral AI
This quantization is done with Google Colab, If you are performing in your local machine/ VM's please remove "! and % " signs
This is exclusively for Linux users
## Clone the git repo (original Llama.cpp)
```
!git clone https://github.com/ggerganov/llama.cpp
%cd llama.cpp
```
# MAKE

## Build
To build llama.cpp you have three different options. But I've used only 2
```
!make
```
### Obtain the model and Weights from Huggingface CLI
```
#install dependencies
!pip install -U "huggingface_hub[cli]"
#exclude the ".bin" files and obtain all other things
!huggingface-cli download mistralai/Mistral-7B-v0.1 --local-dir ./models --exclude "*.bin"
```


## Prepare and Quantize
inside llama.cpp directory perform this:
```
#install Python dependencies
!python3 -m pip install -r requirements.txt
!python3 convert.py models
```
## Quantize the model
```
! ./quantize ./models/ggml-model-f32.gguf ./models/ggml-model-Q4_K_M.gguf Q4_K_M
```
## Infrence the model
```
# start inference on a gguf model
!./main -m ./models/ggml-model-Q4_K_M.gguf -n 128
```
#Cmake
Using Cmake:
```
mkdir build
cd build
cmake ..
cmake --build . --config Release
```
Load the model and weights as mentioned above


## Quantize the model
```
! .build/bin/quantize ./models/ggml-model-f32.gguf ./models/ggml-model-Q4_K_M.gguf Q4_K_M
```
## Infrence the model
```
# start inference on a gguf model
!.build/bin/main -m ./models/ggml-model-Q4_K_M.gguf -n 128
```
