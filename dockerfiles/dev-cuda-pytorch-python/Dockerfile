# 操作系统ubuntu22.04
FROM pytorch/pytorch:2.5.1-cuda12.1-cudnn9-devel

LABEL authors="Oatelauser"

RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && apt update \
    && apt install -y openssh-server netcat \
    # 设置SSH账户密码
    && mkdir /var/run/sshd \
    && echo 'root:root' | chpasswd \
    && sed -i 's/\#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    # 设置pip镜像源
    && pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/ \
    && apt clean autoclean \
    && apt autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/log/*.log


EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd", "-D"]