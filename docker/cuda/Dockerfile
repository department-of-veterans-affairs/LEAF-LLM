# CUDA version depends on host version
FROM nvidia/cuda:12.6.3-devel-ubi9

RUN dnf -y update
RUN dnf -y install git cmake gcc gcc-c++

WORKDIR /app
RUN git clone https://github.com/ggerganov/llama.cpp

WORKDIR /app/llama.cpp

# Tested version
RUN git checkout 8d947136546773f6410756f37fcc5d3e65b8135d

# Select relevant CUDA Architectures: https://github.com/ggml-org/llama.cpp/blob/master/docs/build.md#override-compute-capability-specifications
RUN cmake -B build -DGGML_CUDA=ON -DCMAKE_CUDA_ARCHITECTURES="86" -DCMAKE_EXE_LINKER_FLAGS=-Wl,--allow-shlib-undefined -DLLAMA_CURL=OFF
RUN cmake --build build --config Release -j $(nproc)

WORKDIR /app/llama.cpp/build/bin
