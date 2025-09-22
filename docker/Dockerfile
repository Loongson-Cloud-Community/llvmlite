ARG base=lcr.loongnix.cn/pypa/manylinux_2_38_loongarch64
FROM $base

ARG llvm_version=20.1.8

RUN yum install -y wget

RUN pipx install ninja -i https://lpypi.loongnix.cn/loongson/pypi/+simple

RUN mkdir -p /tmp/llvm &&\
    cd /tmp/llvm &&\
    wget -qO - https://github.com/llvm/llvm-project/releases/download/llvmorg-${llvm_version}/llvm-project-${llvm_version}.src.tar.xz | tar -xzf - --strip-components=1 &&\
    mkdir llvm-build &&\
    cd llvm-build &&\
    cmake -G Ninja -DCMAKE_INSTALL_PREFIX=/opt/llvm-${llvm_version} -DLLVM_ENABLE_PROJECTS="clang" -DCMAKE_BUILD_TYPE=Release -DLLVM_TARGETS_TO_BUILD="LoongArch" ../llvm -DCMAKE_C_FLAGS="-mcmodel=medium -mno-relax" &&\
    ninja && ninja install && rm -rf /tmp/*

ENV PATH="/opt/llvm-${llvm_version}/bin:$PATH"

