FROM redhat/ubi9

RUN dnf -y update
RUN dnf -y install git cmake gcc gcc-c++ openblas-devel

# Workaround: default gcc on UBI9 doesn't support modern CPUs
RUN dnf -y install gcc-toolset-14

WORKDIR /app
RUN git clone https://github.com/ggerganov/llama.cpp

WORKDIR /app/llama.cpp

# Tested version
ARG COMMIT_HASH=9961d244f2df6baf40af2f1ddc0927f8d91578c8
RUN git checkout master
RUN git pull
RUN git checkout ${COMMIT_HASH}

# Workaround: (CC and CCX) default gcc on UBI9 doesn't support modern CPUs
RUN CC="/opt/rh/gcc-toolset-14/root/usr/bin/gcc" CXX="/opt/rh/gcc-toolset-14/root/usr/bin/g++" cmake -B build -DGGML_BLAS=ON -DGGML_BLAS_VENDOR=OpenBLAS -DLLAMA_CURL=OFF

RUN cmake --build build --config Release -j $(nproc)

WORKDIR /app/llama.cpp/build/bin
