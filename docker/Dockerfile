FROM redhat/ubi9

RUN dnf update
RUN dnf -y install git cmake gcc gcc-c++ openblas-devel

WORKDIR /app
RUN git clone https://github.com/ggerganov/llama.cpp

WORKDIR /app/llama.cpp

# Tested version
RUN git checkout 8d947136546773f6410756f37fcc5d3e65b8135d

RUN cmake -B build -DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS -DLLAMA_CURL=OFF
RUN cmake --build build --config Release -j $(nproc)

WORKDIR /app/llama.cpp/build/bin
