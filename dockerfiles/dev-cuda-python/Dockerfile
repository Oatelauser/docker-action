# ubuntu22.04
FROM nvidia/cuda:12.2.2-runtime-ubuntu22.04

LABEL authors="Oatelauser"

RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && apt update \
    && apt install -y wget build-essential zlib1g-dev libssl-dev libffi-dev \
    # 编译构建python
    && wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tar.xz \
    && tar -xf Python-3.12.0.tar.xz && cd Python-3.12.0 \
    && ./configure --enable-optimizations --with-lto \
    && make -j$(nproc) && make install \
    && cp /usr/local/bin/python3.12 /usr/local/bin/python \
    && cp cp /usr/local/bin/pip3 /usr/local/bin/pip \
    && cd .. && rm -rf Python-3.12.0.tar.xz Python-3.12.0 \
    # 设置pip镜像源
    && pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/ \
    # 构建SSH
    && apt install -y openssh-server \
    && mkdir /var/run/sshd \
    # 设置SSH账户密码
    && echo 'root:root' | chpasswd \
    && sed -i 's/\#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    # 清理数据
    && apt clean autoclean \
    && apt autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/log/*.log


EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]