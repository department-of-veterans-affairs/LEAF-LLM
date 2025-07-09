# CUDA version depends on host version
FROM nvidia/cuda:12.6.3-devel-ubi9

RUN dnf -y update
RUN dnf -y install git cmake gcc gcc-c++

WORKDIR /app
RUN git clone https://github.com/ggerganov/llama.cpp

WORKDIR /app/llama.cpp

# Tested version
ARG COMMIT_HASH=98bab638fb28cf95a5a66dd2d51b40d6c8f6d69a
RUN git checkout master
RUN git pull
RUN git checkout ${COMMIT_HASH}

# Select relevant CUDA Architectures if autodetection doesn't work: https://github.com/ggml-org/llama.cpp/blob/master/docs/build.md#override-compute-capability-specifications
RUN cmake -B build -DGGML_CUDA=ON -DCMAKE_EXE_LINKER_FLAGS=-Wl,--allow-shlib-undefined -DLLAMA_CURL=OFF
RUN cmake --build build --config Release -j $(nproc)

WORKDIR /app/llama.cpp/build/bin
