FROM redhat/ubi9

RUN dnf -y update
RUN dnf -y install git cmake gcc gcc-c++ openblas-devel

WORKDIR /app
RUN git clone https://github.com/ggerganov/llama.cpp

WORKDIR /app/llama.cpp

# Tested version
ARG COMMIT_HASH=98bab638fb28cf95a5a66dd2d51b40d6c8f6d69a
RUN git checkout master
RUN git pull
RUN git checkout ${COMMIT_HASH}

RUN cmake -B build -DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS -DLLAMA_CURL=OFF
RUN cmake --build build --config Release -j $(nproc)

WORKDIR /app/llama.cpp/build/bin
