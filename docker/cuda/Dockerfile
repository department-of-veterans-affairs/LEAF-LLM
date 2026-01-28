# CUDA version depends on host version
FROM nvidia/cuda:12.9.1-devel-ubi9

RUN dnf -y update
RUN dnf -y install git cmake gcc gcc-c++

# Workaround: default gcc on UBI9 doesn't support modern CPUs
RUN dnf -y install gcc-toolset-14

WORKDIR /app
RUN git clone https://github.com/ggerganov/llama.cpp

WORKDIR /app/llama.cpp

# Tested version
ARG COMMIT_HASH=f6b533d898ce84bae8d9fa8dfc6697ac087800bf
RUN git checkout master
RUN git pull
RUN git checkout ${COMMIT_HASH}

# Select relevant CUDA Architectures if autodetection doesn't work: https://github.com/ggml-org/llama.cpp/blob/master/docs/build.md#override-compute-capability-specifications
# Workaround: (CC and CCX) default gcc on UBI9 doesn't support modern CPUs
RUN CC="/opt/rh/gcc-toolset-14/root/usr/bin/gcc" CXX="/opt/rh/gcc-toolset-14/root/usr/bin/g++" cmake -B build -DGGML_CUDA=ON -DCMAKE_EXE_LINKER_FLAGS=-Wl,--allow-shlib-undefined -DLLAMA_CURL=OFF -DCMAKE_CUDA_ARCHITECTURES="86"
RUN cmake --build build --config Release -j $(nproc)

WORKDIR /app/llama.cpp/build/bin
